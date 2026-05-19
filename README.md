# Import & Shipment Management System

Production-oriented desktop ERP foundation with an API-first Laravel backend and a Tauri React desktop frontend.

## Structure

- `backend/`: Laravel 11 API foundation, PostgreSQL, Sanctum, versioned API, repositories, services, DTOs, requests, resources, policies, and shared API responses.
- `frontend/`: React + TypeScript + Vite + Tauri desktop app, TailwindCSS, shadcn-style UI primitives, Zustand, React Query, React Router, Axios, React Hook Form, Zod, and TanStack Table foundation.
- `frontend/src/locales`: Arabic-first translation files powered by `i18next` and `react-i18next`.

## First Release Target

Desktop only through Tauri. The backend is client-agnostic and reusable for future Android and iOS apps built with React Native + Expo.

## Run Locally

Prerequisites:

- Node.js 20+
- Rust stable and Cargo for Tauri desktop builds
- PHP 8.2+
- Composer 2+
- PostgreSQL 16+

Optional PostgreSQL helper:

```bash
cp docker-compose.example.yml docker-compose.yml
docker compose up -d
```

Backend:

```bash
cd backend
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan db:seed
php artisan serve
```

Seeded login:

- Email: `adminashraf@erp.com`
- Password: `12345678`

Frontend:

```bash
cd frontend
npm install
cp .env.example .env
npm run desktop:dev
```

Validation commands:

```bash
cd frontend
npm run lint
npm run build
npm run desktop:build

cd ../backend
php artisan route:list
php artisan test
```

Products, recursive categories, and shipment management are implemented, including containers, document upload, automatic status updates, and shipment reporting.
