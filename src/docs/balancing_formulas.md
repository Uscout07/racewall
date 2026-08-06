# 09. Balancing Formulas

## Purpose

This document defines the numerical balancing values used by the RaceWall simulation engine.

These values are starting points for Version 1 and are expected to evolve through testing.

The primary goal is to create races that are:

- Competitive
- Strategic
- Replayable
- Believable

---

# Design Principles

The following principles guide every balancing decision.

- Skill should matter more than luck.
- Strategy should matter more than raw pace.
- Better teams should usually win.
- Underdog victories should be possible but rare.
- Every tyre compound should be useful.
- No single strategy should dominate every race.

---

# Driver Ratings

Every driver attribute ranges from:

```text
0 – 100
```

Average Formula One driver:

```text
80
```

Elite driver:

```text
94–99
```

Attribute impact:

| Attribute       | Primary Effect          |
| --------------- | ----------------------- |
| Pace            | Base lap time           |
| Consistency     | Mistake probability     |
| Wet Skill       | Wet weather performance |
| Aggression      | Overtake attempts       |
| Tyre Management | Tyre degradation        |

---

# Team Ratings

Every team attribute ranges from:

```text
0 – 100
```

Average constructor:

```text
80
```

Top constructor:

```text
95+
```

Attributes:

- Race Pace
- Qualifying Pace
- Straight Speed
- Cornering
- Reliability
- Pit Crew

---

# Track Influence

Track characteristics determine which car attributes matter.

Example weights:

| Attribute      | High-Speed Track | Technical Track |
| -------------- | ---------------: | --------------: |
| Straight Speed |              60% |             25% |
| Cornering      |              40% |             75% |

Examples:

Monza

```text
Straight Weight = 0.70
Corner Weight = 0.30
```

Hungary

```text
Straight Weight = 0.30
Corner Weight = 0.70
```

---

# Tyre Performance

## Base Grip

| Compound     |                        Grip |
| ------------ | --------------------------: |
| Soft         |                         100 |
| Medium       |                          96 |
| Hard         |                          92 |
| Intermediate |  88 (Dry) / 97 (Light Rain) |
| Wet          | 75 (Dry) / 100 (Heavy Rain) |

---

# Base Wear Per Lap

| Compound     | Wear |
| ------------ | ---: |
| Soft         | 3.5% |
| Medium       | 2.5% |
| Hard         | 1.8% |
| Intermediate | 3.2% |
| Wet          | 3.8% |

---

# Tyre Grip Loss

Grip decreases gradually.

| Wear    | Grip Modifier |
| ------- | ------------: |
| 0–30%   |          100% |
| 31–60%  |           98% |
| 61–80%  |           95% |
| 81–90%  |           90% |
| 91–100% |           80% |

Past 100% wear:

- High puncture probability
- Severe pace loss

---

# Push Levels

## Push

Effects:

```text
Lap Time     -0.35 s

Tyre Wear    +30%

Mistake Risk +25%
```

---

## Balanced

Effects:

```text
No modifier
```

---

## Conserve

Effects:

```text
Lap Time     +0.30 s

Tyre Wear    -20%

Mistake Risk -15%
```

---

# Weather Effects

## Sunny

```text
Grip Modifier = 100%
```

---

## Cloudy

```text
Grip Modifier = 99%
```

---

## Light Rain

Dry tyres:

```text
Grip = 80%
```

Intermediate tyres:

```text
Grip = 100%
```

Wet tyres:

```text
Grip = 92%
```

---

## Heavy Rain

Dry tyres:

```text
Grip = 55%
```

Intermediate tyres:

```text
Grip = 82%
```

Wet tyres:

```text
Grip = 100%
```

---

# Weather Changes

Every five laps:

```text
Change Probability = 15%
```

Rain rarely appears instantly.

Example progression:

```text
Sunny
↓
Cloudy
↓
Light Rain
↓
Heavy Rain
```

---

# Fuel Effect

Cars become lighter every lap.

Suggested modifier:

```text
-0.03 s/lap
```

Maximum improvement:

```text
≈ 1.8 seconds
```

---

# Driver Mistake Probability

Base:

```text
0.30%
```

Modified by:

- Consistency
- Weather
- Push Level

Possible outcomes:

| Result        | Probability |
| ------------- | ----------: |
| Small lock-up |        High |
| Off-track     |      Medium |
| Spin          |         Low |
| Retirement    |    Very Low |

---

# Mechanical Failure

Base probability:

```text
0.15%
```

Modified by:

- Reliability
- Aggression
- Race distance

Failures:

- Engine
- Gearbox
- Brakes
- Hydraulics

---

# Safety Car

Base probability:

```text
4%
```

Track modifiers:

| Track     | Modifier |
| --------- | -------: |
| Monaco    |      +4% |
| Singapore |      +3% |
| Spa       |      +2% |
| Monza     |      +1% |

Weather:

Heavy rain:

```text
×2
```

Duration:

```text
2–4 laps
```

---

# Virtual Safety Car

Base probability:

```text
3%
```

Duration:

```text
1–2 laps
```

---

# Pit Stops

Average pit lane loss:

```text
22–30 seconds
```

Pit crew rating affects service time only.

Example:

| Rating | Stationary Time |
| ------ | --------------: |
| 95     |           2.1 s |
| 90     |           2.4 s |
| 80     |           2.8 s |
| 70     |           3.2 s |

Track pit loss remains separate.

---

# Overtaking

An overtake is attempted when:

- Pace advantage exists
- Gap < 1 second

Base probability:

```text
45%
```

Modifiers:

- Aggression
- Tyre advantage
- Track overtaking difficulty
- Weather

Failed attempt:

```text
+0.2 to +0.8 seconds
```

---

# Randomness

Per-lap randomness:

```text
±0.10 seconds
```

Randomness should never exceed:

```text
±0.25 seconds
```

Large swings should come from race events, not random numbers.

---

# AI Strategy

Aggressive AI:

- Pushes more often
- Earlier pit stops
- Greater risk

Balanced AI:

- Follows optimal windows
- Adapts to weather

Conservative AI:

- Longer stints
- Lower mistake probability
- Fewer overtakes

---

# Championship Points

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

Fastest lap points are disabled in Version 1.

---

# Performance Targets

Typical race:

- 0–1 Safety Cars
- 0–2 retirements
- 1–3 pit strategies
- 2–5 meaningful overtakes
- 0–2 weather transitions

The objective is to produce races that feel dynamic without becoming chaotic.

---

# Balancing Philosophy

When adjusting values:

1. Change one parameter at a time.
2. Simulate at least 100 races.
3. Compare outcomes against expected results.
4. Measure diversity of winners and strategies.
5. Prioritize enjoyable gameplay over perfect realism.

---

# Version 1 Goal

The simulation should consistently produce races where:

- Fast teams remain favorites.
- Smart strategy can beat raw pace.
- Weather changes create meaningful decisions.
- Every race tells a different story.
- The player feels responsible for both victories and defeats.
