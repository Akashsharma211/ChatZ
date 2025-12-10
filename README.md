# ChatZ

> A lightweight chat application with user onboarding and Stream-powered real-time chat.

## Overview

ChatZ is a full-stack chat application split into two folders: `backend` (Express + MongoDB + Stream) and `frontend` (React + Vite + Tailwind). The backend exposes REST endpoints for authentication, user management and chat features, while the frontend provides a modern UI that integrates with Stream for real-time messaging/video.

## Features

- Email/password signup & login (JWT via cookie)
- Onboarding flow (profile, languages, bio)
- Real-time chat using Stream
- User search, friend requests, notifications
- Frontend built with React + Vite and Tailwind

## Tech Stack

- Backend: Node.js, Express, Mongoose
- Realtime & Video: Stream (stream-chat, @stream-io/video-react-sdk)
- Frontend: React, Vite, Tailwind, Zustand

## Prerequisites

- Node.js (v18+ recommended)
- npm (or yarn)
- A MongoDB instance (Atlas or local)
- Stream account (API key & secret)

## Environment Variables

Create a `.env` file in `backend/` with the following variables:

- `MONGO_URI` : MongoDB connection string
- `JWT_SECRET_KEY` : Secret used for signing JWTs
- `STREAM_API_KEY` : Stream API key
- `STREAM_API_SECRET` : Stream API secret
- `PORT` (optional) : Backend server port (defaults to `5001`)
- `NODE_ENV` (optional) : `development` or `production`

Example `backend/.env`:

```powershell
MONGO_URI="mongodb+srv://<user>:<pass>@cluster0.mongodb.net/chatz?retryWrites=true&w=majority"
JWT_SECRET_KEY="your_jwt_secret"
STREAM_API_KEY="your_stream_api_key"
STREAM_API_SECRET="your_stream_api_secret"
PORT=5001
NODE_ENV=development
```

## Setup & Local Development

Open two terminals (one for backend, one for frontend).

- Backend (PowerShell):

```powershell
cd backend
npm install
npm run dev
# starts: nodemon src/server.js (dev)
```

- Frontend (PowerShell):

```powershell
cd frontend
npm install
npm run dev
# starts vite dev server (default at http://localhost:5173)
```

Notes:
- The backend uses CORS configured to allow `http://localhost:5173` by default.
- Authentication cookies are set by the backend; ensure both servers run during development.

## Production Build (simple approach)

1. Build the frontend:

```powershell
cd frontend
npm run build
```

2. Serve the built frontend with the backend. The backend serves files from `../frontend/dist` when `NODE_ENV` is `production`.

On Windows PowerShell you can run:

```powershell
$env:NODE_ENV = "production";
cd backend;
node src/server.js
```

Or add a `start` script to `backend/package.json` (optional) for a nicer production workflow.

## API Overview

Major routes are under `backend/src/routes`:

- `POST /api/auth/signup`  — register a new user
- `POST /api/auth/login`   — login (sets JWT cookie)
- `POST /api/auth/logout`  — clear cookie / logout
- `POST /api/auth/onboard` — complete onboarding (protected)
- `GET /api/users/*`       — user-related endpoints
- `POST /api/chat/*`       — chat endpoints

For full details, check the route handlers in `backend/src/routes` and the controllers in `backend/src/controllers`.

## Project Structure

- `backend/` — Express server, controllers, models, and Stream integration
  - `src/server.js` — entry-point
  - `src/lib/db.js` — Mongo connection
  - `src/lib/stream.js` — Stream SDK helpers
  - `src/controllers/` — auth, user, chat logic
  - `src/routes/` — route definitions

- `frontend/` — React app (Vite)
  - `src/` — React components, pages, hooks
  - `public/` — static assets

## Contributing

- Fork the repo and open a PR with a clear description of your changes.
- Run backend and frontend locally and include screenshots or tests when applicable.

## Troubleshooting

- If the frontend cannot connect to the backend, confirm both servers are running and that CORS origin matches.
- Check `backend` logs for DB connection issues (verify `MONGO_URI`).
- Ensure your Stream API key/secret are set and valid.

## License

This project does not include a license file by default. Add a `LICENSE` file if you plan to open-source it.

## Contact

Maintainer: Akashsharma211

Generated README for the ChatZ project.
