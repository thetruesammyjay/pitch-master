# Pitch Master 

A comprehensive football analysis and comparison platform built with the MERN stack that empowers users to create custom Starting XIs, analyze team strengths, and compare players with detailed statistics.

## 🎯 Features

- **Custom Starting XI Builder**: Create and customize your dream team with an interactive formation builder
- **Team Strength Analysis**: Analyze overall team performance based on selected players' attributes
- **Player Profiles**: View detailed player statistics, positions, and performance metrics
- **Player Comparisons**: Side-by-side comparison of multiple players across various attributes
- **Team Management**: Save, edit, and review different team setups
- **Formation Support**: Multiple tactical formations (4-3-3, 4-4-2, 3-5-2, etc.)
- **Responsive Design**: Seamless experience across desktop, tablet, and mobile devices

## 🚀 Tech Stack

### Frontend
- **React.js** - UI component library
- **Redux Toolkit** - State management
- **React Router** - Navigation and routing
- **Axios** - HTTP client
- **Tailwind CSS** - Styling framework
- **React DnD** - Drag and drop functionality

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web application framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling
- **JWT** - Authentication and authorization
- **Bcrypt** - Password hashing

## 📁 Project Structure

```
pitch-master/
├── client/                 # Frontend React application
│   ├── public/
│   ├── src/
│   │   ├── components/    # Reusable UI components
│   │   ├── pages/         # Page components
│   │   ├── redux/         # Redux store and slices
│   │   ├── services/      # API service functions
│   │   ├── utils/         # Helper functions
│   │   ├── assets/        # Images, icons, etc.
│   │   ├── App.js
│   │   └── index.js
│   └── package.json
│
├── server/                # Backend Node/Express application
│   ├── config/           # Configuration files
│   ├── controllers/      # Route controllers
│   ├── models/          # Mongoose models
│   ├── routes/          # API routes
│   ├── middleware/      # Custom middleware
│   ├── utils/           # Helper functions
│   ├── server.js
│   └── package.json
│
├── .gitignore
├── README.md
└── package.json          # Root package.json for scripts
```

## 🛠️ Installation

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or Atlas)
- npm or yarn

### Clone the repository
```bash
git clone https://github.com/thetruesammyjay/pitch-master.git
cd pitch-master
```

### Backend Setup
```bash
cd server
npm install

# Create .env file with the following variables:
# PORT=5000
# MONGODB_URI=your_mongodb_connection_string
# JWT_SECRET=your_jwt_secret_key
# NODE_ENV=development

npm run dev
```

### Frontend Setup
```bash
cd client
npm install

# Create .env file with:
# REACT_APP_API_URL=http://localhost:5000/api

npm start
```

### Run Both Concurrently (from root)
```bash
npm install
npm run dev
```

## 🔧 Environment Variables

### Server (.env)
```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/pitchmaster
JWT_SECRET=your_secure_jwt_secret
NODE_ENV=development
CLIENT_URL=http://localhost:3000
```

### Client (.env)
```
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_ENV=development
```

## 📊 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login
- `GET /api/auth/me` - Get current user

### Players
- `GET /api/players` - Get all players (with pagination and filters)
- `GET /api/players/:id` - Get player by ID
- `POST /api/players` - Create new player (Admin)
- `PUT /api/players/:id` - Update player (Admin)
- `DELETE /api/players/:id` - Delete player (Admin)
- `GET /api/players/search` - Search players

### Teams
- `GET /api/teams` - Get user's saved teams
- `GET /api/teams/:id` - Get team by ID
- `POST /api/teams` - Create new team
- `PUT /api/teams/:id` - Update team
- `DELETE /api/teams/:id` - Delete team
- `GET /api/teams/:id/analysis` - Get team strength analysis

### Comparisons
- `POST /api/comparisons` - Compare multiple players
- `GET /api/comparisons/history` - Get comparison history

## 🎨 Key Components

### Frontend Components
- **FormationBuilder**: Interactive drag-and-drop formation creator
- **PlayerCard**: Display player information and stats
- **PlayerComparison**: Side-by-side player comparison view
- **TeamAnalysis**: Visual representation of team strengths
- **StatRadar**: Radar chart for player attributes
- **Navbar**: Main navigation component
- **ProtectedRoute**: Route wrapper for authentication

### Backend Models
- **User**: User authentication and profile
- **Player**: Player data and statistics
- **Team**: Saved team configurations
- **Comparison**: Player comparison records

## 🔐 Authentication

The application uses JWT (JSON Web Tokens) for authentication:
1. User registers or logs in
2. Server generates JWT token
3. Token stored in localStorage/cookies
4. Token sent with subsequent requests via Authorization header
5. Protected routes verify token validity

## 📱 Mobile Responsiveness

Pitch Master is fully responsive with:
- Mobile-first design approach
- Touch-friendly drag and drop
- Optimized layouts for all screen sizes
- Progressive Web App (PWA) capabilities

## 🧪 Testing

```bash
# Run backend tests
cd server
npm test

# Run frontend tests
cd client
npm test

# Run all tests
npm test
```

## 📦 Deployment

### Backend (Railway/Render/Heroku)
1. Set environment variables
2. Push code to platform
3. Database automatically connects via MONGODB_URI

### Frontend (Vercel/Netlify)
1. Connect GitHub repository
2. Set build command: `npm run build`
3. Set environment variables
4. Deploy

## 🤝 Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

**Samuel Justin Ifiezibe (Sammy Jay)**
- GitHub: [@thetruesammyjay](https://github.com/thetruesammyjay)
- Email: sammyjayisthename@gmail.com

## 🙏 Acknowledgments

- Player data sourced from public football statistics APIs
- Formation tactics inspired by modern football analysis
- Community feedback and contributions

## 🐛 Known Issues

- None at the moment. Please report issues on GitHub.

## 🚧 Roadmap

- [ ] Real-time player statistics updates
- [ ] Advanced analytics and predictions
- [ ] Social features (share teams, challenges)
- [ ] Mobile app version
- [ ] Integration with live match data
- [ ] AI-powered team suggestions
- [ ] Multi-language support

## 📞 Support

For support, email sammyjayisthename@gmail.com or open an issue on GitHub.

---

Made with ⚽ and ❤️ by Felix
