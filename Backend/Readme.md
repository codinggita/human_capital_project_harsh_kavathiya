# 🍽️ Human Capital — Food Price Statistics API

<div align="center">

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-brightgreen?style=flat-square&logo=node.js)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express-4.x-lightgrey?style=flat-square&logo=express)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-NoSQL-13aa52?style=flat-square&logo=mongodb)](https://www.mongodb.com/)
[![JWT](https://img.shields.io/badge/JWT-Authentication-orange?style=flat-square)](https://jwt.io/)
[![MVC](https://img.shields.io/badge/Architecture-MVC-blue?style=flat-square)](.)
[![API](https://img.shields.io/badge/API-RESTful-red?style=flat-square)](.)
[![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)](.)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)

**A Production-Ready RESTful API for FAO Food Price Statistics**
**Built with Node.js · Express.js · MongoDB · JWT Auth · MVC Architecture**

[🚀 Quick Start](#-quick-start) · [📁 Folder Structure](#-folder-structure) · [📊 API Docs](#-api-documentation) · [🔐 Auth Flow](#-authentication-flow) · [✅ Checklist](#-checklist-coverage)

</div>

---

## 📊 Project Overview

| Metric | Value |
|--------|-------|
| 🔌 Total API Endpoints | **100+** |
| 🗄️ MongoDB Collections | **4** |
| 🔐 Auth Type | **JWT + Refresh Token** |
| ⚡ Rate Limit | **100 req / 15 min** |
| 🏗️ Architecture | **MVC + Service Layer** |
| 📦 Core Dependencies | **11** |
| 🌍 Dataset | **FAO Food Price Index** |
| 🔄 API Version | **v1 (/api/v1)** |

---


## 0️⃣ Dataset Understanding & Planning

> ✅ Checklist Item 0 — MANDATORY FIRST STEP

### Dataset Source
**FAO (Food and Agriculture Organization)** — Monthly food price statistics across multiple countries and indicators.

### Raw JSON Structure
```json
[
  {
    "countryCode": "IND",
    "indicator": "FAO_CP_23012",
    "year": 2020,
    "month": 5,
    "value": 142.36,
    "freq": "M"
  }
]
```

### Entities Identified from Dataset

| Entity | Collection | Description |
|--------|-----------|-------------|
| Price Record | `prices` | Core FAO data — main collection |
| Country | `countries` | Country reference (code + name) |
| Indicator | `indicators` | FAO indicator code + description |
| User | `users` | Registered API users |

### Relationships Between Entities

```
prices.countryCode  ──→  countries.countryCode  (Reference)
prices.indicator    ──→  indicators.code         (Reference)
users               ──→  prices (via admin/protected routes)
```

### Data Flow Between APIs

```
dataset.json (FAO)
     ↓
seeds/seedData.js (Import Script)
     ↓
MongoDB prices Collection (10,000+ records)
     ↓
Price Model (Mongoose Schema)
     ↓
Price Service (Business Logic)
     ↓
Price Controller (Request Handler)
     ↓
Price Routes (/api/v1/prices)
     ↓
Client Response (JSON)
```

---

## 🛠️ Tech Stack

> ✅ Checklist Item 1 — Project Setup

<table>
<tr>
<td width="50%">

### Runtime & Framework
```
Node.js 18+         → JavaScript runtime
Express.js 4.x      → Web framework
MongoDB             → NoSQL database
Mongoose            → MongoDB ODM
```

</td>
<td width="50%">

### Security & Utilities
```
jsonwebtoken        → JWT auth
bcryptjs            → Password hashing
express-validator   → Input validation
express-rate-limit  → Rate limiting
cors                → Cross-origin
morgan              → HTTP logging
dotenv              → Env variables
nodemon             → Dev auto-reload
```

</td>
</tr>
</table>

---

## 📁 Folder Structure

> ✅ Checklist Item 1 — Clean Architecture

```
human-capital-backend/
│
├── 📂 config/
│   └── db.js                    ← MongoDB connection
│
├── 📂 models/                   ← Mongoose schemas
│   ├── Price.js                 ← Price schema (core)
│   ├── Country.js               ← Country schema
│   ├── Indicator.js             ← Indicator schema
│   └── User.js                  ← User/Auth schema
│
├── 📂 controllers/              ← Request/Response only
│   ├── priceController.js
│   ├── countryController.js
│   ├── indicatorController.js
│   ├── statsController.js
│   ├── authController.js
│   └── searchController.js
│
├── 📂 services/                 ← Business logic only
│   ├── priceService.js
│   ├── statsService.js
│   └── authService.js
│
├── 📂 routes/                   ← Route definitions
│   ├── priceRoutes.js           ← /api/v1/prices
│   ├── countryRoutes.js         ← /api/v1/countries
│   ├── indicatorRoutes.js       ← /api/v1/indicators
│   ├── statsRoutes.js           ← /api/v1/stats
│   ├── authRoutes.js            ← /api/v1/auth
│   ├── searchRoutes.js          ← /api/v1/search
│   ├── jwtRoutes.js             ← /api/v1/jwt
│   ├── adminRoutes.js           ← /api/v1/admin
│   └── protectedRoutes.js       ← /api/v1/protected
│
├── 📂 middlewares/              ← Cross-cutting concerns
│   ├── authMiddleware.js        ← JWT verification
│   ├── adminMiddleware.js       ← Admin role check
│   ├── errorMiddleware.js       ← Global error handler
│   ├── rateLimitMiddleware.js   ← Rate limiting
│   ├── loggerMiddleware.js      ← Request logging
│   └── validateMiddleware.js    ← Input validation
│
├── 📂 utils/                    ← Shared helpers
│   ├── pagination.js            ← Reusable pagination
│   ├── filterBuilder.js         ← Dynamic filter builder
│   ├── asyncHandler.js          ← Async error wrapper
│   └── apiResponse.js           ← Standardized responses
│
├── 📂 seeds/
│   └── seedData.js              ← Import dataset to MongoDB
│
├── 📄 app.js                    ← Express app setup
├── 📄 server.js                 ← Entry point
├── 📄 dataset.json              ← FAO dataset (place here)
├── 📄 .env                      ← Environment variables
├── 📄 .env.example              ← Template for env vars
├── 📄 .gitignore
└── 📄 package.json
```

## 🔧 Environment Variables

> ✅ Checklist Item 1 — Environment Setup

```bash
# ── Server ──────────────────────────────────────
PORT=5000
NODE_ENV=development

# ── Database ─────────────────────────────────────
# Local MongoDB:
MONGO_URI=mongodb://localhost:27017/human_capital
# OR MongoDB Atlas (cloud):
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

---

## 🗄️ MongoDB Fundamentals

> ✅ Checklist Item 2 — MongoDB Concepts Applied

| Concept | Implementation |
|---------|---------------|
| **NoSQL** | Documents stored as BSON (JSON-like) |
| **Collections** | `prices`, `countries`, `indicators`, `users` |
| **Documents** | Each price record = one document |
| **Embedding** | OTP stored inside User document |
| **Referencing** | `countryCode` references Countries collection |
| **Indexing** | Applied on `year`, `month`, `countryCode`, `value` |
| **Aggregation** | Used for stats, averages, top countries |

### MongoDB Connection

> ✅ Checklist Item 3 — DB Connection in config/db.js

```javascript
// config/db.js
const mongoose = require('mongoose');

const connectDB = async () => {
  const conn = await mongoose.connect(process.env.MONGO_URI);
  console.log(`MongoDB connected: ${conn.connection.host}`);
};

module.exports = connectDB;
```

---

## 📐 Schema Design

> ✅ Checklist Item 4 — Core MongoDB Modeling

### Price Schema (Main Collection)

```javascript
// models/Price.js
{
  countryCode: { type: String, required: true, uppercase: true, trim: true },
  indicator:   { type: String, required: true, trim: true },
  year:        { type: Number, required: true },
  month:       { type: Number, required: true, min: 1, max: 12 },
  value:       { type: Number, required: true },
  freq:        { type: String, default: 'M', enum: ['M', 'A'] },
  isDeleted:   { type: Boolean, default: false },   // ← Soft Delete
  timestamps:  true                                  // ← createdAt, updatedAt
}
// Indexes: countryCode, year, month, indicator, value
```

### Country Schema

```javascript
// models/Country.js
{
  countryCode: { type: String, required: true, unique: true, uppercase: true },
  name:        { type: String, required: true },
  timestamps:  true
}
```

### Indicator Schema

```javascript
// models/Indicator.js
{
  code:        { type: String, required: true, unique: true },
  description: { type: String, required: true },
  timestamps:  true
}
```

### User Schema

```javascript
// models/User.js
{
  name:      { type: String, required: true },
  email:     { type: String, required: true, unique: true, lowercase: true },
  password:  { type: String, required: true },   // bcrypt hashed
  role:      { type: String, enum: ['user', 'admin'], default: 'user' },
  otp:       { code: String, expiresAt: Date },  // OTP embedded
  timestamps: true
}
```

### Collection Relationships Diagram

```
┌─────────────────────────────────────────────────────┐
│                    PRICE DOCUMENT                   │
│  {                                                  │
│    _id:         ObjectId,                           │
│    countryCode: "IND",   ──────────→ countries      │
│    indicator:   "FAO_CP_23012", ───→ indicators     │
│    year:        2020,                               │
│    month:       5,                                  │
│    value:       142.36,                             │
│    freq:        "M",                                │
│    isDeleted:   false,                              │
│    createdAt:   ISODate,                            │
│    updatedAt:   ISODate                             │
│  }                                                  │
└─────────────────────────────────────────────────────┘

┌───────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│   COUNTRY DOC     │    │  INDICATOR DOC   │    │    USER DOC      │
│  countryCode: IND │    │  code: FAO_CP... │    │  role: admin     │
│  name: India      │    │  description:... │    │  email: ...      │
└───────────────────┘    └──────────────────┘    └──────────────────┘
```

---

## 📝 CRUD Operations

> ✅ Checklist Item 5 — Core Backend Logic

### Price CRUD

| Operation | Method | Endpoint | Controller |
|-----------|--------|----------|------------|
| **Create** | `POST` | `/api/v1/prices` | `createPrice()` |
| **Read All** | `GET` | `/api/v1/prices` | `getAllPrices()` |
| **Read One** | `GET` | `/api/v1/prices/:id` | `getPriceById()` |
| **Update** | `PATCH` | `/api/v1/prices/:id` | `updatePrice()` |
| **Replace** | `PUT` | `/api/v1/prices/:id` | `replacePrice()` |
| **Delete** | `DELETE` | `/api/v1/prices/:id` | `deletePrice()` |

**Create Price — Request Body:**
```json
{
  "countryCode": "IND",
  "indicator": "FAO_CP_23012",
  "year": 2025,
  "month": 1,
  "value": 156.80,
  "freq": "M"
}
```

**Success Response:**
```json
{
  "success": true,
  "message": "Price record created successfully",
  "data": {
    "_id": "64a1b2c3d4e5f6a7b8c9d0e1",
    "countryCode": "IND",
    "indicator": "FAO_CP_23012",
    "year": 2025,
    "month": 1,
    "value": 156.80,
    "freq": "M",
    "isDeleted": false,
    "createdAt": "2026-05-28T10:00:00.000Z"
  }
}
```

---

## 🔍 Advanced MongoDB Querying

> ✅ Checklist Item 6 — Filtering, Pagination, Sorting, Search

### Query Parameters Reference

#### 🔵 Filtering

| Parameter | Type | Example | Description |
|-----------|------|---------|-------------|
| `country` | String | `?country=IND` | By country code |
| `year` | Number | `?year=2020` | By year |
| `month` | Number | `?month=5` | By month (1–12) |
| `indicator` | String | `?indicator=FAO_CP_23012` | By indicator |
| `freq` | String | `?freq=M` | By frequency |
| `minValue` | Number | `?minValue=50` | Min value filter |
| `maxValue` | Number | `?maxValue=200` | Max value filter |

#### 🟢 Sorting

| Parameter | Example | Description |
|-----------|---------|-------------|
| `sort` | `?sort=value` | Ascending by value |
| `sort` | `?sort=-value` | Descending (prefix `-`) |
| `sort` | `?sort=year,-value` | Multi-field (comma-separated) |

Supported fields: `value`, `year`, `month`, `country`, `indicator`, `freq`, `createdAt`, `updatedAt`

#### 🟡 Pagination

| Parameter | Default | Example | Description |
|-----------|---------|---------|-------------|
| `page` | `1` | `?page=2` | Page number |
| `limit` | `10` | `?limit=20` | Records per page |

#### 🔴 Search

| Parameter | Example | Description |
|-----------|---------|-------------|
| `search` | `?search=consumer` | Search in indicator text |
| `contains` | `?contains=price` | Partial match |
| `latest` | `?latest=true` | Latest records only |
| `recent` | `?recent=true` | Recent records only |
| `random` | `?random=true` | Random sample |

### MongoDB Operators Used

```javascript
// Filtering operators
{ year: { $gte: 2015, $lte: 2020 } }      // $gte, $lte
{ countryCode: { $in: ['IND', 'USA'] } }   // $in
{ value: { $gt: 100 } }                    // $gt, $lt

// Search with Regex (case-insensitive)
{ indicator: { $regex: 'consumer', $options: 'i' } }

// Combined example
GET /api/v1/prices?country=IND&year=2020&sort=-value&page=1&limit=10
→ Price.find({ countryCode: 'IND', year: 2020 })
         .sort({ value: -1 })
         .skip(0)
         .limit(10)
```

---

## 📊 API Documentation

> ✅ Checklist Item 7 — RESTful API Routing

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

---

### 🏠 Base Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Welcome message + all routes |
| `GET` | `/health` | Server health status |
| `GET` | `/version` | API version info |
| `GET` | `/server-status` | Memory & uptime metrics |
| `GET` | `/metrics` | CPU, PID, performance data |
| `GET` | `/api/v1` | All v1 available endpoints |

---

### 💰 Price Routes

#### Basic CRUD

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/prices` | All prices (filter/sort/paginate) |
| `GET` | `/prices/:id` | Single price by ID |
| `POST` | `/prices` | Create new price |
| `PUT` | `/prices/:id` | Full replace |
| `PATCH` | `/prices/:id` | Partial update |
| `DELETE` | `/prices/:id` | Delete record |

#### Route Parameters

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/prices/country/:code` | By country |
| `GET` | `/prices/year/:year` | By year |
| `GET` | `/prices/month/:month` | By month |
| `GET` | `/prices/indicator/:indicator` | By indicator |
| `GET` | `/prices/frequency/:freq` | By frequency |
| `GET` | `/prices/range/:start/:end` | Year range |
| `GET` | `/prices/country/:code/year/:year` | Country + year |
| `GET` | `/prices/country/:code/month/:month` | Country + month |
| `GET` | `/prices/country/:code/latest` | Latest by country |
| `GET` | `/prices/country/:code/history` | Full history |
| `GET` | `/prices/year/:year/highest` | Highest in year |
| `GET` | `/prices/year/:year/lowest` | Lowest in year |
| `GET` | `/prices/random` | Random sample |
| `GET` | `/prices/latest` | Latest records |
| `GET` | `/prices/recent` | Recent records |
| `GET` | `/prices/trending` | Trending prices |
| `GET` | `/prices/high-value` | High value prices |
| `GET` | `/prices/low-value` | Low value prices |



### 🌍 Country Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/countries` | All countries |
| `POST` | `/countries` | Create country |
| `GET` | `/countries?page=1&limit=10` | Paginated |

---

### 📈 Statistics Routes

> Uses MongoDB Aggregation Pipelines

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
| `GET` | `/stats/records-count` | Total record count |
| `GET` | `/stats/trending` | Trending stats |
| `GET` | `/stats/country/:code` | Country analysis |
| `GET` | `/stats/year/:year` | Year analysis |
| `GET` | `/stats/month/:month` | Month analysis |

**Example: `/stats/top-countries` Response:**
```json
{
  "success": true,
  "message": "Top countries fetched",
  "data": [
    { "countryCode": "IND", "count": 1248 },
    { "countryCode": "USA", "count": 1100 },
    { "countryCode": "CHN", "count": 984 }
  ]
}
```

---

### 🔎 Search Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/search/country?name=India` | Search by country name |
| `GET` | `/search/indicator?text=Consumer` | Search indicators |
| `GET` | `/search/value?value=68` | Search near value |
| `GET` | `/search/year?year=2020` | Search by year |
| `GET` | `/search/frequency?freq=M` | Search by freq |
| `GET` | `/search/prices?q=general` | Full text search |
| `GET` | `/search/prices?q=inflation` | Search inflation |

---

### 🔐 Authentication Routes

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `POST` | `/auth/register` | Create account | ❌ |
| `POST` | `/auth/login` | Get JWT tokens | ❌ |
| `POST` | `/auth/logout` | Logout user | ✅ |
| `POST` | `/auth/refresh-token` | New access token | ❌ |
| `GET` | `/auth/me` | Current user profile | ✅ |
| `POST` | `/auth/change-password` | Update password | ✅ |
| `POST` | `/auth/forgot-password` | Request reset | ❌ |
| `POST` | `/auth/reset-password` | Apply reset | ❌ |
| `POST` | `/auth/send-otp` | Send OTP | ❌ |
| `POST` | `/auth/verify-otp` | Verify OTP | ❌ |

---

### 🔑 JWT Routes

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `POST` | `/jwt/generate-token` | Generate token | ❌ |
| `POST` | `/jwt/verify-token` | Verify a token | ❌ |
| `POST` | `/jwt/refresh-token` | Refresh token | ❌ |
| `GET` | `/jwt/profile` | Protected profile | ✅ |
| `GET` | `/jwt/dashboard` | Protected dashboard | ✅ |
| `GET` | `/jwt/admin` | Admin only | ✅ Admin |
| `GET` | `/jwt/user` | User route | ✅ |
| `GET` | `/jwt/check-role/admin` | Check admin role | ✅ |
| `GET` | `/jwt/check-role/user` | Check user role | ✅ |

---

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

### 🔒 Protected Routes

> Requires `Authorization: Bearer <token>` (any role)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/protected/prices` | Prices (authenticated) |
| `POST` | `/protected/prices` | Create (authenticated) |
| `PATCH` | `/protected/prices/:id` | Update (authenticated) |
| `DELETE` | `/protected/prices/:id` | Delete (authenticated) |

---

## 🔐 Authentication Flow

> ✅ Checklist Item 13 — JWT Based Authentication

```
┌────────────────────────────────────────────────────────────────┐
│                     AUTH FLOW                                  │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  1. REGISTER                                                   │
│     POST /auth/register { name, email, password }              │
│     → Password hashed with bcrypt (10 rounds)                 │
│     → User stored in MongoDB                                   │
│     → Return: success message                                  │
│                                                                │
│  2. LOGIN                                                      │
│     POST /auth/login { email, password }                       │
│     → Compare password with bcrypt                             │
│     → Generate Access Token (7d) + Refresh Token (30d)        │
│     → Return: { user, accessToken, refreshToken }              │
│                                                                │
│  3. PROTECTED REQUEST                                          │
│     Any protected route                                        │
│     Header: Authorization: Bearer <accessToken>               │
│     → authMiddleware verifies token                            │
│     → Attaches user to req.user                                │
│     → Proceeds to controller                                   │
│                                                                │
│  4. TOKEN REFRESH                                              │
│     POST /auth/refresh-token { refreshToken }                  │
│     → Verify refresh token                                     │
│     → Issue new access token                                   │
│                                                                │
│  5. ROLE CHECK (Admin routes)                                  │
│     → authMiddleware (verify JWT)                              │
│     → adminMiddleware (check role === 'admin')                 │
│     → Allow or return 403 Forbidden                            │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

**Register Example:**
```bash
POST /api/v1/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "SecurePass123!"
}
```

**Login Response:**
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "user": {
      "id": "64a1b2c3...",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user"
    },
    "accessToken": "eyJhbGci...",
    "refreshToken": "eyJhbGci..."
  }
}
```

---

## 🧱 Middleware System

> ✅ Checklist Item 10 — Middleware Chain

```
Incoming Request
       ↓
┌──────────────────────────────────────────────────┐
│   GLOBAL MIDDLEWARES (app.js)                    │
│   ① cors()              → Allow cross-origin     │
│   ② express.json()      → Parse JSON body        │
│   ③ morgan('dev')       → Log requests (dev only)│
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
┌──────────────────────────────────────────────────┐
│   CONTROLLER                                     │
│   Handles req/res only, calls service            │
└──────────────────────────────────────────────────┘
       ↓
┌──────────────────────────────────────────────────┐
│   GLOBAL ERROR HANDLER (errorMiddleware.js)      │
│   Catches all errors, sends consistent response  │
└──────────────────────────────────────────────────┘
```

### Middleware Reference

| File | Purpose | Applied On |
|------|---------|-----------|
| `authMiddleware.js` | Verify JWT, attach `req.user` | Protected routes |
| `adminMiddleware.js` | Check `role === 'admin'` | Admin routes |
| `errorMiddleware.js` | Global error handler | All errors |
| `rateLimitMiddleware.js` | Limit requests per IP | All routes |
| `loggerMiddleware.js` | Log method, URL, time | All routes |
| `validateMiddleware.js` | Validate request body | POST/PATCH routes |

---


## 🔬 Aggregation Framework

> ✅ Checklist Item 16 — MongoDB Aggregation Pipelines

### Pipelines Implemented

#### 1. Monthly Average
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

#### 2. Top Countries
```javascript
Price.aggregate([
  { $match: { isDeleted: false } },
  { $group: { _id: '$countryCode', count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 10 },
  { $project: { countryCode: '$_id', count: 1, _id: 0 } }
])
```

#### 3. Value Distribution (Buckets)
```javascript
Price.aggregate([
  { $bucket: {
      groupBy: '$value',
      boundaries: [0, 50, 100, 150, 200, 300],
      default: '300+',
      output: { count: { $sum: 1 }, avg: { $avg: '$value' } }
  }}
])
```

#### 4. Trending (3-Month Comparison)
```javascript
Price.aggregate([
  { $facet: {
      recent3Months: [...],
      previous3Months: [...]
  }},
  { $project: { trendPercentage: {...} } }
])
```

---

## ⚡ Performance Optimization

> ✅ Checklist Item 15 — MongoDB Performance

### Indexes Applied

```javascript
// Price Model — frequently queried fields
PriceSchema.index({ countryCode: 1 });
PriceSchema.index({ year: 1 });
PriceSchema.index({ month: 1 });
PriceSchema.index({ indicator: 1 });
PriceSchema.index({ value: 1 });
PriceSchema.index({ countryCode: 1, year: 1 });       // compound
PriceSchema.index({ countryCode: 1, year: 1, month: 1 }); // compound
PriceSchema.index({ indicator: 1, year: 1 });          // compound
```

### Query Optimization

- **Projection** — Select only required fields
- **Pagination** — `.skip().limit()` to avoid full collection scans
- **Index hints** — Compound indexes for common query patterns
- **Lean queries** — `.lean()` for read-only data (faster)

---

## 🏗️ MVC Architecture

> ✅ Checklist Item 12 — Industry Standard Pattern

```
Client Request
     │
     ▼
  ROUTES            → Define URL patterns, attach middlewares
     │
     ▼
  CONTROLLERS       → Handle req/res ONLY, NO business logic
     │
     ▼
  SERVICES          → Business logic ONLY, NO req/res
     │
     ▼
  MODELS            → Database schema & queries ONLY
     │
     ▼
  MONGODB           → Data storage
```

### Separation of Concerns

| Layer | File | Responsibility |
|-------|------|----------------|
| **Route** | `priceRoutes.js` | URL mapping + middleware chain |
| **Controller** | `priceController.js` | Parse request → call service → send response |
| **Service** | `priceService.js` | Business logic, filtering, sorting |
| **Model** | `Price.js` | Schema + DB queries |
| **Utility** | `pagination.js` | Reusable logic across all layers |

---

## 🌐 System Design

> ✅ Checklist Item 17 — Architecture Understanding

### Monolithic Architecture (Current)

```
┌───────────────────────────────────────────────────┐
│              MONOLITHIC SERVER                    │
│   Express App running on single Node.js process  │
│                                                   │
│   ┌───────┬───────────┬──────┬─────────────────┐ │
│   │Routes │Controllers│Models│Middlewares/Utils│ │
│   └───────┴───────────┴──────┴─────────────────┘ │
│                                                   │
│   MongoDB (single database)                       │
└───────────────────────────────────────────────────┘
```

### Scaling Concepts

| Concept | Description |
|---------|-------------|
| **Vertical Scaling** | Upgrade server RAM/CPU |
| **Horizontal Scaling** | Add more server instances |
| **Load Balancing** | Distribute requests across servers (e.g. Nginx) |
| **Caching** | Redis for frequent queries |
| **Replication** | MongoDB replica sets for high availability |
| **Sharding** | Split MongoDB across multiple machines |
---

## 🌟 Good To Have Features

> ✅ Checklist Item 19 — Implemented Features

| # | Feature | Status | Description |
|---|---------|--------|-------------|
| 1 | API Response Standardization | ✅ Done | `utils/apiResponse.js` — `{ success, message, data, meta }` |
| 2 | Request Logging Middleware | ✅ Done | `middlewares/loggerMiddleware.js` — method, URL, timestamp |
| 3 | Centralized Async Error Handler | ✅ Done | `utils/asyncHandler.js` — wraps all async controllers |
| 4 | Environment-based Config | ✅ Done | Dev/prod configs via `.env` + `NODE_ENV` |
| 5 | Soft Delete Feature | ✅ Done | `isDeleted: true` flag instead of removing |
| 6 | Timestamp Tracking | ✅ Done | `createdAt` + `updatedAt` on all schemas |
| 7 | Basic Rate Limiting | ✅ Done | 100 req/15 min general, 10/15 min auth |
| 8 | Advanced Search with Regex | ✅ Done | Case-insensitive regex search |
| 9 | Database Seeding Script | ✅ Done | `seeds/seedData.js` — bulk import dataset |
| 10 | Reusable Pagination Utility | ✅ Done | `utils/pagination.js` used across all routes |
| 11 | Dynamic Filter Builder | ✅ Done | `utils/filterBuilder.js` |
| 12 | Role-Based Access Control | ✅ Done | `admin` + `user` roles enforced |
| 13 | API Versioning | ✅ Done | All routes under `/api/v1/` |
| 14 | Health Check API | ✅ Done | `GET /health` returns uptime + DB status |
| 15 | Password Hashing (bcrypt) | ✅ Done | Salt rounds = 10 |
| 16 | JWT Token Expiry Handling | ✅ Done | `TokenExpiredError` caught + handled |

---

## ✅ Checklist Coverage

> Full project completion status

### Core Requirements

| # | Section | Status |
|---|---------|--------|
| 0 | Dataset Understanding & Planning | ✅ Complete |
| 1 | Project Setup & Structure | ✅ Complete |
| 2 | MongoDB Fundamentals | ✅ Complete |
| 3 | MongoDB Connection & Config | ✅ Complete |
| 4 | Schema Design | ✅ Complete |
| 5 | CRUD Operations | ✅ Complete |
| 6 | Advanced Querying | ✅ Complete |
| 7 | API Routing System | ✅ Complete |
| 8 | Node.js Core Concepts | ✅ Complete |
| 9 | Express.js Implementation | ✅ Complete |
| 10 | Middleware System | ✅ Complete |
| 11 | CORS Implementation | ✅ Complete |
| 12 | MVC Architecture | ✅ Complete |
| 13 | JWT Authentication | ✅ Complete |
| 14 | Error Handling System | ✅ Complete |
| 15 | MongoDB Performance | ✅ Complete |
| 16 | Aggregation Framework | ✅ Complete |
| 17 | System Design | ✅ Complete |
| 18 | Documentation (README + Postman) | ✅ Complete |
| 19 | Good To Have (16/20) | ✅ Complete |

### Final Evaluation Criteria

| Criteria | Status |
|----------|--------|
| All CRUD APIs working | ✅ |
| Clean MongoDB schema design | ✅ |
| Advanced queries (filter, sort, search, pagination) | ✅ |
| JWT authentication working | ✅ |
| Middleware system structured | ✅ |
| Error handling consistent | ✅ |
| Aggregation pipeline implemented | ✅ |
| MVC architecture followed | ✅ |
| Full dataset integrated | ✅ |
| Postman documentation complete | ✅ |

---

## 🚀 Deployment

### MongoDB Atlas Setup

```bash
# 1. Create free cluster at mongodb.com/atlas
# 2. Get connection string
# 3. Update .env:
MONGO_URI=mongodb+srv://<user>:<password>@cluster0.xxxxx.mongodb.net/human_capital
NODE_ENV=production
```

### Render / Railway Deployment

```bash
# 1. Push code to GitHub
git add .
git commit -m "Production ready"
git push origin main

# 2. Connect repo to Render/Railway
# 3. Set environment variables in dashboard
# 4. Deploy — live URL provided automatically
```

---



## 📄 License

MIT License — Free to use for educational and commercial purposes.

---
