# 06. Folder Architecture

## Purpose

This document defines the project structure for the RaceWall backend.

Every folder has a single responsibility.

The architecture follows a layered design that separates:

- HTTP handling
- Business logic
- Data access
- Game simulation

This makes the project:

- Easy to understand
- Easy to test
- Easy to extend
- Easy to maintain

---

# Project Structure

```text
racewall-backend/

├── docs/
├── prisma/
├── src/
├── tests/
├── .env
├── package.json
├── tsconfig.json
└── README.md
```

---

# docs/

Contains all project documentation.

```text
docs/

01-project-overview.md

02-database-design.md

03-api-contracts.md

04-game-rules.md

05-domain-model.md

06-folder-architecture.md

07-simulation-algorithms.md

08-seed-data.md

09-ui-flow.md

10-development-roadmap.md
```

Documentation should always stay synchronized with the implementation.

---

# prisma/

Contains everything related to Prisma.

```text
prisma/

schema.prisma

migrations/

seed.ts
```

Responsibilities:

- Database schema
- Database migrations
- Seed data

Should never contain business logic.

---

# src/

Contains the application source code.

```text
src/

app.ts

server.ts

config/

controllers/

middleware/

routes/

services/

repositories/

simulation/

validators/

types/

utils/

lib/

generated/
```

---

# app.ts

Creates the Express application.

Responsibilities:

- Initialize Express
- Register middleware
- Register routes

Does NOT:

- Start the server
- Connect business logic

---

# server.ts

Starts the HTTP server.

Responsibilities:

- Load environment variables
- Connect database
- Start Express

Only executed when running the application.

---

# config/

Contains application configuration.

```text
config/

database.ts

jwt.ts

env.ts
```

Responsibilities:

- Database configuration
- JWT configuration
- Environment validation

---

# controllers/

Controllers communicate with HTTP.

```text
controllers/

auth.controller.ts

team.controller.ts

season.controller.ts

race.controller.ts

track.controller.ts

dashboard.controller.ts
```

Responsibilities:

- Receive requests
- Validate request format
- Call services
- Return HTTP responses

Controllers should remain small.

Target size:

Approximately 30–80 lines.

Controllers should never:

- Query Prisma directly
- Calculate lap times
- Contain simulation logic

---

# routes/

Defines API endpoints.

```text
routes/

auth.routes.ts

team.routes.ts

season.routes.ts

race.routes.ts

track.routes.ts

dashboard.routes.ts
```

Responsibilities:

- Define endpoints
- Attach middleware
- Connect controllers

No business logic belongs here.

---

# middleware/

Express middleware.

```text
middleware/

authenticate.ts

errorHandler.ts

requestLogger.ts

validate.ts
```

Responsibilities:

- Authentication
- Error handling
- Logging
- Request validation

---

# validators/

Contains request validation schemas.

```text
validators/

auth.validator.ts

season.validator.ts

race.validator.ts
```

Validation should happen before reaching controllers.

Recommended library:

- Zod

---

# services/

Services contain business workflows.

```text
services/

auth.service.ts

team.service.ts

season.service.ts

race.service.ts

track.service.ts

dashboard.service.ts
```

Responsibilities:

- Coordinate repositories
- Coordinate simulation
- Apply business rules

Example:

RaceService

- Load season
- Load track
- Start simulation
- Save race result

Services should NOT:

- Know HTTP
- Know Express

---

# repositories/

Repositories communicate with the database.

```text
repositories/

user.repository.ts

team.repository.ts

driver.repository.ts

season.repository.ts

race.repository.ts

track.repository.ts
```

Responsibilities:

- Create
- Read
- Update
- Delete

Repositories should contain only database operations.

No calculations.

No simulation.

---

# simulation/

The heart of RaceWall.

```text
simulation/

engine/

calculators/

events/

strategies/

state/

models/

constants/

utils/
```

Everything related to the game lives here.

---

# simulation/engine/

High-level orchestration.

```text
engine/

RaceEngine.ts

SeasonEngine.ts
```

Responsibilities:

- Start race
- Advance race
- Finish race
- Coordinate calculators

---

# simulation/calculators/

Pure mathematical calculations.

```text
calculators/

LapTimeCalculator.ts

TyreWearCalculator.ts

WeatherCalculator.ts

PitStopCalculator.ts

PositionCalculator.ts

ChampionshipCalculator.ts
```

Each calculator should have exactly one responsibility.

Example:

TyreWearCalculator

Input

```text
Soft

18 laps

Push
```

Output

```text
Wear = 63%
```

Nothing else.

---

# simulation/events/

Generates race events.

```text
events/

SafetyCarGenerator.ts

WeatherEventGenerator.ts

MechanicalFailureGenerator.ts

DriverErrorGenerator.ts
```

Responsibilities:

- Decide if events occur
- Generate event objects

They should never modify race state directly.

---

# simulation/strategies/

Player strategy effects.

```text
strategies/

PushStrategy.ts

BalancedStrategy.ts

ConserveStrategy.ts

PitStrategy.ts
```

Responsibilities:

Convert player decisions into simulation modifiers.

---

# simulation/state/

Contains live race state.

```text
state/

RaceState.ts

DriverState.ts

WeatherState.ts
```

Important:

These objects exist only while the race is running.

They are NOT database models.

---

# simulation/models/

Domain objects used by the engine.

```text
models/

Driver.ts

Team.ts

Track.ts

Race.ts

Season.ts
```

These are pure TypeScript models.

No Prisma.

No Express.

---

# simulation/constants/

Game constants.

```text
constants/

Points.ts

Weather.ts

Tyres.ts

Difficulty.ts
```

Avoid hardcoding values throughout the engine.

---

# simulation/utils/

Small helper functions.

Example:

```text
random.ts

probability.ts

clamp.ts
```

Utilities should remain generic.

---

# lib/

Third-party integrations.

```text
lib/

jwt.ts

bcrypt.ts

prisma.ts
```

Responsibilities:

- Create Prisma client
- Hash passwords
- Generate JWTs

---

# types/

Shared TypeScript types.

```text
types/

api.ts

simulation.ts

auth.ts
```

Avoid duplicating interfaces.

---

# generated/

Automatically generated code.

Example:

Prisma Client.

Never edit files in this folder.

---

# tests/

Project tests.

```text
tests/

unit/

integration/

simulation/
```

## Unit

Tests individual calculators.

Example:

- TyreWearCalculator
- LapTimeCalculator

---

## Integration

Tests API endpoints.

Example:

- Signup
- Login
- Create Season

---

## Simulation

Tests complete race scenarios.

Example:

- Full dry race
- Wet race
- Safety Car race
- Mechanical failure

---

# Dependency Rules

Allowed:

```text
Routes
    ↓
Controllers
    ↓
Services
    ↓
Repositories
    ↓
Database
```

Services may also call:

```text
Simulation Engine
```

Simulation Engine may call:

```text
Calculators

Generators

Strategies
```

---

# Forbidden Dependencies

Controllers must NEVER import Prisma.

Repositories must NEVER import Express.

Simulation Engine must NEVER import Express.

Simulation Engine must NEVER import Prisma.

Utilities must NEVER contain business logic.

Routes must NEVER call Prisma directly.

---

# Coding Standards

## One Class = One Responsibility

Good:

```text
TyreWearCalculator
```

Bad:

```text
RaceUtils.ts
```

---

## Small Files

Target:

100–250 lines per file.

If a file exceeds 300 lines,

consider splitting it.

---

## Pure Functions

Calculators should be deterministic.

Given the same input,

they should always return the same output.

---

## Naming Conventions

Classes

```text
PascalCase
```

Example

```text
RaceEngine
```

Methods

```text
camelCase
```

Example

```text
calculateLapTime()
```

Constants

```text
UPPER_SNAKE_CASE
```

Example

```text
MAX_TYRE_WEAR
```

---

# Architectural Goals

The architecture should allow:

- Replacing Express without changing the simulation.
- Replacing Prisma without changing business logic.
- Running the simulation from a CLI.
- Running the simulation inside unit tests.
- Moving the simulation to a desktop application.

Every layer should depend only on the layer beneath it.

---

# Final Architecture

```text
                HTTP Request
                      │
                      ▼
                 Express Routes
                      │
                      ▼
                 Controllers
                      │
                      ▼
                   Services
             ┌────────┴────────┐
             ▼                 ▼
      Repositories      Simulation Engine
             │                 │
             ▼                 ▼
         PostgreSQL      Calculators
                          Events
                          Strategies
                          State
```

---

# Design Goal

The RaceWall codebase should remain modular.

Each feature should be easy to locate.

Each file should have one clear purpose.

New developers should be able to understand the project structure within a few minutes, and future features should fit naturally into the existing architecture without requiring large refactors.
