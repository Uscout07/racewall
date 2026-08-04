# 07. Simulation Algorithms

## Purpose

This document defines the algorithms that power the RaceWall simulation engine.

It focuses on **how races are simulated**, not how the code is written.

The simulation engine should be:

- Deterministic at its core
- Influenced by player strategy
- Enriched by controlled randomness
- Easy to rebalance

---

# Simulation Philosophy

Every race consists of two independent systems.

## 1. Base Simulation

Represents the expected race pace.

This is deterministic.

It is calculated using:

- Driver ability
- Team performance
- Track characteristics
- Weather
- Tyres
- Fuel load

---

## 2. Dynamic Events

Represents unexpected race situations.

Examples:

- Rain
- Safety Car
- Lock-up
- Driver mistake
- Mechanical failure

Events never decide the winner directly.

Instead, they create strategic opportunities.

---

# Complete Race Pipeline

Every lap follows the same sequence.

```text
Start Lap

↓

Update Weather

↓

Update Tyres

↓

Generate Events

↓

Apply Strategy

↓

Calculate Lap Time

↓

Attempt Overtakes

↓

Update Positions

↓

Save Race State

↓

Next Lap
```

---

# Step 1 — Weather Update

Weather is evaluated every five laps.

Possible transitions:

```text
Sunny

↓

Cloudy

↓

Light Rain

↓

Heavy Rain
```

Reverse transitions are also allowed.

Large jumps should be extremely rare.

Weather modifies:

- Grip
- Tyre performance
- Driver mistakes
- Pit strategy

---

# Step 2 — Tyre Update

Every lap:

```text
Wear += Base Wear
```

Base wear depends on:

- Compound
- Driver tyre management
- Push level
- Weather
- Track abrasiveness

Wear influences grip.

Grip decreases gradually.

Near the end of tyre life:

Performance drops rapidly.

---

# Tyre Model

Soft

- Highest grip
- Highest wear

Medium

- Balanced

Hard

- Lowest grip
- Lowest wear

Intermediate

- Best in light rain

Wet

- Best in heavy rain

Using the wrong tyre incurs significant pace penalties.

---

# Step 3 — Event Generation

Every lap calculates event probabilities.

Possible events:

- Driver mistake
- Lock-up
- Mechanical failure
- Rain starts
- Rain stops
- Yellow flag
- Safety Car
- Virtual Safety Car

Each event has:

- Base probability
- Track modifier
- Weather modifier
- Driver modifier

---

# Driver Mistake

Influenced by:

- Consistency
- Weather
- Push level

Possible outcomes:

- Small time loss
- Lock-up
- Off-track excursion
- Spin

Retirements should be extremely rare.

---

# Mechanical Failure

Influenced by:

- Reliability
- Aggression
- Race distance

Failures include:

- Engine
- Gearbox
- Brakes
- Hydraulics

Most failures result in retirement.

---

# Safety Car

Triggered by:

- Major crash
- Debris
- Multi-car incident

Effects:

- Compresses field
- Removes time gaps
- Reduces tyre wear
- Encourages pit stops

Safety Car duration:

Approximately 2–4 laps.

---

# Virtual Safety Car

Less impactful than a Safety Car.

Effects:

- Reduced speed
- Smaller field compression

Duration:

Approximately 1–2 laps.

---

# Step 4 — Strategy Application

Player decisions modify simulation parameters.

## Push

Effects

- Faster pace
- Increased tyre wear
- Higher mistake chance

---

## Balanced

Effects

- Average pace
- Average tyre wear

---

## Conserve

Effects

- Slower pace
- Lower tyre wear
- Reduced mistakes

---

## Pit

Effects

- Lose pit lane time
- New tyre compound
- Reset tyre wear

Pit stop duration depends on:

- Team pit crew
- Track pit loss

---

# Step 5 — Lap Time Calculation

Every driver calculates

```text
Lap Time =
Base Track Time
+ Driver Modifier
+ Team Modifier
+ Track Modifier
+ Tyre Modifier
+ Weather Modifier
+ Fuel Modifier
+ Strategy Modifier
+ Event Modifier
+ Small Randomness
```

Small randomness should remain small.

Skill should dominate.

---

# Driver Modifier

Influenced by

- Pace
- Consistency

Higher pace

↓

Lower lap time.

---

# Team Modifier

Influenced by

- Race Pace
- Straight Speed
- Cornering

Track determines which attributes matter more.

Example:

Monza

Straight Speed has higher influence.

Monaco

Cornering has higher influence.

---

# Track Modifier

Track characteristics modify:

- Car strengths
- Overtaking
- Tyre wear

Example:

Spa rewards

- Straight speed

Hungary rewards

- Cornering

---

# Weather Modifier

Dry tyres on wet track

↓

Major pace loss.

Wet tyres on dry track

↓

Major pace loss.

Correct tyre choice

↓

Normal pace.

---

# Fuel Modifier

Cars begin the race heavy.

As fuel burns:

- Lap times gradually improve.

Fuel effect decreases every lap.

---

# Strategy Modifier

Push

↓

Lower lap time

Higher wear

Conserve

↓

Higher lap time

Lower wear

---

# Event Modifier

Applied only when events occur.

Examples

Lock-up

↓

+0.5 to +2 seconds

Spin

↓

+3 to +8 seconds

Crash

↓

Retirement

---

# Step 6 — Overtake Calculation

Drivers may overtake when:

- Pace advantage exists
- Gap is sufficiently small
- Track allows overtaking

Overtake chance depends on

- Pace difference
- Aggression
- Track difficulty
- Tyre advantage
- DRS (future)

Failed overtakes may:

- Lose time
- Increase tyre wear

---

# Step 7 — Position Update

Drivers are sorted by

```text
Total Race Time
```

Current race order updates.

---

# Step 8 — Race Completion

Race ends when

Leader completes final lap.

Results become official.

Championship updates.

---

# Championship Calculation

After every race

Award points

Update

- Driver standings
- Constructor standings

Calculate

- Championship leader

---

# AI Behaviour

Every AI team has strategy tendencies.

Examples

Aggressive

- Short stints
- Soft tyres

Balanced

- Flexible strategy

Conservative

- Long stints
- Hard tyres

AI should react to

- Weather
- Safety Cars
- Tyre degradation

---

# Randomness Rules

Randomness should obey these principles.

Good randomness:

- Creates opportunities
- Creates tension
- Creates memorable stories

Bad randomness:

- Instantly decides races
- Punishes perfect strategy
- Feels unfair

Randomness should modify outcomes,

never replace skill.

---

# Balancing Principles

The fastest team should usually win.

Great strategy should occasionally defeat superior pace.

Underdog victories should feel memorable.

Every tyre compound should be viable.

Weather should completely change strategic thinking.

Every race should feel unique.

No two seasons should unfold identically.

---

# Future Algorithms

Future versions may introduce:

- DRS
- ERS
- Fuel saving
- Track evolution
- Rubber build-up
- Dirty air
- Blue flags
- Red flags
- Driver confidence
- Team orders
- Car upgrades

These systems should plug into the simulation engine without requiring major architectural changes.

---

# Final Design Principle

The simulation engine should answer one question every lap:

> **"Given the current race state and the player's decisions, what is the most believable outcome?"**

The objective is not perfect realism.

The objective is believable, strategic, and replayable racing.
