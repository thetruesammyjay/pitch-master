# Pitch Master - Backend API Documentation

## Base URL
```
Development: http://localhost:5000/api
Production: https://api.pitchmaster.com/api
```

## Authentication
Most endpoints require authentication using JWT Bearer tokens.

**Authorization Header:**
```
Authorization: Bearer <jwt_token>
```

---

## Table of Contents
1. [Authentication Endpoints](#authentication-endpoints)
2. [User Endpoints](#user-endpoints)
3. [Player Endpoints](#player-endpoints)
4. [Team Endpoints](#team-endpoints)
5. [Comparison Endpoints](#comparison-endpoints)
6. [Error Responses](#error-responses)

---

## Authentication Endpoints

### Register User
Create a new user account.

**Endpoint:** `POST /api/auth/register`

**Access:** Public

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "SecurePass123!",
  "confirmPassword": "SecurePass123!"
}
```

**Success Response:** `201 Created`
```json
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "user": {
      "_id": "64abc123def456",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user",
      "createdAt": "2024-01-15T10:30:00.000Z"
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

**Error Response:** `400 Bad Request`
```json
{
  "success": false,
  "message": "User already exists"
}
```

---

### Login User
Authenticate user and receive JWT token.

**Endpoint:** `POST /api/auth/login`

**Access:** Public

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "SecurePass123!"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "user": {
      "_id": "64abc123def456",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user"
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

**Error Response:** `401 Unauthorized`
```json
{
  "success": false,
  "message": "Invalid email or password"
}
```

---

### Get Current User
Get authenticated user's profile information.

**Endpoint:** `GET /api/auth/me`

**Access:** Private (Requires Authentication)

**Headers:**
```
Authorization: Bearer <jwt_token>
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "_id": "64abc123def456",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user",
    "savedTeams": 5,
    "createdAt": "2024-01-15T10:30:00.000Z"
  }
}
```

---

### Logout User
Logout user (client-side token removal, optional endpoint).

**Endpoint:** `POST /api/auth/logout`

**Access:** Private

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

---

## User Endpoints

### Get User Profile
Get user profile details.

**Endpoint:** `GET /api/users/profile`

**Access:** Private

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "_id": "64abc123def456",
    "name": "John Doe",
    "email": "john@example.com",
    "bio": "Football enthusiast and tactical analyst",
    "favoriteTeam": "Manchester United",
    "savedTeamsCount": 5,
    "comparisonsCount": 12,
    "createdAt": "2024-01-15T10:30:00.000Z"
  }
}
```

---

### Update User Profile
Update user profile information.

**Endpoint:** `PUT /api/users/profile`

**Access:** Private

**Request Body:**
```json
{
  "name": "John Doe Updated",
  "bio": "Passionate about football analytics",
  "favoriteTeam": "Chelsea FC"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Profile updated successfully",
  "data": {
    "_id": "64abc123def456",
    "name": "John Doe Updated",
    "email": "john@example.com",
    "bio": "Passionate about football analytics",
    "favoriteTeam": "Chelsea FC"
  }
}
```

---

### Change Password
Change user password.

**Endpoint:** `PUT /api/users/change-password`

**Access:** Private

**Request Body:**
```json
{
  "currentPassword": "OldPass123!",
  "newPassword": "NewSecurePass456!",
  "confirmPassword": "NewSecurePass456!"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Password changed successfully"
}
```

---

## Player Endpoints

### Get All Players
Retrieve all players with pagination, filtering, and sorting.

**Endpoint:** `GET /api/players`

**Access:** Public

**Query Parameters:**
- `page` (number): Page number (default: 1)
- `limit` (number): Results per page (default: 20, max: 100)
- `position` (string): Filter by position (GK, DEF, MID, FWD)
- `nationality` (string): Filter by nationality
- `team` (string): Filter by club team
- `minRating` (number): Minimum overall rating (0-100)
- `maxRating` (number): Maximum overall rating (0-100)
- `search` (string): Search by player name
- `sort` (string): Sort field (name, rating, age, etc.)
- `order` (string): Sort order (asc, desc)

**Example Request:**
```
GET /api/players?page=1&limit=20&position=FWD&minRating=80&sort=rating&order=desc
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "count": 245,
  "totalPages": 13,
  "currentPage": 1,
  "data": [
    {
      "_id": "64player001",
      "name": "Erling Haaland",
      "position": "FWD",
      "nationality": "Norway",
      "team": "Manchester City",
      "age": 23,
      "overallRating": 91,
      "attributes": {
        "pace": 89,
        "shooting": 94,
        "passing": 65,
        "dribbling": 80,
        "defending": 45,
        "physical": 88
      },
      "image": "https://example.com/players/haaland.jpg",
      "preferredFoot": "left",
      "height": 194,
      "weight": 88
    }
  ]
}
```

---

### Get Player by ID
Get detailed information for a specific player.

**Endpoint:** `GET /api/players/:id`

**Access:** Public

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "_id": "64player001",
    "name": "Erling Haaland",
    "position": "FWD",
    "nationality": "Norway",
    "team": "Manchester City",
    "age": 23,
    "dateOfBirth": "2000-07-21",
    "overallRating": 91,
    "attributes": {
      "pace": 89,
      "shooting": 94,
      "passing": 65,
      "dribbling": 80,
      "defending": 45,
      "physical": 88
    },
    "detailedStats": {
      "attacking": {
        "finishing": 94,
        "shotPower": 91,
        "longShots": 85,
        "positioning": 92,
        "heading": 89
      },
      "skill": {
        "dribbling": 80,
        "ballControl": 81,
        "agility": 78,
        "balance": 77,
        "reactions": 88
      },
      "movement": {
        "acceleration": 89,
        "sprintSpeed": 89,
        "stamina": 85,
        "strength": 88,
        "jumping": 87
      },
      "mentality": {
        "aggression": 72,
        "composure": 88,
        "vision": 68,
        "positioning": 92
      }
    },
    "image": "https://example.com/players/haaland.jpg",
    "preferredFoot": "left",
    "height": 194,
    "weight": 88,
    "jerseyNumber": 9,
    "marketValue": "€180M"
  }
}
```

**Error Response:** `404 Not Found`
```json
{
  "success": false,
  "message": "Player not found"
}
```

---

### Search Players
Search for players by name or attributes.

**Endpoint:** `GET /api/players/search`

**Access:** Public

**Query Parameters:**
- `q` (string): Search query
- `limit` (number): Max results (default: 10)

**Example Request:**
```
GET /api/players/search?q=haaland&limit=5
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "count": 1,
  "data": [
    {
      "_id": "64player001",
      "name": "Erling Haaland",
      "position": "FWD",
      "team": "Manchester City",
      "overallRating": 91,
      "image": "https://example.com/players/haaland.jpg"
    }
  ]
}
```

---

### Create Player (Admin Only)
Add a new player to the database.

**Endpoint:** `POST /api/players`

**Access:** Private (Admin)

**Request Body:**
```json
{
  "name": "New Player",
  "position": "MID",
  "nationality": "Brazil",
  "team": "Barcelona",
  "age": 25,
  "dateOfBirth": "1999-03-15",
  "overallRating": 85,
  "attributes": {
    "pace": 82,
    "shooting": 78,
    "passing": 87,
    "dribbling": 86,
    "defending": 68,
    "physical": 75
  },
  "preferredFoot": "right",
  "height": 178,
  "weight": 72
}
```

**Success Response:** `201 Created`
```json
{
  "success": true,
  "message": "Player created successfully",
  "data": {
    "_id": "64player999",
    "name": "New Player",
    "position": "MID",
    "overallRating": 85
  }
}
```

---

### Update Player (Admin Only)
Update player information.

**Endpoint:** `PUT /api/players/:id`

**Access:** Private (Admin)

**Request Body:**
```json
{
  "overallRating": 86,
  "attributes": {
    "pace": 83,
    "shooting": 79,
    "passing": 88,
    "dribbling": 87,
    "defending": 68,
    "physical": 76
  }
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Player updated successfully",
  "data": {
    "_id": "64player999",
    "name": "New Player",
    "overallRating": 86
  }
}
```

---

### Delete Player (Admin Only)
Remove a player from the database.

**Endpoint:** `DELETE /api/players/:id`

**Access:** Private (Admin)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Player deleted successfully"
}
```

---

## Team Endpoints

### Get User's Teams
Retrieve all teams created by the authenticated user.

**Endpoint:** `GET /api/teams`

**Access:** Private

**Query Parameters:**
- `page` (number): Page number (default: 1)
- `limit` (number): Results per page (default: 10)
- `sort` (string): Sort by field (createdAt, name, rating)
- `order` (string): Sort order (asc, desc)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "count": 5,
  "data": [
    {
      "_id": "64team001",
      "name": "Dream Team XI",
      "formation": "4-3-3",
      "user": "64abc123def456",
      "players": [
        {
          "playerId": "64player001",
          "position": "ST",
          "playerInfo": {
            "name": "Erling Haaland",
            "overallRating": 91,
            "image": "url"
          }
        }
      ],
      "teamRating": 87,
      "createdAt": "2024-01-20T14:30:00.000Z",
      "updatedAt": "2024-01-20T14:30:00.000Z"
    }
  ]
}
```

---

### Get Team by ID
Get detailed information for a specific team.

**Endpoint:** `GET /api/teams/:id`

**Access:** Private (Own teams) / Public (if shared)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "_id": "64team001",
    "name": "Dream Team XI",
    "description": "My ultimate fantasy starting eleven",
    "formation": "4-3-3",
    "user": {
      "_id": "64abc123def456",
      "name": "John Doe"
    },
    "players": [
      {
        "playerId": "64player001",
        "position": "ST",
        "playerInfo": {
          "name": "Erling Haaland",
          "overallRating": 91,
          "position": "FWD",
          "nationality": "Norway",
          "team": "Manchester City",
          "image": "url",
          "attributes": {
            "pace": 89,
            "shooting": 94,
            "passing": 65,
            "dribbling": 80,
            "defending": 45,
            "physical": 88
          }
        }
      },
      {
        "playerId": "64player002",
        "position": "GK",
        "playerInfo": {
          "name": "Alisson Becker",
          "overallRating": 89
        }
      }
      // ... 11 players total
    ],
    "teamRating": 87,
    "chemistry": 85,
    "analysis": {
      "strengths": ["Attacking", "Pace", "Shooting"],
      "weaknesses": ["Passing", "Defending"],
      "averageAge": 26.5,
      "totalMarketValue": "€850M"
    },
    "isPublic": false,
    "createdAt": "2024-01-20T14:30:00.000Z",
    "updatedAt": "2024-01-20T14:30:00.000Z"
  }
}
```

---

### Create Team
Create a new team with custom formation and players.

**Endpoint:** `POST /api/teams`

**Access:** Private

**Request Body:**
```json
{
  "name": "My Ultimate XI",
  "description": "Best team ever assembled",
  "formation": "4-3-3",
  "players": [
    {
      "playerId": "64player001",
      "position": "ST"
    },
    {
      "playerId": "64player002",
      "position": "GK"
    }
    // ... up to 11 players
  ],
  "isPublic": false
}
```

**Validation Rules:**
- Team name: Required, 3-50 characters
- Formation: Must be valid (4-3-3, 4-4-2, 3-5-2, etc.)
- Players: Exactly 11 players required
- Positions: Must match formation structure

**Success Response:** `201 Created`
```json
{
  "success": true,
  "message": "Team created successfully",
  "data": {
    "_id": "64team002",
    "name": "My Ultimate XI",
    "formation": "4-3-3",
    "teamRating": 88,
    "createdAt": "2024-01-21T10:00:00.000Z"
  }
}
```

**Error Response:** `400 Bad Request`
```json
{
  "success": false,
  "message": "Team must have exactly 11 players"
}
```

---

### Update Team
Update team details, formation, or players.

**Endpoint:** `PUT /api/teams/:id`

**Access:** Private (Owner only)

**Request Body:**
```json
{
  "name": "Updated Team Name",
  "formation": "4-4-2",
  "players": [
    {
      "playerId": "64player003",
      "position": "ST"
    }
    // ... updated player list
  ]
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Team updated successfully",
  "data": {
    "_id": "64team001",
    "name": "Updated Team Name",
    "formation": "4-4-2",
    "teamRating": 86
  }
}
```

---

### Delete Team
Delete a team.

**Endpoint:** `DELETE /api/teams/:id`

**Access:** Private (Owner only)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Team deleted successfully"
}
```

---

### Get Team Analysis
Get detailed analysis of team strengths, weaknesses, and statistics.

**Endpoint:** `GET /api/teams/:id/analysis`

**Access:** Private (Owner) / Public (if shared)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "teamId": "64team001",
    "teamName": "Dream Team XI",
    "overallRating": 87,
    "chemistry": 85,
    "formation": "4-3-3",
    "attributeAverages": {
      "pace": 84,
      "shooting": 82,
      "passing": 81,
      "dribbling": 83,
      "defending": 76,
      "physical": 80
    },
    "positionAnalysis": {
      "attack": {
        "rating": 89,
        "players": 3,
        "avgAge": 24
      },
      "midfield": {
        "rating": 86,
        "players": 3,
        "avgAge": 26
      },
      "defense": {
        "rating": 85,
        "players": 4,
        "avgAge": 27
      },
      "goalkeeper": {
        "rating": 88,
        "players": 1,
        "age": 29
      }
    },
    "strengths": [
      {
        "attribute": "Shooting",
        "rating": 89,
        "description": "Exceptional attacking prowess"
      },
      {
        "attribute": "Pace",
        "rating": 87,
        "description": "Very fast team overall"
      }
    ],
    "weaknesses": [
      {
        "attribute": "Defending",
        "rating": 76,
        "description": "Defensive line could be stronger"
      }
    ],
    "teamStats": {
      "averageAge": 26.2,
      "totalMarketValue": "€950M",
      "mostValuablePlayers": [
        {
          "name": "Erling Haaland",
          "value": "€180M"
        }
      ],
      "nationalityDistribution": {
        "Norway": 1,
        "Brazil": 2,
        "France": 3
      }
    },
    "tacticalInsights": {
      "playStyle": "High-pressing, attacking football",
      "keyPlayers": ["Erling Haaland", "Kevin De Bruyne"],
      "recommendations": [
        "Consider adding a defensive midfielder for balance",
        "Strong attacking potential but needs defensive reinforcement"
      ]
    }
  }
}
```

---

### Duplicate Team
Create a copy of an existing team.

**Endpoint:** `POST /api/teams/:id/duplicate`

**Access:** Private (Owner only)

**Success Response:** `201 Created`
```json
{
  "success": true,
  "message": "Team duplicated successfully",
  "data": {
    "_id": "64team003",
    "name": "Dream Team XI (Copy)",
    "formation": "4-3-3"
  }
}
```

---

## Comparison Endpoints

### Compare Players
Compare multiple players side by side.

**Endpoint:** `POST /api/comparisons`

**Access:** Private

**Request Body:**
```json
{
  "playerIds": ["64player001", "64player002", "64player003"],
  "attributes": ["pace", "shooting", "passing", "dribbling", "defending", "physical"]
}
```

**Validation:**
- Minimum 2 players, maximum 4 players
- Player IDs must be valid

**Success Response:** `201 Created`
```json
{
  "success": true,
  "data": {
    "_id": "64comp001",
    "user": "64abc123def456",
    "comparisonDate": "2024-01-22T16:45:00.000Z",
    "players": [
      {
        "playerId": "64player001",
        "playerInfo": {
          "name": "Erling Haaland",
          "position": "FWD",
          "team": "Manchester City",
          "overallRating": 91,
          "attributes": {
            "pace": 89,
            "shooting": 94,
            "passing": 65,
            "dribbling": 80,
            "defending": 45,
            "physical": 88
          }
        }
      },
      {
        "playerId": "64player002",
        "playerInfo": {
          "name": "Kylian Mbappé",
          "position": "FWD",
          "team": "Paris Saint-Germain",
          "overallRating": 91,
          "attributes": {
            "pace": 97,
            "shooting": 89,
            "passing": 80,
            "dribbling": 92,
            "defending": 36,
            "physical": 77
          }
        }
      }
    ],
    "comparison": {
      "pace": {
        "highest": "Kylian Mbappé",
        "values": [89, 97]
      },
      "shooting": {
        "highest": "Erling Haaland",
        "values": [94, 89]
      },
      "passing": {
        "highest": "Kylian Mbappé",
        "values": [65, 80]
      },
      "dribbling": {
        "highest": "Kylian Mbappé",
        "values": [80, 92]
      },
      "defending": {
        "highest": "Erling Haaland",
        "values": [45, 36]
      },
      "physical": {
        "highest": "Erling Haaland",
        "values": [88, 77]
      }
    },
    "winner": {
      "overall": "Tie",
      "categories": {
        "Erling Haaland": ["shooting", "physical"],
        "Kylian Mbappé": ["pace", "passing", "dribbling"]
      }
    }
  }
}
```

---

### Get Comparison History
Get user's comparison history.

**Endpoint:** `GET /api/comparisons/history`

**Access:** Private

**Query Parameters:**
- `page` (number): Page number (default: 1)
- `limit` (number): Results per page (default: 10)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "count": 12,
  "data": [
    {
      "_id": "64comp001",
      "comparisonDate": "2024-01-22T16:45:00.000Z",
      "playerCount": 2,
      "players": [
        {
          "name": "Erling Haaland",
          "team": "Manchester City"
        },
        {
          "name": "Kylian Mbappé",
          "team": "Paris Saint-Germain"
        }
      ]
    }
  ]
}
```

---

### Get Comparison by ID
Get detailed comparison results.

**Endpoint:** `GET /api/comparisons/:id`

**Access:** Private (Owner only)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "_id": "64comp001",
    "comparisonDate": "2024-01-22T16:45:00.000Z",
    "players": [...],
    "comparison": {...},
    "winner": {...}
  }
}
```

---

### Delete Comparison
Delete a comparison from history.

**Endpoint:** `DELETE /api/comparisons/:id`

**Access:** Private (Owner only)

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Comparison deleted successfully"
}
```

---

## Error Responses

### Standard Error Format
All error responses follow this format:

```json
{
  "success": false,
  "message": "Error message description",
  "error": "ErrorType",
  "statusCode": 400
}
```

### Common HTTP Status Codes

**400 Bad Request**
- Invalid request data
- Validation errors
- Missing required fields

```json
{
  "success": false,
  "message": "Validation error",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    },
    {
      "field": "password",
      "message": "Password must be at least 8 characters"
    }
  ]
}
```

**401 Unauthorized**
- Missing or invalid authentication token
- Token expired

```json
{
  "success": false,
  "message": "Not authorized, token failed",
  "error": "Unauthorized"
}
```

**403 Forbidden**
- User doesn't have permission
- Accessing resource owned by another user

```json
{
  "success": false,
  "message": "Access denied. Admin privileges required.",
  "error": "Forbidden"
}
```

**404 Not Found**
- Resource doesn't exist
- Invalid ID

```json
{
  "success": false,
  "message": "Resource not found",
  "error": "NotFound"
}
```

**409 Conflict**
- Duplicate resource
- Conflicting state

```json
{
  "success": false,
  "message": "User already exists with this email",
  "error": "Conflict"
}
```

**500 Internal Server Error**
- Server errors
- Database errors

```json
{
  "success": false,
  "message": "Internal server error",
  "error": "ServerError"
}
```

---

## Rate Limiting

API requests are rate-limited to prevent abuse:

**Limits:**
- Authenticated users: 100 requests per 15 minutes
- Unauthenticated users: 20 requests per 15 minutes

**Rate Limit Headers:**
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1642857600
```

**Rate Limit Exceeded Response:** `429 Too Many Requests`
```json
{
  "success": false,
  "message": "Too many requests, please try again later",
  "retryAfter": 900
}
```

---

## Pagination

Endpoints that return lists support pagination:

**Query Parameters:**
- `page`: Page number (default: 1)
- `limit`: Items per page (default: 20, max: 100)

**Response Format:**
```json
{
  "success": true,
  "count": 245,
  "totalPages": 13,
  "currentPage": 1,
  "hasNextPage": true,
  "hasPrevPage": false,
  "data": [...]
}
```

---

## Sorting and Filtering

Most GET endpoints support sorting and filtering:

**Sort Parameters:**
- `sort`: Field to sort by
- `order`: `asc` or `desc`

**Example:**
```
GET /api/players?sort=rating&order=desc
```

**Filter Parameters:**
Vary by endpoint, see specific endpoint documentation.

---

## Data Validation

### Player Attributes Range
All player attributes must be between 0-100:
- pace: 0-100
- shooting: 0-100
- passing: 0-100
- dribbling: 0-100
- defending: 0-100
- physical: 0-100

### Valid Positions
- GK (Goalkeeper)
- DEF (Defender)
- MID (Midfielder)
- FWD (Forward)

### Valid Formations
- 4-3-3
- 4-4-2
- 4-2-3-1
- 3-5-2
- 3-4-3
- 5-3-2
- 4-1-4-1
- 4-5-1

---

## API Versioning

Current version: `v1`

All endpoints are prefixed with `/api/v1/` in production.

Future versions will be available at `/api/v2/`, etc.

---

## Contact & Support

For API support or questions:
- Email: sammyjayisthename@gmail.com
- GitHub Issues: github.com/thetruesammyjay/pitch-master/issues

---

**Last Updated:** January 2024

**API Version:** 1.0.0
