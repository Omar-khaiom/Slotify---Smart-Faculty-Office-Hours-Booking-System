# Slotify – Smart Faculty Office Hours Booking System

A Django-based web application for scheduling and managing faculty office hours.

## Features

**Students** – Browse faculty, check availability, book slots with overlap protection, manage bookings.

**Faculty** – Create office-hour slots, set capacity & location, monitor attendance, view rosters.

**Admins** – Analytics dashboard, user management via Django Admin, system oversight.

Security includes role-based access control, CSRF protection, transactional booking logic, and session management.

## Architecture

- **Framework**: Django 5 + Bootstrap 5
- **Apps**: `accounts` (user auth), `scheduling` (slots & bookings), `analytics` (reporting)
- **Database**: SQLite (dev) / MySQL, PostgreSQL (production)
- **Frontend**: Django templates with premium CSS theme

## Quick Start

**Prerequisites**: Python 3.10+, pip, PowerShell 5+ (or bash)

```powershell
cd "d:\Slotify – Smart Faculty Office Hours Booking System"
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Visit:
- App: http://127.0.0.1:8000/
- Admin: http://127.0.0.1:8000/admin/

## 🛠️ Step-by-Step Local Setup

### 1. Create and activate a virtual environment (PowerShell)

```powershell
cd "d:\Slotify – Smart Faculty Office Hours Booking System"
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If `python` fails, confirm Python 3.10+ is installed and available in your PATH.

### 2. Install Python dependencies

```powershell
pip install -r requirements.txt
```

### 3. Apply database migrations

```powershell
python manage.py migrate
```

If you see `no such table: accounts_user`, re-run the migrations with the virtual environment active.

### 4. Create an admin (superuser) account

```powershell
python manage.py createsuperuser
```

Follow the prompts to set a username, email (optional), and password. This account can access both the admin site and internal dashboards.

### 5. Start the development server

```powershell
python manage.py runserver
```

Visit the application at `http://127.0.0.1:8000/` and the admin at `http://127.0.0.1:8000/admin/`.

### 6. Create faculty and student accounts

1. Sign in to `/admin/` with the superuser you just created.
2. Navigate to **Users** under the **Accounts** section.
3. Add a new user and assign credentials.
4. Set the `role` field to `FACULTY` or `STUDENT` as needed.
5. Save the user; repeat for each account required.

Faculty accounts can immediately create office-hour slots from their dashboard; students can browse and book available slots.

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

## 🆘 Troubleshooting & Help

- **`python` or `pip` not recognized**: Re-open PowerShell, ensure Python 3.10+ is installed, and re-run `python -m venv .venv` so Windows updates PATH for the session.
- **`pip install mysqlclient` fails**: Install the *Microsoft Build Tools for Visual Studio* or switch to a pure-Python driver (e.g., `pip install pymysql`) and update `DATABASES` accordingly.
- **`django.db.utils.OperationalError: no such table`**: Your migrations did not run; activate the virtual environment and execute `python manage.py migrate` again.
- **Port 8000 already in use**: Stop other Django instances or run `python manage.py runserver 0.0.0.0:8001` to use a different port.
- **Unable to log in**: Double-check username/password, confirm the account is active, and verify the `role` is correctly set to `FACULTY` or `STUDENT` for dashboard access.
- **Superuser forgotten**: Create a new one by running `python manage.py createsuperuser` while the server is stopped.
- **CSRF verification failed**: Clear cookies or ensure you are accessing the site via `http://127.0.0.1:8000/` and not mixing localhost domains.
