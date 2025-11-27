# Slotify – Smart Faculty Office Hours Booking System

A Django-based web application that simplifies scheduling and managing faculty office hours for educational institutions.

## Features
# Slotify – Smart Faculty Office Hours Booking System

Slotify is a Django application that streamlines how faculty publish office-hour availability and how students reserve time. It ships with polished dashboards, capacity-aware booking, analytics, and a clean Bootstrap UI—ready for campus pilots or further customization.

## ✨ Feature Highlights

| Audience | Capabilities |
| --- | --- |
| **Students** | Browse faculty directory, check capacity-aware availability, book/cancel slots with overlap protection, track upcoming visits. |
| **Faculty** | Create slots with capacity + locations, view attendee rosters, monitor fill rates, manage bookings from dashboards. |
| **Admins** | Review analytics (totals, peak hours, top faculty, recent activity), manage everything via Django Admin, prepare data for reporting. |

Additional safeguards include role-based access control, CSRF protection, booking race-condition prevention with database transactions, and clear feedback via Django's messages framework.

## 🧱 Architecture Overview

- **Framework**: Django 5 + Django templates with Bootstrap 5 styling.
- **Apps**:
  - `accounts` – custom `User` model with role helpers and authentication views.
  - `scheduling` – Slot & Booking models, capacity logic, student/faculty workflows.
  - `analytics` – aggregate queries for management dashboards.
- **Database**: SQLite for local development; compatible with MySQL/PostgreSQL (see `requirements.txt`).
- **Static/Templating**: Single `templates/` directory (after cleanup) plus `/static` for shared assets.

```
slotify/
├─ accounts/      # Custom user + auth views
├─ scheduling/    # Slots, bookings, dashboards
├─ analytics/     # Reporting endpoints
├─ templates/     # Base layout + feature pages
├─ static/        # CSS/JS/media (optional)
├─ requirements.txt
└─ manage.py
```

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- pip (comes with Python)
- PowerShell 5+ (Windows) or a shell of choice

### Quickstart

```powershell
cd "d:\Slotify – Smart Faculty Office Hours Booking System"
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser   # follow prompts
python manage.py runserver
```

Then visit:

- App: http://127.0.0.1:8000/
- Admin: http://127.0.0.1:8000/admin/

### Seeding Users

1. Log in to `/admin/` with your superuser.
2. Create faculty accounts (set role = `FACULTY`, optionally department).
3. Create student accounts (role = `STUDENT`).
4. Faculty can immediately create slots; students can browse and book.

### Typical Workflows

- **Faculty**: Dashboard → “Create Slot” → set time/location/capacity → monitor attendees via slot detail view.
- **Students**: “Browse Faculty” → choose professor → pick a slot with available capacity → review/cancel under “My Bookings”.
- **Admins**: Use `/analytics/` for KPIs and `/admin/` for full CRUD across users/slots/bookings.

## 🧪 Testing & Quality

Run the existing Django test suite (add your own as features grow):

```powershell
.\.venv\Scripts\python.exe manage.py test
```

## 📦 Configuration Notes

- Custom `User` model is defined in `accounts.models`; set `AUTH_USER_MODEL = "accounts.User"` (already configured).
- Templates directory has been consolidated under `/templates`—no `templetes/` duplicates remain.
- Static files are served from `/static`; adjust `STATICFILES_DIRS` or storage backends for production.

## 🌤️ Deployment Hints

- Use environment variables (`python-decouple` included) for secrets and database URLs.
- Suggested stack: Gunicorn + Nginx on AWS EC2, RDS for relational storage, S3 for static/media, ALB + Auto Scaling for resilience.
- `mysqlclient` is listed for MySQL connectivity; swap for `psycopg` if moving to PostgreSQL.

## 🧭 Roadmap Ideas

- Notifications (email/SMS) for booking confirmations
- Repeating slot templates and calendar UI
- Attendance tracking & exportable analytics (CSV/PDF)
- Optional React/Next.js front-end backed by the same API layer

## 📄 License

Educational / courseware codebase. Adapt freely for academic or internal pilots; add a commercial license if deploying broadly.
5. View/manage bookings at **My Bookings**
