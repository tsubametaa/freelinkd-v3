# Freelinkd v3

>A Next.js 15 app (Turbopack) for the Freelinkd project — a small marketplace-style site that includes admin, UMKM, and user areas, forms, and a chatbot.

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

- Next.js 15 (Turbopack)
- React 19
- TypeScript
- Tailwind CSS
- dotenv for environment variable loading
- lucide-react for icons
- @datastax/astra-db-ts (Cassandra / Astra DB client)

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

## Linting / Type checking

TypeScript is configured. Run the TypeScript compiler or your editor's type checks. Example:

  npx tsc --noEmit

Tailwind is included; if you need to build CSS ensure your PostCSS/Tailwind config is set (project already contains `postcss.config.mjs` and Tailwind v4).

## Deployment

This is a standard Next.js app and can be deployed to Vercel, Netlify (with adapter), or any Node hosting that supports Next.js. With Vercel, simply connect the repository and set environment variables in the dashboard.

If you deploy to a server where you run `npm run build` and `npm run start`, ensure the environment variables are present in the runtime environment.

## Notes & gotchas

- Next version is `15.5.2` and expects modern Node and the new Turbopack; if you experience issues in dev mode, try removing `--turbopack` from the `dev` script to fall back to Webpack.
- Tailwind v4 may require a PostCSS toolchain compatible with your environment.
- Check API routes under `app/api/` for any required external services (Astra DB, Midtrans) and configure their credentials before testing features that depend on them.

## Contributing

1. Fork the repo
2. Create a feature branch
3. Make changes and add tests if applicable
4. Open a pull request

## License

Add your project's license here.

---

If you want, I can update the README with exact environment variable names by scanning `lib/` and `app/api/` files — would you like me to gather those now?

This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
