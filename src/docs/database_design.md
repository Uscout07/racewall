# 02. Database Design

## Purpose

This document defines the database architecture for RaceWall.

It explains:

- The entities in the system
- The relationships between them
- Why each table exists
- Which data is persistent
- Which data belongs only in the simulation engine

This document reflects the current Prisma schema and should be kept in sync with it.

---

# Database Design Principles

## 1. Store Persistent Data

The database stores information that must survive after the application closes.

Examples:

- Users
- Seasons
- Teams
- Drivers
- Tracks
- Races
- Race Results
- Race Events

Transient simulation state belongs in memory.

---

## 2. Separate Static and Dynamic Data

### Static Data

These tables rarely change.

- Team
- Driver
- Track

These are seeded once and reused.

### Dynamic Data

These change during gameplay.

- User
- Season
- Race
- RaceDriver
- RaceEvent

---

## 3. Normalize Relationships

Each entity has one responsibility.

Examples:

- A Driver belongs to one Team.
- A Race belongs to one Season.
- A Race belongs to one Track.
- A Race contains many RaceDrivers.
- A Race contains many RaceEvents.

---

## 4. Design for Expansion

The schema should support future additions such as:

- Driver transfers
- Car upgrades
- Contracts
- Sponsors
- Multiple championships

without requiring major redesign.

---

# Entity Overview

```text
User
│
└── Season
     │
     ├── Race
     │     ├── RaceDriver
     │     └── RaceEvent
     │
     └── Current Race

Track
│
└── Race

Team
│
└── Driver
      │
      ├── RaceDriver
      └── RaceEvent
```

---

# User

## Description

Represents a RaceWall player.

A user owns one or more seasons.

## Fields

| Field     | Type     | Description           |
| --------- | -------- | --------------------- |
| id        | UUID     | Primary Key           |
| email     | String   | Unique login email    |
| password  | String   | Hashed password       |
| createdAt | DateTime | Account creation date |

## Relationships

- One User has many Seasons.

---

# Team

## Description

Represents a constructor.

Teams define the baseline performance of the car.

## Fields

| Field             | Description               |
| ----------------- | ------------------------- |
| id                | Primary Key               |
| name              | Team name                 |
| color             | UI color                  |
| budget            | Constructor budget        |
| constructorRating | Overall strength          |
| racePace          | Race performance          |
| qualifyingPace    | Qualifying performance    |
| straightSpeed     | Straight-line performance |
| cornering         | Cornering ability         |
| reliability       | Reliability rating        |
| pitCrew           | Pit crew performance      |

## Relationships

- One Team has many Drivers.

---

# Driver

## Description

Represents a racing driver.

Drivers provide the human performance component of the simulation.

## Fields

| Field       | Description             |
| ----------- | ----------------------- |
| id          | Primary Key             |
| name        | Driver name             |
| pace        | Raw speed               |
| wetSkill    | Wet weather performance |
| consistency | Mistake resistance      |
| aggression  | Overtaking tendency     |
| teamId      | Owning team             |

## Relationships

- One Driver belongs to one Team.
- One Driver appears in many RaceDrivers.
- One Driver may appear in many RaceEvents.

---

# Track

## Description

Represents a racing circuit.

Tracks influence how different cars perform.

## Fields

| Field           | Description                  |
| --------------- | ---------------------------- |
| id              | Primary Key                  |
| name            | Circuit name                 |
| laps            | Total race laps              |
| straightBias    | Importance of straight speed |
| cornerBias      | Importance of cornering      |
| rainProbability | Chance of rainfall           |

## Relationships

- One Track has many Races.

## Future Fields

These may be added later:

- pitLoss
- safetyCarChance
- abrasiveness

---

# Season

## Description

Represents a championship played by one user.

A season stores long-term progress.

## Fields

| Field         | Description           |
| ------------- | --------------------- |
| id            | Primary Key           |
| userId        | Owner                 |
| name          | Season name           |
| difficulty    | Difficulty level      |
| currentRaceId | Current race          |
| completed     | Championship complete |
| createdAt     | Creation date         |

## Relationships

- Belongs to one User.
- Contains many Races.
- References one current Race.

---

# Race

## Description

Represents a single Grand Prix.

This table stores persistent race information.

## Fields

| Field       | Description          |
| ----------- | -------------------- |
| id          | Primary Key          |
| trackId     | Circuit              |
| seasonId    | Owning season        |
| weather     | Starting weather     |
| temperature | Starting temperature |
| completed   | Race finished        |

## Relationships

- Belongs to one Track.
- Belongs to one Season.
- Has many RaceDrivers.
- Has many RaceEvents.

---

# RaceDriver

## Description

Represents one driver's participation in one race.

This is effectively a junction table between Driver and Race with additional race-specific information.

## Fields

| Field          | Description                      |
| -------------- | -------------------------------- |
| id             | Primary Key                      |
| raceId         | Race                             |
| driverId       | Driver                           |
| gridPosition   | Starting position                |
| finishPosition | Final position                   |
| pitStops       | Number of pit stops              |
| bestLap        | Fastest lap                      |
| points         | Championship points earned       |
| status         | Running, Finished, Retired, etc. |

## Relationships

- Belongs to one Race.
- Belongs to one Driver.

---

# RaceEvent

## Description

Represents an important event during a race.

Examples:

- Rain begins
- Driver mistake
- Safety Car
- Mechanical failure
- Pit stop

## Fields

| Field       | Description                |
| ----------- | -------------------------- |
| id          | Primary Key                |
| raceId      | Race                       |
| driverId    | Optional affected driver   |
| lap         | Lap number                 |
| type        | Event type                 |
| description | Human-readable description |
| createdAt   | Event timestamp            |

## Relationships

- Belongs to one Race.
- Optionally belongs to one Driver.

`driverId` is nullable because some events affect the entire race rather than a specific driver.

---

# Relationship Summary

## User

```
User

1 ─────────── N Season
```

---

## Season

```
Season

1 ─────────── N Race
```

---

## Track

```
Track

1 ─────────── N Race
```

---

## Team

```
Team

1 ─────────── N Driver
```

---

## Driver

```
Driver

1 ─────────── N RaceDriver

1 ─────────── N RaceEvent
```

---

## Race

```
Race

1 ─────────── N RaceDriver

1 ─────────── N RaceEvent
```

---

# Persistent vs Runtime Data

## Stored in Database

- Users
- Seasons
- Teams
- Drivers
- Tracks
- Races
- Race Results
- Race Events

## Runtime Only

The following should remain inside the simulation engine:

- Current lap state
- Current tyre wear
- Current grip
- Temporary weather transitions
- Live race gaps
- Random seed state
- Strategy modifiers

Only the final outcome should be persisted.

---

# Why RaceDriver Exists

Instead of storing race information directly on Driver:

```
Driver

finishPosition
```

we use

```
Driver

↓

RaceDriver

↓

Race
```

This allows:

- One driver to participate in many races.
- Historical race results.
- Career statistics.
- Future multi-season support.

---

# Why RaceEvent Exists

Race events are stored separately because they provide:

- Race replay timeline
- Post-race summaries
- Live event feed
- Commentary
- Debugging

Without RaceEvent the simulation would know what happened, but the application could not explain why it happened.

---

# Future Database Extensions

Possible future models:

- SimulationConfig
- ChampionshipStanding
- CarUpgrade
- Contract
- Sponsor
- DriverTransfer
- Research
- Finance

These should be introduced only when required by gameplay.

---

# Schema Goals

The schema should remain:

- Simple
- Normalized
- Easy to understand
- Easy to query
- Easy to extend

The database stores **facts**.

The simulation engine computes **behavior**.

Keeping those responsibilities separate makes the codebase significantly easier to maintain as RaceWall grows.
