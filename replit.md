# Smart Attendance System

## Overview

A full-stack Smart Attendance System for college faculty to manage student attendance with face recognition support, timetable management, and downloadable reports.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod v3, `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (ESM bundle)
- **Frontend**: React + Vite + TailwindCSS + React Query
- **Auth**: Session-based (express-session + bcryptjs)

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── api-server/         # Express 5 API server
│   └── attendance-app/     # React + Vite frontend (routes at /)
├── lib/
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   └── db/                 # Drizzle ORM schema + DB connection
│       └── src/schema/
│           ├── faculty.ts
│           ├── students.ts
│           ├── timetable.ts
│           └── attendance.ts
├── scripts/
│   └── src/seed.ts         # Seed script for sample data
```

## Default Login

- Email: `admin@college.edu`
- Password: `faculty123`

## Features

1. **Faculty Login** — Session-based auth with bcrypt password hashing
2. **Student Management** — CRUD for students (name, register number, dept, year, section, photo)
3. **Timetable Management** — Weekly schedule by day/period/class
4. **Attendance Marking** — Manual attendance marking per class per date
5. **Live Camera Feed** — Simulated camera page for face recognition integration
6. **Reports & Export** — Attendance summary with CSV export, low attendance alerts (<75%)
7. **Dashboard** — Today's classes with attendance stats

## Database Schema

- `faculty` — id, name, email, password_hash, department
- `students` — id, name, register_number, department, year, section, photo_path
- `timetable` — id, day, time_slot, start_time, end_time, subject, faculty_name, department, year, section, room
- `attendance` — id, student_id, timetable_id, date, status (Present/Absent), marked_by

## API Endpoints

- `POST /api/auth/login` — Login
- `POST /api/auth/logout` — Logout
- `GET /api/auth/me` — Current user
- `GET/POST /api/students` — List/create students
- `GET/PUT/DELETE /api/students/:id` — Read/update/delete student
- `GET/POST /api/timetable` — List/create timetable entries
- `GET /api/timetable/current` — Active class right now
- `PUT/DELETE /api/timetable/:id` — Update/delete entry
- `GET/POST /api/attendance` — List/mark attendance
- `GET /api/attendance/summary` — Per-student attendance %
- `GET /api/attendance/today` — Today's class overview
- `GET /api/attendance/export` — Download CSV

## Running Seed

```bash
pnpm --filter @workspace/scripts run seed
```
