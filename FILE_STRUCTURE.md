# Pitch Master - Complete File Structure

## Root Directory Structure

```
pitch-master/
├── client/                          # Frontend React application
├── server/                          # Backend Node/Express application
├── .gitignore                       # Git ignore file
├── .env.example                     # Environment variables example
├── README.md                        # Project documentation
├── package.json                     # Root package.json for concurrent scripts
└── LICENSE                          # MIT License file
```

---

## Client Directory (Frontend)

```
client/
├── public/
│   ├── index.html                   # Main HTML file
│   ├── favicon.ico                  # App icon
│   ├── manifest.json                # PWA manifest
│   ├── robots.txt                   # SEO robots file
│   └── images/                      # Static images
│       ├── logo.png
│       ├── field-bg.jpg
│       └── default-player.png
│
├── src/
│   ├── components/                  # Reusable UI components
│   │   ├── common/                  # Common components
│   │   │   ├── Button.jsx
│   │   │   ├── Input.jsx
│   │   │   ├── Modal.jsx
│   │   │   ├── Loader.jsx
│   │   │   ├── ErrorBoundary.jsx
│   │   │   └── Tooltip.jsx
│   │   │
│   │   ├── layout/                  # Layout components
│   │   │   ├── Navbar.jsx
│   │   │   ├── Footer.jsx
│   │   │   ├── Sidebar.jsx
│   │   │   └── Container.jsx
│   │   │
│   │   ├── player/                  # Player-related components
│   │   │   ├── PlayerCard.jsx
│   │   │   ├── PlayerProfile.jsx
│   │   │   ├── PlayerStats.jsx
│   │   │   ├── PlayerList.jsx
│   │   │   ├── PlayerSearch.jsx
│   │   │   └── PlayerFilter.jsx
│   │   │
│   │   ├── team/                    # Team-related components
│   │   │   ├── FormationBuilder.jsx
│   │   │   ├── FormationSelector.jsx
│   │   │   ├── TeamCard.jsx
│   │   │   ├── TeamList.jsx
│   │   │   ├── TeamAnalysis.jsx
│   │   │   ├── PositionSlot.jsx
│   │   │   └── TeamSummary.jsx
│   │   │
│   │   ├── comparison/              # Comparison components
│   │   │   ├── PlayerComparison.jsx
│   │   │   ├── ComparisonTable.jsx
│   │   │   ├── StatRadar.jsx
│   │   │   └── ComparisonHistory.jsx
│   │   │
│   │   └── auth/                    # Authentication components
│   │       ├── LoginForm.jsx
│   │       ├── RegisterForm.jsx
│   │       ├── ProtectedRoute.jsx
│   │       └── AuthGuard.jsx
│   │
│   ├── pages/                       # Page components
│   │   ├── Home.jsx                 # Landing page
│   │   ├── Dashboard.jsx            # User dashboard
│   │   ├── CreateTeam.jsx           # Team creation page
│   │   ├── MyTeams.jsx              # User's saved teams
│   │   ├── PlayerDatabase.jsx       # Browse all players
│   │   ├── PlayerDetail.jsx         # Single player details
│   │   ├── ComparePages.jsx         # Player comparison page
│   │   ├── TeamAnalytics.jsx        # Team analysis page
│   │   ├── Login.jsx                # Login page
│   │   ├── Register.jsx             # Registration page
│   │   ├── Profile.jsx              # User profile
│   │   └── NotFound.jsx             # 404 page
│   │
│   ├── redux/                       # Redux state management
│   │   ├── store.js                 # Redux store configuration
│   │   │
│   │   ├── slices/                  # Redux slices
│   │   │   ├── authSlice.js         # Authentication state
│   │   │   ├── playerSlice.js       # Players state
│   │   │   ├── teamSlice.js         # Teams state
│   │   │   ├── comparisonSlice.js   # Comparisons state
│   │   │   └── uiSlice.js           # UI state (modals, loaders)
│   │   │
│   │   └── middleware/              # Custom middleware
│   │       └── errorMiddleware.js
│   │
│   ├── services/                    # API service layer
│   │   ├── api.js                   # Base Axios instance
│   │   ├── authService.js           # Authentication API calls
│   │   ├── playerService.js         # Player API calls
│   │   ├── teamService.js           # Team API calls
│   │   └── comparisonService.js     # Comparison API calls
│   │
│   ├── utils/                       # Utility functions
│   │   ├── constants.js             # App constants
│   │   ├── formations.js            # Formation configurations
│   │   ├── validators.js            # Form validators
│   │   ├── helpers.js               # Helper functions
│   │   ├── calculations.js          # Team analysis calculations
│   │   └── formatters.js            # Data formatters
│   │
│   ├── hooks/                       # Custom React hooks
│   │   ├── useAuth.js               # Authentication hook
│   │   ├── usePlayers.js            # Players data hook
│   │   ├── useTeams.js              # Teams data hook
│   │   ├── useDebounce.js           # Debounce hook
│   │   └── useLocalStorage.js       # LocalStorage hook
│   │
│   ├── context/                     # React Context (if needed)
│   │   └── ThemeContext.js          # Theme context
│   │
│   ├── assets/                      # Static assets
│   │   ├── images/                  # Image files
│   │   ├── icons/                   # Icon files
│   │   └── styles/                  # Global styles
│   │       ├── index.css            # Main CSS
│   │       └── tailwind.css         # Tailwind imports
│   │
│   ├── App.js                       # Root App component
│   ├── index.js                     # Entry point
│   ├── App.test.js                  # App tests
│   └── setupTests.js                # Test configuration
│
├── .env                             # Environment variables (not in git)
├── .env.example                     # Environment variables example
├── .gitignore                       # Git ignore
├── package.json                     # Dependencies and scripts
├── tailwind.config.js               # Tailwind configuration
└── README.md                        # Frontend documentation
```

---

## Server Directory (Backend)

```
server/
├── config/                          # Configuration files
│   ├── db.js                        # MongoDB connection
│   ├── cloudinary.js                # Image upload config (optional)
│   └── constants.js                 # Server constants
│
├── controllers/                     # Route controllers
│   ├── authController.js            # Authentication logic
│   ├── playerController.js          # Player CRUD operations
│   ├── teamController.js            # Team CRUD operations
│   ├── comparisonController.js      # Comparison operations
│   └── userController.js            # User profile operations
│
├── models/                          # Mongoose schemas
│   ├── User.js                      # User model
│   ├── Player.js                    # Player model
│   ├── Team.js                      # Team model
│   └── Comparison.js                # Comparison model
│
├── routes/                          # API routes
│   ├── authRoutes.js                # Auth endpoints
│   ├── playerRoutes.js              # Player endpoints
│   ├── teamRoutes.js                # Team endpoints
│   ├── comparisonRoutes.js          # Comparison endpoints
│   └── userRoutes.js                # User endpoints
│
├── middleware/                      # Custom middleware
│   ├── authMiddleware.js            # JWT verification
│   ├── errorHandler.js              # Error handling
│   ├── validation.js                # Request validation
│   ├── adminMiddleware.js           # Admin authorization
│   └── upload.js                    # File upload handling
│
├── utils/                           # Utility functions
│   ├── generateToken.js             # JWT token generation
│   ├── validators.js                # Data validators
│   ├── calculations.js              # Team analysis calculations
│   ├── seeders.js                   # Database seeders
│   └── helpers.js                   # Helper functions
│
├── tests/                           # Test files
│   ├── auth.test.js                 # Auth tests
│   ├── player.test.js               # Player tests
│   ├── team.test.js                 # Team tests
│   └── setup.js                     # Test setup
│
├── data/                            # Seed data
│   ├── players.json                 # Sample players data
│   └── formations.json              # Formation templates
│
├── .env                             # Environment variables (not in git)
├── .env.example                     # Environment variables example
├── .gitignore                       # Git ignore
├── server.js                        # Entry point
├── package.json                     # Dependencies and scripts
└── README.md                        # Backend documentation
```

---

## Key Files Details

### Client Key Files

**src/App.js**
```javascript
// Main application component with routing
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import { Provider } from 'react-redux';
import store from './redux/store';
// Routes and components
```

**src/redux/store.js**
```javascript
// Redux store configuration
import { configureStore } from '@reduxjs/toolkit';
import authReducer from './slices/authSlice';
import playerReducer from './slices/playerSlice';
// More reducers
```

**src/services/api.js**
```javascript
// Base Axios configuration with interceptors
import axios from 'axios';
// Request/response interceptors for auth token
```

### Server Key Files

**server.js**
```javascript
// Express server setup
const express = require('express');
const cors = require('cors');
const connectDB = require('./config/db');
// Routes, middleware, error handling
```

**config/db.js**
```javascript
// MongoDB connection
const mongoose = require('mongoose');
// Connection with error handling
```

**models/Player.js**
```javascript
// Player schema definition
// Fields: name, position, stats, attributes, team, nationality, etc.
```

**models/Team.js**
```javascript
// Team schema definition
// Fields: name, formation, players, user, analysis, etc.
```

---

## Environment Variables

### Client (.env)
```
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_ENV=development
```

### Server (.env)
```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/pitchmaster
JWT_SECRET=your_secure_random_string
JWT_EXPIRE=30d
NODE_ENV=development
CLIENT_URL=http://localhost:3000
```

---

## Scripts (package.json)

### Root package.json
```json
{
  "scripts": {
    "client": "cd client && npm start",
    "server": "cd server && npm run dev",
    "dev": "concurrently \"npm run server\" \"npm run client\"",
    "install-all": "npm install && cd client && npm install && cd ../server && npm install"
  }
}
```

### Client package.json
```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
```

### Server package.json
```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest --watchAll",
    "seed": "node utils/seeders.js"
  }
}
```

---

## Dependencies

### Client Dependencies
- react
- react-dom
- react-router-dom
- @reduxjs/toolkit
- react-redux
- axios
- tailwindcss
- react-beautiful-dnd / react-dnd
- recharts (for charts)
- react-icons

### Server Dependencies
- express
- mongoose
- dotenv
- bcryptjs
- jsonwebtoken
- cors
- express-validator
- nodemon (dev)
- jest (dev)
- supertest (dev)

---

This structure follows MERN stack best practices with clear separation of concerns, scalability, and maintainability in mind.
