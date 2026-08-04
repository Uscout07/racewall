# 05. Domain Model

## Purpose

This document defines the core business entities of RaceWall and the responsibilities of each entity.

It is intentionally independent of:

- Express
- React
- Prisma
- PostgreSQL
- REST APIs

This document answers one question:

> **What does each object represent, and what is it responsible for?**

---

# Design Principles

Every domain object should follow these principles.

## Single Responsibility

Each object should have one clear purpose.

Objects should never perform work outside their responsibility.

---

## High Cohesion

Data and behavior that naturally belong together should remain together.

---

## Low Coupling

Objects should know as little as possible about each other.

For example:

- Drivers should not know about HTTP.
- Teams should not know about the database.
- Race simulation should not know about authentication.

---

## Pure Domain

The domain model should remain independent from frameworks.

It should be possible to run the simulation:

- inside Express
- inside a CLI
- inside a desktop application
- inside unit tests

without changing any business logic.

---

# User

## Description

Represents a player of RaceWall.

A user owns seasons.

## Responsibilities

- Register an account
- Authenticate
- Own multiple seasons
- View statistics
- Save progress

## Does NOT

- Simulate races
- Calculate standings
- Know race strategy

---

# Team

## Description

Represents a constructor participating in the championship.

A team owns exactly two drivers.

A team provides car performance characteristics.

## Properties

- Name
- Color
- Constructor Rating
- Budget
- Race Pace
- Qualifying Pace
- Straight Speed
- Cornering
- Reliability
- Pit Crew

## Responsibilities

- Define baseline car performance
- Influence qualifying pace
- Influence race pace
- Influence pit stop duration
- Influence reliability

## Does NOT

- Drive the car
- Decide strategy
- Calculate race results

---

# Driver

## Description

Represents a racing driver.

Drivers compete on behalf of a team.

## Properties

- Pace
- Consistency
- Wet Skill
- Aggression
- Tyre Management

## Responsibilities

- Produce lap pace
- Make driving mistakes
- Preserve tyres
- React to weather
- Attempt overtakes

## Does NOT

- Decide pit strategy
- Own championship standings
- Save race results

---

# Track

## Description

Represents a race circuit.

Tracks influence car performance.

## Properties

- Name
- Laps
- Straight Bias
- Corner Bias
- Rain Probability
- Pit Loss
- Safety Car Chance

## Responsibilities

- Define race length
- Influence lap time
- Influence overtaking
- Influence weather probability

## Does NOT

- Simulate weather
- Award points

---

# Season

## Description

Represents an entire championship.

A season contains multiple races.

## Responsibilities

- Track current race
- Track championship progress
- Store completed races
- Calculate championship completion

## Owns

- Races
- Driver standings
- Constructor standings

## Does NOT

- Simulate individual laps

---

# Race

## Description

Represents a single Grand Prix.

The race is the central object of the simulation.

## Owns

- Track
- Weather
- Drivers
- Current lap
- Events
- Race state

## Responsibilities

- Start the race
- Advance laps
- Finish the race
- Produce race results

## States

- Scheduled
- In Progress
- Finished
- Abandoned

## Does NOT

- Authenticate users
- Save itself to the database

---

# Race Driver

## Description

Represents a driver's participation in a specific race.

This object exists because a driver's state changes every race.

## Properties

- Grid Position
- Finish Position
- Points
- Pit Stops
- Best Lap
- Status

## Responsibilities

- Store race outcome
- Store race statistics

## Does NOT

- Calculate lap times

---

# Race Event

## Description

Represents a significant event during a race.

Examples include:

- Safety Car
- Rain Starts
- Driver Error
- Pit Stop
- Mechanical Failure
- Crash

## Responsibilities

- Record what happened
- Record when it happened
- Record who was involved

## Does NOT

- Change race state directly

The simulation engine is responsible for applying the consequences of an event.

---

# Standings

## Description

Represents the championship standings.

Standings are derived from completed race results.

## Responsibilities

- Rank drivers
- Rank constructors
- Calculate championship leader
- Calculate points

## Does NOT

- Simulate races

---

# Weather

## Description

Represents current race conditions.

Weather is mutable.

## Properties

- Weather Type
- Temperature

## Responsibilities

- Affect lap times
- Affect tyre choice
- Affect driver mistakes
- Trigger weather events

## Does NOT

- Decide pit strategy

---

# Tyre

## Description

Represents the tyre compound currently fitted to a car.

## Types

- Soft
- Medium
- Hard
- Intermediate
- Wet

## Responsibilities

- Provide grip
- Wear over time
- Determine available pace

## Does NOT

- Decide when to pit

---

# Strategy

## Description

Represents player decisions during the race.

## Available Decisions

- Push
- Balanced
- Conserve
- Pit
- Stay Out

## Responsibilities

- Modify race pace
- Modify tyre wear
- Modify risk

## Does NOT

- Directly determine finishing position

---

# Simulation Engine

## Description

The simulation engine is the heart of the game.

It applies all game rules.

## Responsibilities

- Simulate qualifying
- Simulate races
- Generate events
- Calculate lap times
- Update standings
- Apply player strategy

## Does NOT

- Authenticate users
- Read HTTP requests
- Write database queries
- Render the UI

The simulation engine should be completely framework-independent.

---

# Repository Layer

## Description

The repository layer communicates with the database.

## Responsibilities

- Save data
- Read data
- Update data
- Delete data

## Does NOT

- Contain business logic
- Simulate races

---

# Service Layer

## Description

Services coordinate business operations.

Services call repositories and the simulation engine.

## Responsibilities

- Validate business rules
- Coordinate workflows
- Return application data

## Example

RaceService may:

- Load season
- Load track
- Start simulation
- Save results

It should **not** calculate lap times itself.

---

# Controller Layer

## Description

Controllers are responsible for HTTP communication.

## Responsibilities

- Receive requests
- Validate input
- Call services
- Return responses

Controllers should remain thin.

---

# Dependency Flow

Business logic should only flow downward.

```text
HTTP Request
        │
        ▼
Controller
        │
        ▼
Service
        │
        ├──────────────┐
        ▼              ▼
Repository      Simulation Engine
        │
        ▼
Database
```

The Simulation Engine must never depend on:

- Express
- Prisma
- PostgreSQL

This keeps the core game portable.

---

# Object Relationships

```text
User
│
└── owns
    ▼
Season
│
├── contains
│   ▼
│  Race
│   │
│   ├── Track
│   ├── Weather
│   ├── Race Drivers
│   └── Race Events
│
└── produces
    ▼
Standings

Team
│
└── owns
    ▼
Drivers
```

---

# Architectural Rules

The following rules should never be violated.

1. Domain objects must not depend on Express.
2. Domain objects must not depend on Prisma.
3. Controllers must never contain business logic.
4. Services coordinate work but should not implement simulation mathematics.
5. Repositories only communicate with the database.
6. The simulation engine owns every gameplay calculation.
7. Every class should have a single responsibility.
8. Every feature should be testable without running the web server.

---

# Design Goal

The ultimate goal is to keep the simulation engine completely independent from the application framework.

If tomorrow RaceWall becomes:

- a desktop game,
- a browser game,
- a CLI simulator, or
- a mobile application,

the simulation engine should continue working without modification.

This separation allows the project to scale while keeping the codebase clean, testable, and easy to maintain.
