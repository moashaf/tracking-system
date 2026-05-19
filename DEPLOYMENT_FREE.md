# Free Trial Deployment

This project can be deployed for a small public trial using:

- Frontend: Vercel
- Backend: Koyeb
- Database: Supabase PostgreSQL

This setup is intended for testing with a small number of users. Free services can sleep, restart, or hit limits.

## 1. GitHub

Push the repository to GitHub without local secrets.

Do not commit these files:

- `backend/.env`
- `frontend/.env`
- `backend/vendor`
- `frontend/node_modules`
- `frontend/dist`

## 2. Supabase Database

Create a Supabase project, then copy the PostgreSQL connection details.

Use Supabase's direct database connection values if available:

- Host
- Port
- Database
- User
- Password

If Supabase gives you only a connection string, keep it for the backend variable `DB_URL`.

## 3. Backend on Koyeb

Create a new Koyeb service from the GitHub repository.

Recommended settings:

- Root directory: `backend`
- Build type: Dockerfile
- Dockerfile: `Dockerfile`
- Port: `8000`

Environment variables:

```env
APP_NAME="Import Shipment ERP"
APP_ENV=production
APP_KEY=
APP_DEBUG=false
APP_URL=https://YOUR-KOYEB-BACKEND-URL

APP_LOCALE=ar
APP_FALLBACK_LOCALE=en
APP_FAKER_LOCALE=en_US

LOG_CHANNEL=stderr
LOG_LEVEL=warning

DB_CONNECTION=pgsql
DB_URL=
DB_HOST=
DB_PORT=5432
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=

SESSION_DRIVER=cookie
SESSION_LIFETIME=120
SESSION_ENCRYPT=false
SESSION_PATH=/
SESSION_DOMAIN=null

CACHE_STORE=database
QUEUE_CONNECTION=database

SANCTUM_STATEFUL_DOMAINS=
CORS_ALLOWED_ORIGINS=https://YOUR-VERCEL-FRONTEND-URL
CORS_ALLOWED_ORIGINS_PATTERNS=
FRONTEND_URL=https://YOUR-VERCEL-FRONTEND-URL

RUN_MIGRATIONS=true
```

Generate `APP_KEY` locally from the backend folder:

```bash
php artisan key:generate --show
```

After the first successful deploy, you can change `RUN_MIGRATIONS` to `false` and run migrations manually when needed.

Health check URL:

```text
https://YOUR-KOYEB-BACKEND-URL/api/v1/health
```

## 4. Frontend on Vercel

Import the same GitHub repository into Vercel.

Recommended settings:

- Root directory: `frontend`
- Install command: `npm install`
- Build command: `npm run build`
- Output directory: `dist`

Environment variables:

```env
VITE_API_BASE_URL=https://YOUR-KOYEB-BACKEND-URL/api/v1
VITE_APP_NAME=Import Shipment ERP
```

After deploy, open the Vercel URL and test login and the main workflows.

## 5. Smoke Test

Check:

- Backend health endpoint returns success.
- Frontend loads without a blank page.
- Login works.
- Dashboard loads.
- Products, shipments, reports, users, and backups pages open.
- Create/update/delete actions work with expected permissions.

## Notes

- Free hosting is suitable for trials, not guaranteed production uptime.
- Supabase free projects have storage and usage limits.
- Koyeb free instances are small, so first load and heavy reports can be slow.
- For a real launch, move to a paid VPS or paid app platform before inviting many users.
