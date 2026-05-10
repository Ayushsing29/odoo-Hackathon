# ✈️ Traveloop — Travel Planning Application

A full-stack travel planning app built with React + Vite (frontend) and Express + SQLite (backend).

## Features

| Screen | Description |
|--------|-------------|
| Login / Signup | JWT-based authentication |
| Dashboard | Welcome, stats, recent trips, popular destinations |
| My Trips | Trip list with edit/view/delete |
| Create Trip | Form with name, dates, budget |
| Itinerary Builder | Add stops (cities) and activities per stop |
| Itinerary View | List view + calendar view by date |
| City Search | Filter by name/region, add to trip |
| Activity Search | Filter by city/category/cost, add to stop |
| Budget | Pie chart, bar chart, expense list, over-budget alert |
| Packing Checklist | Categorized items, progress bar, reset |
| Trip Notes | Per-trip/stop notes with edit/delete |
| Shared Itinerary | Public URL, copy trip, social share |
| User Profile | Edit name/avatar/language, saved destinations, delete account |

## Tech Stack

- **Frontend**: React 18, React Router v6, Recharts, Vite
- **Backend**: Express.js, sql.js (pure-JS SQLite), bcryptjs, JWT
- **Database**: SQLite (via sql.js, persisted to `traveloop.db`)

## Setup & Run

### 1. Install dependencies

```bash
# Backend
cd backend
npm install --ignore-scripts

# Frontend
cd ../frontend
npm install
```

### 2. Start the backend (port 4000)

```bash
cd backend
npm start
# or for dev with auto-reload:
npm run dev
```

### 3. Start the frontend (port 3000)

```bash
cd frontend
npm run dev
```

Open http://localhost:3000 in your browser.

## Database Schema

```
users          → id, name, email, password, avatar, language
trips          → id, user_id, name, description, start_date, end_date, is_public, share_token, total_budget
stops          → id, trip_id, city, country, start_date, end_date, order_index
activities     → id, stop_id, name, description, category, cost, duration, date, time
budget_items   → id, trip_id, category, label, amount, date
checklist_items→ id, trip_id, label, category, is_checked
notes          → id, trip_id, stop_id, content, created_at
saved_destinations → id, user_id, city, country
```

## API Endpoints

```
POST   /api/auth/signup
POST   /api/auth/login

GET    /api/trips
POST   /api/trips
GET    /api/trips/:id
PUT    /api/trips/:id
DELETE /api/trips/:id
GET    /api/trips/share/:token

POST   /api/trips/:tripId/stops
PUT    /api/stops/:id
DELETE /api/stops/:id

POST   /api/stops/:stopId/activities
PUT    /api/activities/:id
DELETE /api/activities/:id

GET/POST /api/trips/:tripId/budget
DELETE   /api/budget/:id

GET/POST /api/trips/:tripId/checklist
PUT/DELETE /api/checklist/:id

GET/POST /api/trips/:tripId/notes
PUT/DELETE /api/notes/:id

GET/PUT/DELETE /api/profile
POST/DELETE    /api/profile/saved/:city

GET /api/cities?q=&region=
GET /api/activities?city=&category=&max_cost=
```
