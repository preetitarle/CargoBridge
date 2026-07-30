# 🚢 CargoBridge — Full-Stack Logistics Platform

India's container slot marketplace connecting SMEs with Freight Forwarders.

---

## 🗂 Project Structure

```
cargobridge/
├── backend/
│   ├── main.py           ← FastAPI server (all API routes)
│   ├── models.py         ← Database tables (SQLAlchemy)
│   ├── schemas.py        ← Request/response shapes (Pydantic)
│   ├── auth.py           ← JWT tokens + password hashing
│   ├── seed_data.py      ← 10 demo vessels + 3 demo users
│   ├── database.py       ← SQLite connection
│   └── requirements.txt  ← Python packages to install
├── frontend/
│   ├── index.html        ← Landing page + Auth modal
│   ├── api.js            ← Shared API client (used by all pages)
│   ├── translations.json ← English + Hindi strings
│   └── pages/
│       ├── dashboard.html  ← SME dashboard
│       └── forwarder.html  ← Freight Forwarder portal
├── START_BACKEND.bat     ← Windows: double-click to start
├── start_backend.sh      ← Mac/Linux: run to start
└── README.md
```

---

## ⚡ QUICKSTART (5 Steps)

### Step 1 — Install Python

- Go to https://www.python.org/downloads/
- Download Python **3.9 or newer**
- During install: ✅ **CHECK** "Add Python to PATH"
- Click Install

### Step 2 — Extract the ZIP

- Right-click the ZIP → Extract All
- Remember where you extracted it (e.g. Desktop/cargobridge)

### Step 3 — Start the Backend

**On Windows:**
- Open the `cargobridge` folder
- Double-click `START_BACKEND.bat`
- A black window opens — this is the server running
- You should see: `Uvicorn running on http://0.0.0.0:8000`

**On Mac/Linux:**
```bash
cd cargobridge
chmod +x start_backend.sh
./start_backend.sh
```

> ⚠️ Keep this window open! The server must stay running.

### Step 4 — Open the Frontend

- Open the `frontend` folder
- Double-click `index.html` to open in your browser

> ✅ That's it! The app is running.

### Step 5 — Login and explore

Use these demo accounts:

| Role | Email | Password |
|------|-------|----------|
| SME / Exporter | ria@sharmaexports.com | demo1234 |
| Freight Forwarder | arjun@mehtafreight.com | demo1234 |

---

## 🎯 How to Demo

### As an SME (Exporter):
1. Open `index.html` → click **Get Started**
2. Choose **SME / Exporter** → Sign In
3. Email: `ria@sharmaexports.com` / Password: `demo1234`
4. You're on the dashboard → see LIVE + AI listings
5. Set TEU needed → click **Search Slots**
6. Click **Book Slot** on any vessel
7. Choose payment method → **Confirm Payment**
8. Go to **My Bookings** to see your booking
9. Go to **Live Tracking** to see vessel movement

### As a Freight Forwarder:
1. Open `index.html` → **Get Started**
2. Choose **Freight Forwarder** → Sign In
3. Email: `arjun@mehtafreight.com` / Password: `demo1234`
4. Dashboard shows your listings and KPIs
5. Click **Add Empty Slots** → fill form → Publish
6. Click **Booking Requests** → Approve or Decline with message
7. Decline now sends a real rejection message (bug fixed!)

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /signup | Create account |
| POST | /login | Login, get JWT |
| GET | /listings | All active listings |
| GET | /listings/search | Search with filters |
| POST | /listings | Create listing (FF only) |
| PUT | /listings/{id} | Update listing |
| GET | /my-listings | My listings (FF) |
| POST | /book | Book a slot (SME) |
| GET | /my-bookings | My bookings (SME) |
| GET | /requests | Booking requests (FF) |
| POST | /approve/{id} | Approve request |
| POST | /reject/{id} | Reject with message |
| GET | /track/{booking_id} | Vessel tracking data |
| GET | /predictions | AI predicted slots |
| GET | /stats | Platform stats |
| GET | /co2 | CO2 savings calculator |
| WS | /ws/track/{id} | Live tracking WebSocket |

**Interactive API docs:** http://localhost:8000/docs

---

## 🧠 AI Prediction Logic

The AI engine generates predicted container slots based on:
- Historical route patterns (last 30 days of data)
- Available CBM calculation per route
- Confidence score (65–98%) based on route popularity
- CO2 savings estimation per predicted slot
- Results sorted by AI confidence score (highest first)
- Tagged with 🤖 in the UI so SMEs know it's a prediction

---

## 💾 Database

Uses **SQLite** (zero setup needed — file created automatically).

Tables:
- `users` — SMEs and Freight Forwarders
- `container_listings` — All vessel slot listings
- `bookings` — Confirmed bookings
- `booking_requests` — Forwarder approval queue
- `payments` — Mock payment records

The database file `cargobridge.db` is created in the `backend/` folder on first run.

**Data persists across restarts** — logout and log back in, your data is still there.

---

## 🌍 Multi-Language

- English (default) and Hindi supported
- Translation strings in `frontend/translations.json`
- Toggle in UI (language button in nav)

---

## 🐛 Issues Fixed vs Original

| Issue | Fix |
|-------|-----|
| Data lost on logout | All data now stored in SQLite DB |
| Decline had no message | Full rejection message flow added |
| Static mock data | All data fetched from real API |
| No auth | JWT auth with bcrypt password hashing |
| No persistence | DB persists across sessions |

---

## 🛠 Troubleshooting

**"pip is not recognized"**
→ Reinstall Python and check "Add to PATH"

**"Port 8000 already in use"**
→ Change port: `uvicorn main:app --port 8001`
→ Then update `API_BASE` in `frontend/api.js` to `http://localhost:8001`

**Browser shows "Failed to fetch"**
→ Make sure the backend is running (black terminal window)
→ Check you see `Uvicorn running on http://0.0.0.0:8000`

**CORS error in browser**
→ Don't open HTML files from a file:// URL in some browsers
→ Try: `python3 -m http.server 3000` in the frontend folder
→ Then open http://localhost:3000

---

## 📊 Demo Data Included

- **10 vessels** across India's top routes
- **5 routes**: Mumbai→Dubai, Mumbai→Singapore, Chennai→Rotterdam, Mundra→Hamburg, Kolkata→Felixstowe
- **3 demo users**: 1 SME, 2 Freight Forwarders
- **AI predictions** generated live per search
- **AIS tracking** simulated with real port coordinates

---

*Built for hackathon demo. CargoBridge — closing India's empty container gap.*
