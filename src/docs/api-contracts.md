# 03. API Contracts

This document defines the HTTP API for the RaceWall season simulator demo.

---

# 1. Authentication

---

## POST /auth/signup

### Description

Creates a new user account and returns authentication tokens.

### Authentication

**Not Required**

### Request Body

```json
{
  "email": "you@example.com",
  "password": "MySuperSecret123"
}
```

### Validation

#### email

- Required
- Must be a valid email address
- Maximum 255 characters
- Must be unique

#### password

- Required
- Minimum 8 characters
- Maximum 128 characters

### Success Response

**201 Created**

```json
{
  "user": {
    "id": "41db1265-8bc1-4ab3-992f-885799a4af1d",
    "email": "you@example.com"
  },
  "accessToken": "<jwt-access-token>",
  "refreshToken": "<jwt-refresh-token>",
  "expiresIn": 3600
}
```

### Error Responses

**400 Bad Request**

```json
{
  "message": "Validation failed",
  "errors": [
    {
      "field": "password",
      "message": "Password must be at least 8 characters long"
    }
  ]
}
```

**409 Conflict**

```json
{
  "message": "Email already exists"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Email addresses are unique.
- Passwords are hashed on the server before being stored.
- Authentication tokens are issued immediately after successful signup.

---

## POST /auth/login

### Description

Authenticates a user and returns authentication tokens.

### Authentication

**Not Required**

### Request Body

```json
{
  "email": "you@example.com",
  "password": "MySuperSecret123"
}
```

### Validation

#### email

- Required

#### password

- Required

### Success Response

**200 OK**

```json
{
  "user": {
    "id": "41db1265-8bc1-4ab3-992f-885799a4af1d",
    "email": "you@example.com"
  },
  "accessToken": "<jwt-access-token>",
  "refreshToken": "<jwt-refresh-token>",
  "expiresIn": 3600
}
```

### Error Responses

**400 Bad Request**

```json
{
  "message": "Validation failed"
}
```

**401 Unauthorized**

```json
{
  "message": "Invalid email or password"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Email and password are verified against stored credentials.
- A new access token and refresh token are issued after successful authentication.

---

## GET /auth/me

### Description

Returns information about the currently authenticated user.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "user": {
    "id": "41db1265-8bc1-4ab3-992f-885799a4af1d",
    "email": "you@example.com"
  }
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Returns the authenticated user's profile.
- The access token must be supplied in the `Authorization` header using the Bearer scheme.

---

## POST /auth/refresh

### Description

Generates a new access token using a valid refresh token.

### Authentication

**Not Required**

### Request Body

```json
{
  "refreshToken": "<jwt-refresh-token>"
}
```

### Validation

#### refreshToken

- Required
- Must be a valid refresh token

### Success Response

**200 OK**

```json
{
  "accessToken": "<new-jwt-access-token>",
  "expiresIn": 3600
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired refresh token"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Refresh tokens have a longer lifetime than access tokens.
- A valid refresh token is required to obtain a new access token.

---

## POST /auth/logout

### Description

Logs the current user out by invalidating the refresh token.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

```json
{
  "refreshToken": "<jwt-refresh-token>"
}
```

### Success Response

**200 OK**

```json
{
  "message": "Logged out successfully"
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- The supplied refresh token is revoked.
- The client should remove any stored authentication tokens after logout.

---

# 2. Teams

---

## GET /teams

### Description

Fetches the details of all available teams.

### Authentication

**Not Required**

### Headers

None

### Request Body

None

### Success Response

**200 OK**

```json
{
  "teams": [
    {
      "id": 1,
      "name": "The Papayas",
      "color": "#FF8000",
      "constructorRating": 90,
      "racePace": 90,
      "qualifyingPace": 92,
      "straightSpeed": 95,
      "cornering": 88,
      "reliability": 82,
      "pitCrew": 92
    }
  ]
}
```

### Error Responses

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Returns all available teams.
- Team statistics are read-only.
- Teams may be ordered by constructor rating.

---

## GET /teams/:id

### Description

Fetches detailed information about a single team.

### Authentication

**Not Required**

### Headers

None

### Request Body

None

### Success Response

**200 OK**

```json
{
  "team": {
    "id": 1,
    "name": "The Papayas",
    "color": "#FF8000",
    "budget": 300000000,
    "constructorRating": 90,
    "racePace": 90,
    "qualifyingPace": 92,
    "straightSpeed": 95,
    "cornering": 88,
    "reliability": 82,
    "pitCrew": 92,
    "drivers": [
      {
        "id": 11,
        "name": "Smooth Operator",
        "pace": 91,
        "wetSkill": 87,
        "consistency": 89,
        "aggression": 72
      }
    ]
  }
}
```

### Error Responses

**404 Not Found**

```json
{
  "message": "Team not found"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- This endpoint is intended for the team detail screen.
- It returns more data than `GET /teams`.

---

# 3. Tracks

---

## GET /tracks

### Description

Returns all available race tracks.

### Authentication

**Not Required**

### Headers

None

### Request Body

None

### Success Response

**200 OK**

```json
{
  "tracks": [
    {
      "id": 1,
      "name": "Spa",
      "laps": 44,
      "straightBias": 20,
      "cornerBias": 8,
      "rainProbability": 35
    }
  ]
}
```

### Error Responses

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Tracks are static reference data.
- The frontend uses this to show available race weekends.

---

## GET /tracks/:id

### Description

Returns detailed information about a single track.

### Authentication

**Not Required**

### Headers

None

### Request Body

None

### Success Response

**200 OK**

```json
{
  "track": {
    "id": 1,
    "name": "Spa",
    "laps": 44,
    "straightBias": 20,
    "cornerBias": 8,
    "rainProbability": 35,
    "description": "High-speed track with strong straight-line advantage.",
    "trackType": "High Speed"
  }
}
```

### Error Responses

**404 Not Found**

```json
{
  "message": "Track not found"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- The detailed view can include a description or tag fields later.

---

# 4. Seasons

---

## POST /seasons

### Description

Creates a new racing season for the authenticated user.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

```json
{
  "teamId": 1,
  "difficulty": "NORMAL"
}
```

### Validation

#### teamId

- Required
- Must reference a valid team

#### difficulty

- Required
- Must be one of the supported difficulty levels

### Success Response

**201 Created**

```json
{
  "season": {
    "id": 12,
    "name": "My First Season",
    "difficulty": "NORMAL",
    "completed": false,
    "currentRaceId": 1,
    "createdAt": "2026-07-30T16:20:00.000Z"
  },
  "team": {
    "id": 1,
    "name": "The Papayas"
  }
}
```

### Error Responses

**400 Bad Request**

```json
{
  "message": "Validation failed"
}
```

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Team not found"
}
```

**409 Conflict**

```json
{
  "message": "User already has an active season"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- A user can only have one active season at a time in the demo version.
- The selected team cannot be changed after season creation.

---

## GET /seasons

### Description

Returns all seasons belonging to the authenticated user.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "seasons": [
    {
      "id": 12,
      "name": "My First Season",
      "difficulty": "NORMAL",
      "completed": false,
      "createdAt": "2026-07-30T16:20:00.000Z"
    }
  ]
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Useful for showing a season picker or continue screen.

---

## GET /seasons/:id

### Description

Returns detailed information about a specific season.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "season": {
    "id": 12,
    "name": "My First Season",
    "difficulty": "NORMAL",
    "completed": false,
    "createdAt": "2026-07-30T16:20:00.000Z",
    "team": {
      "id": 1,
      "name": "The Papayas",
      "color": "#FF8000"
    },
    "nextRace": {
      "id": 31,
      "track": {
        "id": 4,
        "name": "Monza"
      }
    }
  }
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Season not found"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- This endpoint powers the season overview screen.
- It can return the next race preview to reduce extra API calls.

---

## DELETE /seasons/:id

### Description

Deletes a season permanently.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "message": "Season deleted successfully"
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Season not found"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- Deleting a season removes its races and standings in the demo version.
- If you do not want hard deletes later, this can become a soft delete.

---

# 5. Races

---

## POST /races/:id/start

### Description

Starts a race and returns the initial race state.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "race": {
    "id": 31,
    "status": "IN_PROGRESS",
    "currentLap": 1,
    "totalLaps": 44,
    "track": {
      "id": 4,
      "name": "Monza"
    },
    "weather": {
      "type": "CLOUDY",
      "temperature": 22
    },
    "grid": [
      {
        "driverId": 11,
        "name": "Smooth Operator",
        "team": "The Papayas",
        "position": 1
      }
    ]
  }
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Race not found"
}
```

**409 Conflict**

```json
{
  "message": "Race has already started"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

- This endpoint initializes the race simulation state.
- It should be idempotent or protected from duplicate starts.

---

## POST /races/:id/next-lap

### Description

Simulates the next lap and returns the updated race state.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

```json
{
  "strategy": "BALANCED"
}
```

### Validation

#### strategy

* Required
* Must be one of the supported strategy modes

### Success Response

**200 OK**

```json
{
  "race": {
    "id": 31,
    "currentLap": 2,
    "status": "IN_PROGRESS",
    "leaderboard": [
      {
        "driverId": 11,
        "name": "Smooth Operator",
        "position": 1,
        "gapToLeader": 0
      }
    ],
    "events": [
      {
        "lap": 2,
        "type": "PIT_STOP",
        "description": "The Papayas pit for Medium tyres."
      }
    ]
  }
}
```

### Error Responses

**400 Bad Request**

```json
{
  "message": "Validation failed"
}
```

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Race not found"
}
```

**409 Conflict**

```json
{
  "message": "Race is not in progress"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* This is the main gameplay endpoint.
* It advances the simulation by one lap.

---

## POST /races/:id/decision

### Description

Sends a strategic decision for the current race state.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

```json
{
  "decision": "PIT",
  "tyreCompound": "MEDIUM"
}
```

### Validation

#### decision

* Required
* Must be one of:

  * `PUSH`
  * `CONSERVE`
  * `PIT`
  * `BALANCED`

#### tyreCompound

* Required when `decision` is `PIT`
* Must be one of:

  * `SOFT`
  * `MEDIUM`
  * `HARD`

### Success Response

**200 OK**

```json
{
  "message": "Decision accepted",
  "race": {
    "id": 31,
    "nextDecisionAtLap": 18
  }
}
```

### Error Responses

**400 Bad Request**

```json
{
  "message": "Validation failed"
}
```

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Race not found"
}
```

**409 Conflict**

```json
{
  "message": "Decision cannot be applied at this time"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* This endpoint is useful if you want decisions to be separate from lap simulation.
* If you prefer a simpler MVP, you can merge this into `POST /races/:id/next-lap`.

---

## POST /races/:id/finish

### Description

Finishes the race and returns the final results.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "race": {
    "id": 31,
    "status": "FINISHED",
    "results": [
      {
        "driverId": 11,
        "name": "Smooth Operator",
        "team": "The Papayas",
        "finishPosition": 2,
        "points": 18,
        "bestLap": 83.421,
        "pitStops": 1
      }
    ],
    "strategyGrade": "A",
    "expectedFinishPosition": 4,
    "actualFinishPosition": 2,
    "overperformed": true
  }
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Race not found"
}
```

**409 Conflict**

```json
{
  "message": "Race is not in progress"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* This endpoint ends the simulation and persists the result.
* It should also update season standings.

---

## GET /races/:id

### Description

Returns the current state or final state of a race.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "race": {
    "id": 31,
    "status": "IN_PROGRESS",
    "currentLap": 12,
    "track": {
      "name": "Monza"
    },
    "weather": {
      "type": "LIGHT_RAIN",
      "temperature": 19
    }
  }
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Race not found"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* Useful for refreshing the live race screen.
* Can return either the current live state or the final stored result.

---

## GET /races/:id/events

### Description

Returns all significant events for a race.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "events": [
    {
      "id": 1,
      "raceId": 31,
      "lap": 2,
      "type": "PIT_STOP",
      "driverId": 11,
      "description": "The Papayas pit for Medium tyres.",
      "createdAt": "2026-07-30T16:40:00.000Z"
    }
  ]
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Race not found"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* This powers the event timeline on the UI.
* Events should be sorted by lap and creation time.

---

# 6. Standings

---

## GET /seasons/:id/standings

### Description

Returns the current driver and constructor standings for a season.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "seasonId": 12,
  "driverStandings": [
    {
      "driverId": 11,
      "name": "Smooth Operator",
      "team": "The Papayas",
      "points": 25,
      "wins": 1,
      "podiums": 2
    }
  ],
  "constructorStandings": [
    {
      "teamId": 1,
      "name": "The Papayas",
      "points": 35,
      "wins": 1,
      "podiums": 2
    }
  ]
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**404 Not Found**

```json
{
  "message": "Season not found"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* This endpoint powers the championship screen.
* It should be recalculated after each race finishes.

---

## GET /leaderboard

### Description

Returns global leaderboard data across all users or all completed seasons.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "leaderboard": [
    {
      "userId": "41db1265-8bc1-4ab3-992f-885799a4af1d",
      "username": "you@example.com",
      "bestSeasonPoints": 184,
      "bestFinish": 1
    }
  ]
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* This is optional for the demo.
* You can also make this public later if you want a shared community leaderboard.

---

# 7. Dashboard

---

## GET /dashboard

### Description

Returns the data needed for the main dashboard in one request.

### Authentication

**Required**

### Headers

```http
Authorization: Bearer <access-token>
```

### Request Body

None

### Success Response

**200 OK**

```json
{
  "activeSeason": {
    "id": 12,
    "name": "My First Season",
    "difficulty": "NORMAL",
    "completed": false
  },
  "nextRace": {
    "id": 31,
    "track": {
      "name": "Monza"
    }
  },
  "lastRace": {
    "id": 30,
    "finishPosition": 2,
    "strategyGrade": "A"
  },
  "driverStandings": [],
  "constructorStandings": []
}
```

### Error Responses

**401 Unauthorized**

```json
{
  "message": "Invalid or expired access token"
}
```

**500 Internal Server Error**

```json
{
  "message": "Internal server error"
}
```

### Notes

* This endpoint reduces frontend request count.
* It is ideal for loading the home screen quickly.

---

# 8. Standard Error Shape

All validation errors should follow this structure:

```json
{
  "message": "Validation failed",
  "errors": [
    {
      "field": "password",
      "message": "Password must be at least 8 characters long"
    }
  ]
}
```

# 9. Common Conventions

* Use `Authorization: Bearer <token>` for protected endpoints.
* Return numbers as numbers, not strings.
* Return dates as ISO 8601 strings.
* Use `200 OK`, `201 Created`, `400 Bad Request`, `401 Unauthorized`, `404 Not Found`, `409 Conflict`, and `500 Internal Server Error` consistently.
* Keep list endpoints lightweight.
* Keep detail endpoints richer.
* Keep simulation logic out of the API contract.

