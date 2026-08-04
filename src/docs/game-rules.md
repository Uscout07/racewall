# 04. Game Rules

## Purpose

This document defines the gameplay rules for **RaceWall**. It describes **what** the game should do, not **how** it should be implemented.

The simulation engine will later implement the rules defined here.

---

# 1. Core Philosophy

RaceWall is **not** a driving simulator.

RaceWall is a **race strategy simulator**.

The player never controls the car directly. Instead, they take the role of the team's race engineer and strategist, making decisions before and during the race.

The game should reward:

- Good strategy
- Long-term planning
- Risk management
- Adaptability

The game should **not** reward luck alone.

Random events should create interesting strategic situations rather than decide the outcome of races by themselves.

---

# 2. Season Flow

Every season follows the same progression.

```text
Create Season
      ↓
Choose Team
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race
      ↓
Championship Updated
      ↓
Next Race
      ↓
Season Complete
```

---

# 3. Race Weekend

Each race weekend consists of three phases.

## Practice

Practice sessions are informational.

The player gains estimates about:

- Weather forecast
- Tyre degradation
- Recommended pit window
- Track grip
- Expected race pace

No championship points are awarded.

---

## Qualifying

Qualifying determines the starting grid.

Grid position depends on:

- Driver pace
- Car qualifying pace
- Track characteristics
- Weather conditions

No championship points are awarded.

---

## Race

The race is the main gameplay phase.

The player manages strategy while the simulation determines the racing outcome.

At the end of the race:

- Championship points are awarded.
- Driver standings are updated.
- Constructor standings are updated.

---

# 4. Teams

Every team has fixed characteristics.

| Attribute          | Description                       |
| ------------------ | --------------------------------- |
| Constructor Rating | Overall team strength             |
| Race Pace          | Long-run race performance         |
| Qualifying Pace    | One-lap performance               |
| Straight Speed     | Advantage on straights            |
| Cornering          | Performance in technical sections |
| Reliability        | Chance of avoiding failures       |
| Pit Crew           | Average pit stop performance      |

All team attributes range from **0–100**.

---

# 5. Drivers

Each driver has independent attributes.

| Attribute       | Description                   |
| --------------- | ----------------------------- |
| Pace            | Raw speed                     |
| Consistency     | Ability to avoid mistakes     |
| Wet Skill       | Performance in wet conditions |
| Aggression      | Overtaking willingness        |
| Tyre Management | Ability to preserve tyres     |

All driver attributes range from **0–100**.

Driver ratings remain constant during a season.

---

# 6. Tracks

Each track defines its own characteristics.

| Attribute         | Description                      |
| ----------------- | -------------------------------- |
| Laps              | Total race laps                  |
| Straight Bias     | Rewards high straight-line speed |
| Corner Bias       | Rewards cornering performance    |
| Rain Probability  | Chance of rainfall               |
| Pit Loss          | Time lost during pit stop        |
| Safety Car Chance | Base probability of Safety Car   |

Example:

**Monza**

- Straight Bias: +20
- Corner Bias: +5
- Pit Loss: 23 seconds
- Rain Probability: 18%

---

# 7. Weather

Weather conditions:

- Sunny
- Cloudy
- Light Rain
- Heavy Rain

Weather is generated before the race.

During the race, weather may change approximately every five laps.

Weather transitions should remain realistic.

Example:

```text
Sunny
    ↓
Cloudy
    ↓
Light Rain
    ↓
Heavy Rain
```

Avoid unrealistic transitions such as:

```text
Sunny
    ↓
Heavy Rain
    ↓
Sunny
```

within a single lap.

Weather influences:

- Lap times
- Tyre choice
- Driver mistakes
- Pit strategy

---

# 8. Tyres

Available tyre compounds:

- Soft
- Medium
- Hard
- Intermediate
- Wet

Each compound has:

- Grip
- Wear rate
- Ideal weather conditions

### Soft

- Highest grip
- Highest wear
- Best for qualifying
- Poor for long stints

### Medium

- Balanced grip
- Balanced wear
- Suitable for most race conditions

### Hard

- Lowest grip
- Lowest wear
- Ideal for long stints

### Intermediate

- Designed for light rain
- Poor performance on dry tracks

### Wet

- Designed for heavy rain
- Extremely poor performance on dry tracks

No tyre compound should always be the optimal choice.

---

# 9. Strategy

The player only makes decisions when strategy matters.

Available decisions include:

- Push
- Balanced
- Conserve
- Pit
- Stay Out

Each decision changes the race.

### Push

Advantages:

- Faster lap times
- More overtaking opportunities

Disadvantages:

- Increased tyre wear
- Increased mistake probability

---

### Balanced

Advantages:

- Stable performance
- Predictable tyre wear

Disadvantages:

- Few strategic advantages

---

### Conserve

Advantages:

- Reduced tyre wear
- Lower mistake probability

Disadvantages:

- Slower lap times

---

### Pit

Advantages:

- Fresh tyres
- Opportunity to react to changing conditions

Disadvantages:

- Time lost in pit lane

---

### Stay Out

Advantages:

- No pit time loss

Disadvantages:

- Increased tyre degradation
- Risk of slower pace

---

# 10. Race Events

Possible race events include:

- Safety Car
- Virtual Safety Car
- Yellow Flag
- Driver Mistake
- Lock-up
- Crash
- Mechanical Failure
- Rain Starts
- Rain Stops

Most races should contain **0–2 major events**.

Events should influence strategy rather than randomly determine the race winner.

---

# 11. Race Result

Every race generates:

- Final classification
- Championship points
- Fastest lap (future feature)
- Pit stop summary
- Strategy rating
- Expected finishing position
- Actual finishing position

Example:

```text
Expected Finish: P7

Actual Finish: P3

Result:

Overperformed
```

This allows the player to evaluate the quality of their strategic decisions.

---

# 12. Championship

Championship points:

| Position | Points |
| -------- | -----: |
| P1       |     25 |
| P2       |     18 |
| P3       |     15 |
| P4       |     12 |
| P5       |     10 |
| P6       |      8 |
| P7       |      6 |
| P8       |      4 |
| P9       |      2 |
| P10      |      1 |

Fastest lap points are **not included in Version 1**.

---

# 13. Difficulty

Difficulty should improve AI decision-making rather than artificially increasing performance.

Difficulty influences:

- Forecast accuracy
- AI strategy quality
- Driver mistake frequency
- Random event severity

Difficulty should **never** directly increase car speed.

---

# 14. Balancing Principles

The following principles guide all gameplay decisions.

- Strategy should matter more than luck.
- Better teams should usually win.
- Underdog victories should remain possible.
- Every tyre compound should have meaningful use cases.
- Weather should meaningfully change strategy.
- No single strategy should dominate every race.
- Every race should contain at least one meaningful decision.
- Random events should create opportunities rather than frustration.

---

# 15. Information & Uncertainty

The player should never have perfect information.

Examples:

- Weather forecasts are approximately 80% accurate.
- Tyre life is estimated rather than exact.
- Safety Car probability is hidden.
- Rival pit strategies remain unknown until executed.
- Mechanical failures cannot be predicted with certainty.

Players should make decisions using incomplete information, just as real race engineers do.

---

# Future Expansions

The following features are intentionally excluded from Version 1 but may be added later.

- Driver transfers
- Car upgrades
- Research & Development
- Sprint weekends
- Engine modes
- Fuel management
- DRS and ERS systems
- Driver morale
- Team finances
- Contracts
- Sponsor management
- Career mode
- Multiplayer
- Steam Workshop / Mod support

---

# Design Principle

> **Every mechanic should exist in Version 1, but every mechanic should be implemented in its simplest meaningful form.**

The goal of the first release is to validate the gameplay loop while building a solid foundation for future expansion.
