# Freelinkd v3

> A Next.js 15 (App Router) application for the Freelinkd marketplace platform. It provides:

- Public site pages (landing, services, portfolio)
- User areas for freelancers and UMKM (registration, dashboards)
- Admin area for content, user management and chatbot data uploads
- API routes for forms, payments and chatbot operations

This README documents how to run, develop, and deploy the project, the key architecture, exact dependencies used, and required environment variables.

## Quick start

Requirements

- Node.js 18+ (recommended)
- npm or yarn

Install

1. Clone the repo

   git clone <repo-url>
   cd freelinkd-v3

2. Install dependencies

   npm install

3. Create environment variables

   Create a `.env.local` file in the project root and add the variables described in the "Environment variables" section below.

4. Run the dev server

   npm run dev

The app will be available at http://localhost:3000 by default.

## Scripts

Available npm scripts (from `package.json`):

- `npm run dev` — Starts Next.js in development mode using Turbopack.
- `npm run build` — Builds the app for production (Turbopack enabled).
- `npm run start` — Starts the production server after building.

## Technologies

The project uses the following main technologies and libraries (exact versions are in `package.json`):

- Next.js 15 (App Router, Turbopack enabled)
- React 19
- TypeScript 5
- Tailwind CSS 4 (with `@tailwindcss/postcss`)
- dotenv — load environment variables from `.env` files
- lucide-react — icon components
- @datastax/astra-db-ts — Astra DB / Cassandra client used by chatbot and data storage

For full dependency list and versions see `package.json` (we also include a summary below).

## Project structure (important paths)

- `app/` — Next.js App Router pages, components and API routes.

  - `app/page.tsx` — Root page
  - `app/layout.tsx` — Root layout
  - `app/api/` — Server routes (authentication, forms, payment, chatbot)
  - `app/components/` — UI components (navbar, footer, admin/user/umkm specific components)
  - `app/site/` — site-level pages including admin and dashboard pages

- `lib/` — small helpers and services (auth, db, form, midtrans, chatbot helper)
- `services/` — higher-level UI services (hire, join)
- `public/` — static assets
- `app/types/` — TypeScript types used by the app

## Environment variables

This project uses `dotenv`. Create `.env.local` (gitignored) in the project root and add any of the variables used by `lib/*` and `app/api/*`. Common variables you may need:

- `NEXT_PUBLIC_BASE_URL` — (optional) public URL for the app
- `DATABASE_URL` or Cassandra/Astra-specific variables used by `@datastax/astra-db-ts` (see your Astra DB config)
- `MIDTRANS_SERVER_KEY` / `MIDTRANS_CLIENT_KEY` — if using Midtrans payment integration in `lib/midtrans.ts`
- Any auth-related secrets (JWT_SECRET, NEXTAUTH_SECRET, etc.) depending on how `lib/auth.ts` is implemented

If you open the files under `lib/` and `app/api/` you will see exact variable names required; add them to `.env.local` accordingly.

### Example `.env.local`

Copy this into `.env.local` and replace the placeholders with real values:

````
# App
NEXT_PUBLIC_BASE_URL=http://localhost:3000

# AstraDB (used by chatbot and some data collections)
ASTRA_DB_TOKEN=your_astra_db_token
ASTRA_DB_ENDPOINT=https://<your-astra-endpoint>.apps.datastax.com

# Midtrans (optional, if payment integration is used)
MIDTRANS_SERVER_KEY=your_midtrans_server_key
MIDTRANS_CLIENT_KEY=your_midtrans_client_key

# Freelinkd v3

Professional marketplace platform built with Next.js (App Router).

Freelinkd connects freelancers and UMKM with a lightweight marketplace and administrative tools. The application includes:

- Public marketing pages (landing, services, portfolio)
- User portals for freelancers and UMKM (registration, profiles, dashboards)
- Admin panel (content management, user management, chatbot data uploads)
- Server routes for forms, payments, and chatbot operations

This document explains how to set up, run, develop, and deploy the project, lists core dependencies, and documents required environment variables.

---

## Table of contents

- [Quick start](#quick-start)
- [Scripts](#scripts)
- [Technologies & dependencies](#technologies--dependencies)
- [Project structure](#project-structure)
- [Environment variables](#environment-variables)
- [Development notes](#development-notes)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [Team](#team)
- [License](#license)

---

## Quick start

Requirements

- Node.js 18+ (recommended)
- npm, yarn, pnpm, or bun

Install

1. Clone the repository

```bash
git clone <repo-url>
cd freelinkd-v3
````

2. Install dependencies

```bash
npm install
```

3. Create environment variables

Create a `.env.local` file in the project root and add values as shown in the [Environment variables](#environment-variables) section.

4. Start development server

```bash
npm run dev
```

Visit http://localhost:3000

---

## Scripts

Key npm scripts (defined in `package.json`):

- `npm run dev` — start development server (Turbopack)
- `npm run build` — build for production
- `npm run start` — run production server (after build)

---

## Technologies & dependencies

Primary packages (from `package.json`):

- `next@15.5.2` — React framework (App Router + Turbopack)
- `react@19.1.0`, `react-dom@19.1.0` — UI rendering
- `typescript@^5` — static types
- `tailwindcss@^4`, `@tailwindcss/postcss@^4` — utility CSS + PostCSS
- `dotenv@^17.2.2` — environment variable loader
- `lucide-react@^0.543.0` — icon components
- `@datastax/astra-db-ts@^2.0.2` — Astra DB client for chatbot / data storage

Dev / type dependencies:

- `@types/node`, `@types/react`, `@types/react-dom` — TypeScript definitions

Note: consult `package.json` for the definitive dependency list and versions.

---

## Project structure

High-level layout and important files:

- `app/` — App Router pages, layouts, components, and API routes
  - `app/layout.tsx`, `app/page.tsx` — global layout and root page
  - `app/api/` — server endpoints (auth, forms, payments, chatbot)
  - `app/components/` — shared UI components
  - `app/site/` — site-specific pages (admin, dashboard, etc.)
- `lib/` — helper modules (auth, db, midtrans, chatbot utilities)
- `services/` — page-level service helpers (hire, join)
- `public/` — static assets
- `app/types/` — TypeScript types used across the app

This layout helps locate code when adding features or debugging.

---

## Environment variables

Local secrets should be placed in `.env.local` at the project root. Only variables prefixed with `NEXT_PUBLIC_` are exposed to the browser.

Example `.env.local` (replace placeholders):

```env
# App
NEXT_PUBLIC_BASE_URL=http://localhost:3000

# AstraDB (used by chatbot and some collections)
ASTRA_DB_TOKEN=your_astra_db_token
ASTRA_DB_ENDPOINT=https://<your-astra-endpoint>.apps.datastax.com

# Midtrans (optional)
MIDTRANS_SERVER_KEY=your_midtrans_server_key
MIDTRANS_CLIENT_KEY=your_midtrans_client_key

# Auth / JWT
JWT_SECRET=supersecretjwt
NEXTAUTH_SECRET=anothersecret

# Optional DB connection
DATABASE_URL=your_database_connection_string
```

Tip: keep server-only secrets out of version control. Use deployment platform secret settings for production.

---

## Development notes

- Type checking: `npx tsc --noEmit`
- Editor: use TypeScript-aware tooling for best DX
- Tailwind: config and PostCSS files are present (`postcss.config.mjs`)
- If the project integrates with external services (Astra DB, Midtrans), ensure credentials are set before exercising those flows

---

## Deployment

Recommended: Vercel (native Next.js support). Steps:

1. Connect repository to Vercel
2. Set environment variables in project settings
3. Vercel will run `npm run build` and deploy automatically

Alternative (self-hosted):

```powershell
npm ci --production; npm run build; npm run start
```

Ensure runtime environment variables are configured on your host.

---

## Contributing

Contributions are welcome. Suggested workflow:

1. Fork the repository and create a feature branch
2. Run the dev server and implement changes
3. Add tests for new features when applicable
4. Open a pull request with a clear description

If you'd like, I can generate a `CONTRIBUTORS.md` file from git history.

---

## Team

Project maintainers:

- Alvin Putra — Developer (https://github.com/tsubametaa)
- Alif Fahmi — CTO (https://github.com/aliffahmi1207)

---

## License

Specify the project license (e.g., `MIT`). If desired, I can add an `LICENSE` file.
