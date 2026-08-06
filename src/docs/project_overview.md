# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.

# 01. Project Overview

## Purpose

This document defines the vision, scope, and product goals for **RaceWall**.

RaceWall is a race strategy simulator inspired by Formula 1 management games. The player does **not** drive the car. Instead, they act as the race engineer and strategist, making decisions that influence race outcomes.

---

# Product Summary

RaceWall is an open-source motorsport strategy simulator where the player:

- Chooses a team
- Starts a season
- Makes qualifying and race decisions
- Responds to weather and race events
- Competes for championship points
- Compares actual performance against expected performance

The experience is designed to feel like a tactical race weekend rather than a driving game.

---

# Core Idea

The game is about **decision-making under uncertainty**.

The player does not know everything in advance.

They must react to:

- Tyre wear
- Changing weather
- Safety Cars
- Driver mistakes
- Mechanical failures
- Race pace fluctuations
- Opponent strategy

Good strategy should beat raw luck over time.

---

# What Makes RaceWall Different

Most racing games focus on driving.

Most management games focus on spreadsheets.

RaceWall sits between the two:

- More interactive than a spreadsheet simulator
- More strategic than a driving game
- More game-like than a standard dashboard app

The goal is to make the player feel like a real race strategist making high-stakes decisions lap by lap.

---

# Target User

The primary user is someone who enjoys:

- Motorsport strategy
- Formula 1
- Management games
- Simulation games
- Tactical decision-making
- Open-source projects

The project is also designed as a portfolio piece that demonstrates:

- Backend architecture
- Domain modeling
- Database design
- API design
- Simulation logic
- Clean code structure

---

# MVP Scope

The first version of RaceWall should support:

- User signup and login
- Team selection
- Season creation
- A full race weekend simulation
- Weather changes
- Tyre compounds
- Safety Cars
- Race strategy choices
- Race results
- Championship standings

This is enough to validate the core gameplay loop.

---

# Out of Scope for Version 1

The following features are intentionally excluded from the first release:

- Driver transfers
- Car upgrades
- Research and development
- Sponsorships
- Team finances
- Multiplayer
- Career mode
- DRS and ERS systems
- Fuel management
- Mod support
- Live commentary
- Real-world licensing or branding

These may be added later if the demo proves fun.

---

# Design Goals

RaceWall should be:

## Strategic

The player should feel that choices matter.

## Believable

Races should behave like real motorsport scenarios, even if simplified.

## Replayable

No two races should feel exactly the same.

## Modular

Each system should be independent and replaceable.

## Lightweight

The game should be small enough to run locally and easy to deploy as a demo.

## Expandable

Future systems should plug into the existing architecture without major rewrites.

---

# Product Experience

The player experience should follow this flow:

```text id="n7c6hz"
Create Account
      ↓
Choose Team
      ↓
Start Season
      ↓
Race Weekend
      ↓
Practice
      ↓
Qualifying
      ↓
Race Strategy
      ↓
Race Simulation
      ↓
Results
      ↓
Standings
```

Each step should be understandable without requiring a tutorial wall.

---

# Technical Direction

RaceWall is designed as a modular system with three major layers:

## Domain and Simulation

Contains the game rules and race logic.

## Backend API

Handles authentication, persistence, and data delivery.

## Frontend

Renders the dashboard, race screen, standings, and team screens.

The simulation engine must remain framework-independent so it can run in:

- Express
- CLI
- Browser
- Desktop app
- Tests

---

# Success Criteria

The project is successful if:

- The race simulation feels fun
- The player understands why they won or lost
- Weather and strategy matter
- Results feel fair
- The game can be played from start to finish
- The codebase remains clean and modular

---

# Long-Term Vision

If the first version works, RaceWall can evolve into:

- A full season management game
- A local-first desktop game
- A browser demo
- A mod-friendly motorsport sandbox
- A community leaderboard platform

The long-term aim is to build a small but believable strategy game with room to grow.

---

# Final Principle

RaceWall should never feel like a disguised todo app.

It should feel like a real game where the player is responsible for every major strategic outcome.
