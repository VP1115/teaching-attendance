# TeachingTracker

`HTML/JS` | `Supabase (PostgreSQL)` | `Vercel` | `offline-first`

A full-stack web app for managing student batches, tracking attendance class-by-class, and monitoring fee collection. Built as a single HTML file with a Supabase backend, deployed on Vercel.

**Live demo:** [teaching-attendance.vercel.app](https://teaching-attendance.vercel.app)

---

## What it does

TeachingTracker lets a teacher manage multiple student batches, each with its own schedule, fee structure, and roster. For each batch, attendance is recorded per student on a monthly calendar. The app works offline using localStorage and automatically syncs to Supabase when a connection is available.

---

## Key features

- **Batch management** — create and edit batches with schedule (days of week, time, duration, grade levels) and fee type (flat monthly or per-class)
- **Student roster** — add students with name and parent contact per batch
- **Monthly attendance calendar** — mark each student as present / absent / recording / alternate for every scheduled class date
- **Extra and cancelled classes** — add ad-hoc extra sessions; mark any scheduled date as cancelled
- **Fee tracking** — per-student fee payment records with date-paid fields; per-class fees are calculated automatically from attendance
- **Stats dashboard** — summary cards showing total students, attendance percentage, and fee status across all batches
- **CSV export** — export attendance and student data per batch
- **Offline-first sync** — reads from localStorage when Supabase is unreachable; pushes local-only changes to the cloud on reconnect
- **Responsive design** — works on desktop and mobile

---

## Tech stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML, CSS, JavaScript (single file) |
| Backend / database | Supabase (PostgreSQL) |
| Hosting | Vercel (static) |

---

## How it works

The entire application is one HTML file served as a static asset by Vercel. On load, it probes Supabase for connectivity. If reachable, it loads from the database and updates the local cache. If offline, it falls back to localStorage. On reconnect, any local-only changes are pushed to the cloud.

All state is held in in-memory caches (`batchesCache`, `studentsCache`, `attendanceCache`) and written to both localStorage and Supabase on every change.

---

## Setup

To run your own instance:

1. Create a Supabase project and note your project URL and anon key.
2. Create the required tables (batches, students, attendance, cancelled classes, fee records) using the Supabase dashboard or SQL editor.
3. Replace the Supabase URL and anon key in `teaching_attendance_complete.html`.
4. Push to a GitHub repo and deploy via Vercel — the `vercel.json` config is already included.

To run locally (offline-only, no Supabase):
```bash
open teaching_attendance_complete.html
# or just drag the file into a browser
```

---

## Status

Live at [teaching-attendance.vercel.app](https://teaching-attendance.vercel.app). Personal tool in active use.
