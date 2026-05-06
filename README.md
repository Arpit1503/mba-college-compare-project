# MBACompare

MBACompare is a responsive React application for comparing online MBA programs in India. It helps students review universities side by side across fees, accreditation, rankings, salary data, placement support, scholarships, EMI options, ROI, and best-fit recommendations.

Live demo: https://mba-compare.vercel.app

## Highlights

- Side-by-side comparison for two universities
- Searchable university directory
- Locked premium comparison flow with a lead form
- Session-based unlock experience after form submission
- Mobile-first UI built with Tailwind CSS
- Vercel-ready client routing and serverless API routes
- Optional local backend for lead capture and SMS notifications

## Tech Stack

- React 18
- Vite
- Tailwind CSS
- React Router
- Lucide React
- Vercel Serverless Functions
- Node.js local API server

## Project Structure

```text
mba-compare/
  api/                 Vercel serverless API routes
  backend/             Optional local Node API server
  src/
    assets/            Logos and static assets
    components/        Reusable UI components
    data/              University comparison data
    pages/             Route-level screens
  index.html
  package.json
  tailwind.config.js
  vercel.json
  vite.config.js
```

## Getting Started

Install dependencies:

```bash
npm install
```

Start the frontend:

```bash
npm run dev
```

The Vite app runs on `http://127.0.0.1:5173` by default.

## Local API

The project includes a local Node API server for development lead submissions.

Create a `.env` file from the example:

```bash
cp .env.example .env
```

Start the local API:

```bash
npm run api
```

The local API runs on `http://127.0.0.1:3002` by default. Vite proxies `/api` requests to this server during local development.

## Environment Variables

```env
API_PORT=3002
VITE_API_URL=http://127.0.0.1:3002
SMS_TO=+910000000000
```

`VITE_API_URL` is only needed for local development when calling a separate API server. In production, the app uses same-origin `/api` routes on Vercel.

`SMS_TO` is used by the optional local backend SMS workflow. Keep real phone numbers and credentials out of Git.

## Available Scripts

```bash
npm run dev      # Start Vite development server
npm run api      # Start the optional local Node API server
npm run build    # Build production assets
npm run preview  # Preview the production build locally
```

## API Routes

### `GET /api/health`

Returns a simple health payload.

```json
{ "ok": true }
```

### `POST /api/leads`

Accepts unlock-form submissions.

```json
{
  "name": "Student Name",
  "email": "student@example.com",
  "phone": "+919876543210"
}
```

On Vercel, submissions are validated and logged by the serverless function. For persistent lead storage, connect the endpoint to a database, CRM, webhook, or email/SMS provider.

## Deployment

This project is configured for Vercel.

```bash
npm run build
vercel --prod
```

`vercel.json` defines the Vite build settings and rewrites React Router pages back to `index.html` so direct visits to `/compare`, `/universities`, and `/unlock` work correctly.

## Data Notes

University data lives in `src/data/universities.js`. Review and update this file as fees, accreditations, rankings, placement data, and scholarship details change.

## License

This project is private unless you add a license file.
