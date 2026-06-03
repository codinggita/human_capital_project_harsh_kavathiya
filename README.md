# 🍽️ Human Capital — Food Price Statistics (Full Stack)

<div align="center">

[![React](https://img.shields.io/badge/React-18%2B-61DAFB?style=flat-square&logo=react)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-5.x-646CFF?style=flat-square&logo=vite)](https://vitejs.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-brightgreen?style=flat-square&logo=node.js)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express-4.x-lightgrey?style=flat-square&logo=express)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-NoSQL-13aa52?style=flat-square&logo=mongodb)](https://www.mongodb.com/)
[![JWT](https://img.shields.io/badge/JWT-Authentication-orange?style=flat-square)](https://jwt.io/)
[![MVC](https://img.shields.io/badge/Architecture-MVC-blue?style=flat-square)](.)
[![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)](.)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)

**A Full Stack Application for FAO Food Price Statistics**
**React.js · Vite · Node.js · Express.js · MongoDB · JWT Auth · MVC Architecture**

[🚀 Quick Start](#-quick-start) · [📁 Folder Structure](#-folder-structure) · [🎨 Frontend](#-frontend) · [📊 API Docs](#-api-documentation) · [🔐 Auth Flow](#-authentication-flow) · [🌐 Deployment](#-deployment)

</div>

---

## 📊 Project Overview

| Metric | Value |
|--------|-------|
| 🎨 Frontend | **React.js 18+ (Vite)** |
| 🔌 Total API Endpoints | **100+** |
| 🗄️ MongoDB Collections | **4** |
| 🔐 Auth Type | **JWT + Refresh Token** |
| ⚡ Rate Limit | **100 req / 15 min** |
| 🏗️ Architecture | **MVC + Service Layer** |
| 📦 Core Dependencies | **11 (backend) + 8 (frontend)** |
| 🌍 Dataset | **FAO Food Price Index** |
| 🔄 API Version | **v1 (/api/v1)** |

---

## 🚀 Quick Start

### Prerequisites

```bash
node -v       # v18 or higher
npm -v        # v9 or higher
mongod        # MongoDB running locally OR Atlas URI in .env
```

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/human-capital.git
cd human-capital
```

### 2. Setup Backend

```bash
cd backend
npm install
cp .env.example .env        # Fill in your environment variables
node seeds/seedData.js      # Seed the FAO dataset into MongoDB
npm run dev                 # Starts on http://localhost:5000
```

### 3. Setup Frontend

```bash
cd frontend
npm install
cp .env.example .env        # Set VITE_API_BASE_URL
npm run dev                 # Starts on http://localhost:5173
```

### 4. Open the App

```
Frontend  →  http://localhost:5173
Backend   →  http://localhost:5000
API Base  →  http://localhost:5000/api/v1
```

---

## 📁 Folder Structure

```
human-capital/
│
├── 📂 backend/                          ← Node.js + Express API
│   ├── 📂 config/
│   │   └── db.js                        ← MongoDB connection
│   │
│   ├── 📂 models/                       ← Mongoose schemas
│   │   ├── Price.js                     ← Price schema (core)
│   │   ├── Country.js                   ← Country schema
│   │   ├── Indicator.js                 ← Indicator schema
│   │   └── User.js                      ← User/Auth schema
│   │
│   ├── 📂 controllers/                  ← Request/Response only
│   │   ├── priceController.js
│   │   ├── countryController.js
│   │   ├── indicatorController.js
│   │   ├── statsController.js
│   │   ├── authController.js
│   │   └── searchController.js
│   │
│   ├── 📂 services/                     ← Business logic only
│   │   ├── priceService.js
│   │   ├── statsService.js
│   │   └── authService.js
│   │
│   ├── 📂 routes/                       ← Route definitions
│   │   ├── priceRoutes.js               ← /api/v1/prices
│   │   ├── countryRoutes.js             ← /api/v1/countries
│   │   ├── indicatorRoutes.js           ← /api/v1/indicators
│   │   ├── statsRoutes.js               ← /api/v1/stats
│   │   ├── authRoutes.js                ← /api/v1/auth
│   │   ├── searchRoutes.js              ← /api/v1/search
│   │   ├── jwtRoutes.js                 ← /api/v1/jwt
│   │   ├── adminRoutes.js               ← /api/v1/admin
│   │   └── protectedRoutes.js           ← /api/v1/protected
│   │
│   ├── 📂 middlewares/
│   │   ├── authMiddleware.js            ← JWT verification
│   │   ├── adminMiddleware.js           ← Admin role check
│   │   ├── errorMiddleware.js           ← Global error handler
│   │   ├── rateLimitMiddleware.js       ← Rate limiting
│   │   ├── loggerMiddleware.js          ← Request logging
│   │   └── validateMiddleware.js        ← Input validation
│   │
│   ├── 📂 utils/
│   │   ├── pagination.js                ← Reusable pagination
│   │   ├── filterBuilder.js             ← Dynamic filter builder
│   │   ├── asyncHandler.js              ← Async error wrapper
│   │   └── apiResponse.js               ← Standardized responses
│   │
│   ├── 📂 seeds/
│   │   └── seedData.js                  ← Import dataset to MongoDB
│   │
│   ├── 📄 app.js                        ← Express app setup
│   ├── 📄 server.js                     ← Entry point
│   ├── 📄 dataset.json                  ← FAO dataset
│   ├── 📄 .env
│   ├── 📄 .env.example
│   └── 📄 package.json
│
├── 📂 frontend/                         ← React.js + Vite App
│   ├── 📂 public/
│   │   └── favicon.ico
│   │
│   ├── 📂 src/
│   │   ├── 📂 api/                      ← Axios API layer
│   │   │   ├── axiosInstance.js         ← Base Axios config + interceptors
│   │   │   ├── authApi.js               ← Auth API calls
│   │   │   ├── priceApi.js              ← Price API calls
│   │   │   ├── statsApi.js              ← Stats API calls
│   │   │   └── searchApi.js             ← Search API calls
│   │   │
│   │   ├── 📂 components/               ← Reusable UI components
│   │   │   ├── 📂 layout/
│   │   │   │   ├── Navbar.jsx
│   │   │   │   ├── Sidebar.jsx
│   │   │   │   └── Footer.jsx
│   │   │   ├── 📂 common/
│   │   │   │   ├── Loader.jsx
│   │   │   │   ├── ErrorMessage.jsx
│   │   │   │   ├── Pagination.jsx
│   │   │   │   └── ProtectedRoute.jsx
│   │   │   └── 📂 charts/
│   │   │       ├── LineChart.jsx
│   │   │       ├── BarChart.jsx
│   │   │       └── PieChart.jsx
│   │   │
│   │   ├── 📂 pages/                    ← Page-level components
│   │   │   ├── Home.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Prices.jsx
│   │   │   ├── PriceDetail.jsx
│   │   │   ├── Countries.jsx
│   │   │   ├── Statistics.jsx
│   │   │   ├── Search.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   └── AdminPanel.jsx
│   │   │
│   │   ├── 📂 context/                  ← React Context (global state)
│   │   │   └── AuthContext.jsx          ← Auth state + token management
│   │   │
│   │   ├── 📂 hooks/                    ← Custom React hooks
│   │   │   ├── useAuth.js               ← Auth hook
│   │   │   ├── usePrices.js             ← Price data fetching
│   │   │   └── useStats.js              ← Stats data fetching
│   │   │
│   │   ├── 📂 utils/
│   │   │   ├── tokenStorage.js          ← localStorage token helpers
│   │   │   └── formatters.js            ← Date/number formatters
│   │   │
│   │   ├── App.jsx                      ← Root component + routes
│   │   ├── main.jsx                     ← Vite entry point
│   │   └── index.css
│   │
│   ├── 📄 index.html
│   ├── 📄 vite.config.js
│   ├── 📄 .env
│   ├── 📄 .env.example
│   └── 📄 package.json
│
└── 📄 README.md                         ← This file
```

---

## 🔧 Environment Variables

### Backend — `backend/.env`

```bash
# ── Server ──────────────────────────────────────
PORT=5000
NODE_ENV=development

# ── Database ─────────────────────────────────────
MONGO_URI=mongodb://localhost:27017/human_capital
# OR Atlas:
# MONGO_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net/human_capital

# ── JWT ──────────────────────────────────────────
JWT_SECRET=human_capital_jwt_super_secret_key_2026
JWT_EXPIRES_IN=7d
JWT_REFRESH_SECRET=human_capital_refresh_secret_2026
JWT_REFRESH_EXPIRES_IN=30d

# ── Security ─────────────────────────────────────
BCRYPT_SALT_ROUNDS=10

# ── Rate Limiting ────────────────────────────────
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX=100
AUTH_RATE_LIMIT_MAX=10
```

### Frontend — `frontend/.env`

```bash
# ── API ──────────────────────────────────────────
VITE_API_BASE_URL=http://localhost:5000/api/v1

# ── App ──────────────────────────────────────────
VITE_APP_NAME=Human Capital
VITE_APP_VERSION=1.0.0
```

---

## 🎨 Frontend

### Tech Stack

| Tool | Purpose |
|------|---------|
| **React 18** | UI library |
| **Vite** | Build tool + dev server |
| **React Router v6** | Client-side routing |
| **Axios** | HTTP client with interceptors |
| **React Context** | Global auth state |
| **Recharts / Chart.js** | Data visualization |
| **Tailwind CSS** | Utility-first styling |

### Available Scripts

```bash
npm run dev        # Start dev server (http://localhost:5173)
npm run build      # Production build → dist/
npm run preview    # Preview production build locally
npm run lint       # ESLint check
```

### Pages & Routes

| Route | Page | Auth Required |
|-------|------|--------------|
| `/` | Home — Landing page | ❌ |
| `/dashboard` | Dashboard with charts | ✅ |
| `/prices` | Browse all price records | ❌ |
| `/prices/:id` | Single price detail | ❌ |
| `/countries` | Countries list | ❌ |
| `/statistics` | Aggregated stats & graphs | ❌ |
| `/search` | Full text search | ❌ |
| `/login` | Login form | ❌ |
| `/register` | Registration form | ❌ |
| `/admin` | Admin panel | ✅ Admin only |

### Axios Instance & Interceptors

```javascript
// src/api/axiosInstance.js
import axios from 'axios';

const api = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL,
  headers: { 'Content-Type': 'application/json' },
});

// Attach JWT token to every request
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('accessToken');
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

// Auto refresh token on 401
api.interceptors.response.use(
  (res) => res,
  async (error) => {
    if (error.response?.status === 401) {
      // Attempt token refresh and retry
    }
    return Promise.reject(error);
  }
);

export default api;
```

### Auth Context

```javascript
// src/context/AuthContext.jsx
const AuthContext = createContext();

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [token, setToken] = useState(localStorage.getItem('accessToken'));

  const login = (userData, accessToken, refreshToken) => {
    setUser(userData);
    setToken(accessToken);
    localStorage.setItem('accessToken', accessToken);
    localStorage.setItem('refreshToken', refreshToken);
  };

  const logout = () => {
    setUser(null);
    setToken(null);
    localStorage.clear();
  };

  return (
    <AuthContext.Provider value={{ user, token, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};
```

### Protected Route Component

```jsx
// src/components/common/ProtectedRoute.jsx
import { Navigate } from 'react-router-dom';
import { useAuth } from '../hooks/useAuth';

const ProtectedRoute = ({ children, adminOnly = false }) => {
  const { user, token } = useAuth();
  if (!token) return <Navigate to="/login" />;
  if (adminOnly && user?.role !== 'admin') return <Navigate to="/" />;
  return children;
};
```

### App Router Setup

```jsx
// src/App.jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <AuthProvider>
      <BrowserRouter>
        <Navbar />
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/prices" element={<Prices />} />
          <Route path="/prices/:id" element={<PriceDetail />} />
          <Route path="/countries" element={<Countries />} />
          <Route path="/statistics" element={<Statistics />} />
          <Route path="/search" element={<Search />} />
          <Route path="/login" element={<Login />} />
          <Route path="/register" element={<Register />} />
          <Route path="/dashboard" element={
            <ProtectedRoute><Dashboard /></ProtectedRoute>
          } />
          <Route path="/admin" element={
            <ProtectedRoute adminOnly><AdminPanel /></ProtectedRoute>
          } />
        </Routes>
      </BrowserRouter>
    </AuthProvider>
  );
}
```

---

## 🗄️ Backend

### Tech Stack

| Tool | Purpose |
|------|---------|
| **Node.js 18+** | JavaScript runtime |
| **Express.js 4.x** | Web framework |
| **MongoDB** | NoSQL database |
| **Mongoose** | MongoDB ODM |
| **jsonwebtoken** | JWT auth |
| **bcryptjs** | Password hashing |
| **express-validator** | Input validation |
| **express-rate-limit** | Rate limiting |
| **cors** | Cross-origin support |
| **morgan** | HTTP logging |
| **dotenv** | Environment config |

### Available Scripts

```bash
npm run dev       # Start with nodemon (auto-reload)
npm start         # Start production server
node seeds/seedData.js   # Seed FAO dataset into MongoDB
```

### Data Flow

```
dataset.json (FAO)
     ↓
seeds/seedData.js
     ↓
MongoDB → prices collection
     ↓
Price Model (Mongoose)
     ↓
Price Service (Business Logic)
     ↓
Price Controller (Request Handler)
     ↓
Price Routes → /api/v1/prices
     ↓
Axios (Frontend) → React UI
```

---

## 📐 Schema Design

### Price Schema (Main Collection)

```javascript
{
  countryCode: { type: String, required: true, uppercase: true },
  indicator:   { type: String, required: true },
  year:        { type: Number, required: true },
  month:       { type: Number, required: true, min: 1, max: 12 },
  value:       { type: Number, required: true },
  freq:        { type: String, default: 'M', enum: ['M', 'A'] },
  isDeleted:   { type: Boolean, default: false },
  timestamps:  true
}
```

### User Schema

```javascript
{
  name:      { type: String, required: true },
  email:     { type: String, required: true, unique: true, lowercase: true },
  password:  { type: String, required: true },   // bcrypt hashed
  role:      { type: String, enum: ['user', 'admin'], default: 'user' },
  otp:       { code: String, expiresAt: Date },
  timestamps: true
}
```

---

## 📊 API Documentation

**Base URL:** `http://localhost:5000/api/v1`

**Standard Response Format:**
```json
{
  "success": true,
  "message": "Records fetched successfully",
  "data": [...],
  "meta": {
    "total": 1000,
    "page": 1,
    "limit": 10,
    "totalPages": 100
  }
}
```

### 🏠 Base Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Welcome + all routes |
| `GET` | `/health` | Server health status |
| `GET` | `/version` | API version info |
| `GET` | `/server-status` | Memory & uptime |
| `GET` | `/metrics` | CPU, PID, performance |
| `GET` | `/api/v1` | All v1 endpoints |

### 💰 Price Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/prices` | All prices (filter/sort/paginate) |
| `GET` | `/prices/:id` | Single price |
| `POST` | `/prices` | Create price |
| `PUT` | `/prices/:id` | Full replace |
| `PATCH` | `/prices/:id` | Partial update |
| `DELETE` | `/prices/:id` | Delete |
| `GET` | `/prices/country/:code` | By country |
| `GET` | `/prices/year/:year` | By year |
| `GET` | `/prices/range/:start/:end` | Year range |
| `GET` | `/prices/country/:code/year/:year` | Country + year |
| `GET` | `/prices/country/:code/latest` | Latest by country |
| `GET` | `/prices/year/:year/highest` | Highest in year |
| `GET` | `/prices/year/:year/lowest` | Lowest in year |
| `GET` | `/prices/trending` | Trending prices |
| `GET` | `/prices/random` | Random sample |

### Query Parameters

| Parameter | Type | Example | Description |
|-----------|------|---------|-------------|
| `country` | String | `?country=IND` | Filter by country |
| `year` | Number | `?year=2020` | Filter by year |
| `month` | Number | `?month=5` | Filter by month |
| `indicator` | String | `?indicator=FAO_CP_23012` | Filter by indicator |
| `minValue` | Number | `?minValue=50` | Min value |
| `maxValue` | Number | `?maxValue=200` | Max value |
| `sort` | String | `?sort=-value` | Sort (- = descending) |
| `page` | Number | `?page=2` | Page number |
| `limit` | Number | `?limit=20` | Records per page |
| `search` | String | `?search=consumer` | Text search |

### 📈 Statistics Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/stats/prices` | Overall price stats |
| `GET` | `/stats/highest-value` | Highest price ever |
| `GET` | `/stats/lowest-value` | Lowest price ever |
| `GET` | `/stats/monthly-average` | Monthly averages |
| `GET` | `/stats/yearly-average` | Yearly averages |
| `GET` | `/stats/top-countries` | Top 10 countries |
| `GET` | `/stats/top-indicators` | Most used indicators |
| `GET` | `/stats/value-distribution` | Value distribution |
| `GET` | `/stats/trending` | Trending stats |
| `GET` | `/stats/country/:code` | Country analysis |
| `GET` | `/stats/year/:year` | Year analysis |

### 🔎 Search Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/search/country?name=India` | By country name |
| `GET` | `/search/indicator?text=Consumer` | By indicator text |
| `GET` | `/search/value?value=68` | By value proximity |
| `GET` | `/search/prices?q=general` | Full text search |

### 🔐 Authentication Routes

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `POST` | `/auth/register` | Create account | ❌ |
| `POST` | `/auth/login` | Get JWT tokens | ❌ |
| `POST` | `/auth/logout` | Logout | ✅ |
| `POST` | `/auth/refresh-token` | New access token | ❌ |
| `GET` | `/auth/me` | Current user | ✅ |
| `POST` | `/auth/change-password` | Update password | ✅ |
| `POST` | `/auth/forgot-password` | Request reset | ❌ |
| `POST` | `/auth/reset-password` | Apply reset | ❌ |
| `POST` | `/auth/send-otp` | Send OTP | ❌ |
| `POST` | `/auth/verify-otp` | Verify OTP | ❌ |

### 👑 Admin Routes

> Requires `Authorization: Bearer <token>` with `role: admin`

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/admin/prices` | View all prices |
| `POST` | `/admin/prices` | Create price |
| `PATCH` | `/admin/prices/:id` | Update price |
| `DELETE` | `/admin/prices/:id` | Delete price |
| `GET` | `/admin/dashboard` | Dashboard stats |
| `GET` | `/admin/stats` | Full statistics |

---

## 🔐 Authentication Flow

```
┌────────────────────────────────────────────────────────────────────┐
│                     FULL STACK AUTH FLOW                           │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  1. REGISTER (Frontend Form → API)                                 │
│     POST /auth/register { name, email, password }                  │
│     → Password hashed with bcrypt (10 rounds)                     │
│     → User stored in MongoDB                                       │
│     → Redirect to Login                                            │
│                                                                    │
│  2. LOGIN (Frontend Form → API → Context)                          │
│     POST /auth/login { email, password }                           │
│     → JWT Access Token (7d) + Refresh Token (30d)                 │
│     → Tokens stored in localStorage                                │
│     → AuthContext updated with user object                         │
│     → Redirect to Dashboard                                        │
│                                                                    │
│  3. PROTECTED REQUEST (Axios Interceptor → API)                    │
│     Axios adds: Authorization: Bearer <accessToken>               │
│     → authMiddleware verifies JWT                                  │
│     → req.user attached → controller runs                          │
│                                                                    │
│  4. TOKEN REFRESH (Axios Response Interceptor)                     │
│     On 401 → POST /auth/refresh-token                             │
│     → New access token issued + stored                             │
│     → Original request retried automatically                       │
│                                                                    │
│  5. LOGOUT                                                         │
│     POST /auth/logout → localStorage cleared                       │
│     → AuthContext reset → Redirect to Login                        │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

## 🧱 Middleware System

```
Incoming Request
       ↓
┌──────────────────────────────────────────────────┐
│   GLOBAL MIDDLEWARES                             │
│   ① cors()              → Allow React origin     │
│   ② express.json()      → Parse JSON body        │
│   ③ morgan('dev')       → Log requests           │
│   ④ rateLimitMiddleware → Max 100 req/15 min      │
└──────────────────────────────────────────────────┘
       ↓
┌──────────────────────────────────────────────────┐
│   ROUTE-SPECIFIC MIDDLEWARES                     │
│   ① validateMiddleware  → Validate input fields  │
│   ② authMiddleware      → Verify JWT token       │
│   ③ adminMiddleware     → Check admin role       │
└──────────────────────────────────────────────────┘
       ↓
   CONTROLLER → SERVICE → MODEL → MONGODB
       ↓
┌──────────────────────────────────────────────────┐
│   GLOBAL ERROR HANDLER                           │
│   Sends consistent JSON error response           │
└──────────────────────────────────────────────────┘
```

### CORS Configuration (for React dev server)

```javascript
// backend/app.js
app.use(cors({
  origin: ['http://localhost:5173', 'http://localhost:3000'],
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));
```

---

## 🔬 Aggregation Pipelines

### Monthly Average

```javascript
Price.aggregate([
  { $match: { isDeleted: false } },
  { $group: {
      _id: { year: '$year', month: '$month' },
      avgValue: { $avg: '$value' },
      count: { $sum: 1 }
  }},
  { $sort: { '_id.year': -1, '_id.month': -1 } }
])
```

### Top Countries

```javascript
Price.aggregate([
  { $match: { isDeleted: false } },
  { $group: { _id: '$countryCode', count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 10 },
  { $project: { countryCode: '$_id', count: 1, _id: 0 } }
])
```

---

## ⚡ Performance Optimization

### Backend Indexes

```javascript
PriceSchema.index({ countryCode: 1 });
PriceSchema.index({ year: 1 });
PriceSchema.index({ month: 1 });
PriceSchema.index({ countryCode: 1, year: 1 });
PriceSchema.index({ countryCode: 1, year: 1, month: 1 });
PriceSchema.index({ indicator: 1, year: 1 });
```

### Frontend Optimizations

- **Lazy loading** — `React.lazy()` + `Suspense` for page-level code splitting
- **Axios caching** — Cache frequently-used stat endpoints in state or context
- **Debounced search** — Delay API calls while user types in search
- **Pagination** — Avoid fetching full datasets; use `page` + `limit` params
- **Memoization** — `useMemo` / `useCallback` for expensive computations

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        BROWSER                                  │
│   React App (Vite)                                              │
│   ┌──────────┬──────────┬─────────────┬──────────────────────┐ │
│   │  Pages   │Components│  Context /  │   Axios API Layer    │ │
│   │(Routes)  │  (UI)    │  Hooks      │ (HTTP to backend)    │ │
│   └──────────┴──────────┴─────────────┴──────────────────────┘ │
└──────────────────────────────┬──────────────────────────────────┘
                               │  HTTP (JSON)
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                      NODE.JS SERVER                             │
│   Express App                                                   │
│   ┌──────────┬─────────────┬──────────┬──────────────────────┐ │
│   │  Routes  │ Controllers │ Services │   Middlewares/Utils  │ │
│   └──────────┴─────────────┴──────────┴──────────────────────┘ │
│                            │                                    │
│                            ▼                                    │
│                  Mongoose Models                                 │
└──────────────────────────────┬──────────────────────────────────┘
                               │
                               ▼
                    ┌─────────────────┐
                    │    MongoDB      │
                    │ prices          │
                    │ countries       │
                    │ indicators      │
                    │ users           │
                    └─────────────────┘
```

---

## 🌐 Deployment

### Frontend — Vercel / Netlify

```bash
cd frontend
npm run build     # Creates dist/ folder

# Vercel
npx vercel        # Follow prompts

# Netlify
npx netlify deploy --prod --dir=dist
```

**Set environment variable on platform:**
```
VITE_API_BASE_URL = https://your-backend.onrender.com/api/v1
```

### Backend — Render / Railway

```bash
# 1. Push to GitHub
git add . && git commit -m "Production ready" && git push

# 2. Connect repo on Render.com or Railway.app
# 3. Set environment variables in dashboard
# 4. Set start command: node server.js
```

### MongoDB Atlas

```bash
# In backend .env:
MONGO_URI=mongodb+srv://<user>:<password>@cluster0.xxxxx.mongodb.net/human_capital
NODE_ENV=production
```

### Production CORS

```javascript
// backend/app.js — update for production
origin: process.env.NODE_ENV === 'production'
  ? 'https://your-frontend.vercel.app'
  : ['http://localhost:5173', 'http://localhost:3000']
```

---

## ✅ Full Stack Checklist

| # | Section | Status |
|---|---------|--------|
| 0 | Dataset Understanding & Planning | ✅ |
| 1 | Project Setup (Backend + Frontend) | ✅ |
| 2 | MongoDB Fundamentals | ✅ |
| 3 | MongoDB Connection | ✅ |
| 4 | Schema Design (4 models) | ✅ |
| 5 | CRUD Operations | ✅ |
| 6 | Advanced Querying (filter, sort, paginate, search) | ✅ |
| 7 | RESTful API Routing (100+ endpoints) | ✅ |
| 8 | Node.js Core Concepts | ✅ |
| 9 | Express.js Implementation | ✅ |
| 10 | Middleware System | ✅ |
| 11 | CORS (configured for React) | ✅ |
| 12 | MVC Architecture | ✅ |
| 13 | JWT Authentication (Access + Refresh) | ✅ |
| 14 | Error Handling (global + async) | ✅ |
| 15 | MongoDB Indexes & Performance | ✅ |
| 16 | Aggregation Framework | ✅ |
| 17 | System Design | ✅ |
| 18 | Frontend — React.js + Vite | ✅ |
| 19 | Frontend — Axios + Interceptors | ✅ |
| 20 | Frontend — Protected Routes | ✅ |
| 21 | Frontend — Auth Context | ✅ |
| 22 | Frontend — Charts & Data Viz | ✅ |
| 23 | Deployment Ready | ✅ |

---

## 📄 License

MIT License — Free to use for educational and commercial purposes.
