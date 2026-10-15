# Job Tracker API

A production-style REST API for tracking job applications, built with **Node.js, Express 5, TypeScript, PostgreSQL and Prisma**. It's the backend foundation for my AI projects: later months add a Next.js frontend, an LLM-powered assistant, and an AI agent that works on top of this API.

> 🚧 Work in progress — part of my [Full-stack AI Engineer Journey](https://github.com/githubnahid122/fullstack-ai-engineer-journey).

## Features

- [ ] User registration and login (JWT access tokens + refresh tokens in httpOnly cookies)
- [ ] CRUD for job applications: company, role, status, salary range, applied date, notes
- [ ] Pagination, filtering by status, and sorting on the list endpoint
- [ ] Request validation with Zod and a consistent error format
- [ ] Users can only access their own applications
- [ ] Rate limiting on auth routes
- [ ] Integration tests with Vitest + Supertest
- [ ] Structured logging and a health check
- [ ] Deployed with a hosted PostgreSQL database

## Tech stack

| Area | Tools |
| --- | --- |
| Runtime | Node.js (LTS), TypeScript |
| Framework | Express 5 |
| Database | PostgreSQL, Prisma ORM |
| Validation | Zod |
| Auth | JWT, bcrypt |
| Security | helmet, cors, express-rate-limit |
| Testing | Vitest, Supertest |
| Logging | Pino |

## Project structure

```
src/
  config/        Environment config (validated with Zod)
  routes/        URL → controller mapping
  controllers/   Request/response handling
  services/      Business logic
  middleware/    Auth, validation, error handling, logging
  app.ts         Express app setup
  server.ts      Starts the server
```

## Getting started

### Prerequisites

- Node.js LTS
- PostgreSQL (local, Docker, or a free Neon database) — from Week 2

### Setup

```bash
git clone https://github.com/githubnahid122/job-tracker-api.git
cd job-tracker-api
npm install
cp .env.example .env   # then fill in the values
npm run dev
```

The API runs at `http://localhost:3000`. Check `GET /health`.

## API endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| GET | `/health` | Health check |
| POST | `/api/v1/auth/register` | Create an account |
| POST | `/api/v1/auth/login` | Log in |
| POST | `/api/v1/auth/refresh` | Refresh the access token |
| POST | `/api/v1/auth/logout` | Log out |
| GET | `/api/v1/applications` | List applications (`?page=&limit=&status=&sort=`) |
| GET | `/api/v1/applications/:id` | Get one application |
| POST | `/api/v1/applications` | Create an application |
| PATCH | `/api/v1/applications/:id` | Update an application |
| DELETE | `/api/v1/applications/:id` | Delete an application |

### Error format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request body",
    "details": []
  }
}
```

## Roadmap

- **Month 1:** REST API, PostgreSQL, authentication, tests, deployment
- **Month 2:** Redis caching, background jobs, Docker, Next.js frontend, AI features
- **Month 4:** AI agent and MCP server built on top of this API

## License

MIT
