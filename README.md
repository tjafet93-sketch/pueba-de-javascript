# Workspace Reservation App

A single-page application (SPA) for managing workspace reservations, built with vanilla JavaScript and Vite. Users can log in, create reservations, and track their status. Admins have full control to approve, reject, edit, or delete any reservation.

## Tech Stack

- **Vite** — build tool and dev server
- **Tailwind CSS v4** — utility-first styling via the Vite plugin
- **json-server** — mock REST API backed by `db.json`
- **concurrently** — runs Vite and json-server in parallel

## Project Structure

```
src/
├── api/
│   └── http.js              # Fetch wrapper (GET, POST, PUT, PATCH, DELETE)
├── assets/                  # Static images and SVGs
├── components/
│   ├── ReservationCard.js   # Reservation display card with role-based action buttons
│   └── Sidebar.js           # Navigation sidebar with logout
├── controllers/
│   ├── login.controller.js          # Login form handling and session creation
│   ├── home.controller.js           # Loads and filters reservations by role
│   ├── reservation.controller.js    # New reservation form submission
│   └── editReservation.controller.js # Edit form loading and submission
├── router/
│   └── router.js            # Client-side router with history API and auth guards
├── services/
│   └── reservation.service.js  # API calls for reservation CRUD
├── views/                   # View functions that return HTML strings
├── utils.js                 # Session helpers and notification system
├── main.js                  # App entry point
└── style.css                # Global styles
```

## Getting Started

**Prerequisites:** Node.js 18+

```bash
# Install dependencies
npm install

# Start the development server (Vite + json-server run together)
npm run dev
```

The app will be available at `http://localhost:5173` and the mock API at `http://localhost:3001`.

## Test Credentials

| Role  | Email           | Password |
|-------|-----------------|----------|
| Admin | admin@test.com  | A123456  |
| User  | user@test.com   | A123456  |
| User  | user2@test.com  | A123456  |

## Features

**All authenticated users**
- Log in and maintain a session via `localStorage`
- View their own reservations on the home page
- Create new reservations (status starts as `pending`)
- Edit or cancel their own reservations while status is `pending`

**Admin only**
- View all reservations from every user
- Approve, reject, edit, or delete any reservation

## Routing

Routes are handled client-side using the History API. Protected routes redirect to `/` if no session is found.

| Path               | View                  | Access    |
|--------------------|-----------------------|-----------|
| `/`                | Login                 | Public    |
| `/home`            | Home / dashboard      | Auth only |
| `/reservations`    | New reservation form  | Auth only |
| `/edit-reservation`| Edit reservation form | Auth only |

## API Endpoints

Served by json-server on port 3001.

| Method | Endpoint              | Description              |
|--------|-----------------------|--------------------------|
| GET    | /users                | Query users by email/password |
| GET    | /reservations         | Get all reservations     |
| POST   | /reservations         | Create a reservation     |
| PATCH  | /reservations/:id     | Update a reservation     |
| DELETE | /reservations/:id     | Delete a reservation     |

## Build

```bash
npm run build
```

Output goes to the `dist/` folder, ready for static hosting.
