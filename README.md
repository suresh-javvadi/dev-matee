# DevTinder

A "Tinder for developers" — a full-stack MERN app where developers create profiles, swipe through a feed, send connection requests, and manage matches. Built to practice production-style REST API design, JWT auth, and a React + Redux frontend.

## Features

- Signup / login with hashed passwords and JWT (httpOnly cookie) sessions
- Authenticated profile view, edit, and password change
- Feed of other users to connect with (paginated, excludes existing connections/requests)
- Send connection requests (`interested` / `ignored`)
- Review incoming requests (`accepted` / `rejected`)
- View your connections (matches) and pending requests received

## Tech Stack

| Layer     | Tech                                                        |
| --------- | ------------------------------------------------------------ |
| Frontend  | React 19, React Router, Redux Toolkit, Tailwind CSS, DaisyUI, Axios, Vite |
| Backend   | Node.js, Express 5, MongoDB, Mongoose                        |
| Auth      | JWT, bcrypt, httpOnly cookies                                 |
| Deployment| AWS EC2, PM2, Nginx                                           |

## Project Structure

```
backend/     Express REST API (auth, profile, requests, feed)
frontend/    React SPA (Vite + Redux Toolkit + Tailwind)
```

## API Overview

| Method | Endpoint                                   | Description                          |
| ------ | ------------------------------------------- | ------------------------------------- |
| POST   | `/signup`                                   | Create a new account                  |
| POST   | `/login`                                    | Log in, receive JWT cookie            |
| POST   | `/logout`                                   | Clear the cookie and log out          |
| GET    | `/profile/view`                             | View your own profile                 |
| PATCH  | `/profile/edit`                             | Edit your own profile                 |
| PATCH  | `/profile/password`                         | Change your password                  |
| POST   | `/request/send/:status/:toUserId`           | Send a request (`interested`/`ignored`) |
| PATCH  | `/request/review/:status/:requestId`        | Review a request (`accepted`/`rejected`) |
| GET    | `/user/requests/received`                   | List requests you've received         |
| GET    | `/user/connections`                         | List your matches                     |
| GET    | `/user/feed`                                | Discover other users (paginated)      |

All routes except `/signup` and `/login` require an authenticated session (JWT cookie).

## Getting Started

### Prerequisites

- Node.js 18+
- A MongoDB instance (local or [MongoDB Atlas](https://www.mongodb.com/atlas))

### Backend

```bash
cd backend
npm install
```

Create a `.env` file in `backend/`:

```env
MONGO_URI=mongodb://localhost:27017/dev_tinder
JWT_SECRET=your-secret-key
```

```bash
npm run dev     # starts on http://localhost:3000
```

### Frontend

```bash
cd frontend
npm install
npm run dev      # starts on http://localhost:5173
```

By default the frontend talks to `http://localhost:3000`. To point it elsewhere (e.g. in production), set `VITE_API_URL` in `frontend/.env.production`.

## Author

**Suresh Javvadi**
