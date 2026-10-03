# Base44 Dev Environment

## Project Overview
Next.js 16 (App Router, Turbopack) + React 19.2 + React Compiler + Tailwind CSS 4.
Originally a Netlify Platform Starter — uses @netlify/blobs and Netlify edge functions.

## Setup
- `docker compose -f docker-compose.base44.yml up -d` starts the dev server on port 3000.
- Node 22 base image; source is bind-mounted at `/app`; `node_modules` and `.next` are anonymous volumes to avoid host conflicts.
- Dependencies install on container startup via `npm install` (no lockfile-frozen flag — lockfile may not match the sandbox platform).

## Key Fixes Applied for Base44 Preview
1. **middleware.js** — `X-Frame-Options: DENY` was set unconditionally, blocking the preview iframe. Now only set when `process.env.NODE_ENV === 'production'`.
2. **next.config.js** — Added `allowedDevOrigins` using `BASE44_PUBLIC_HOST_SUFFIX` so Next.js accepts the preview origin for dev assets/HMR.

## Notes
- The `/blobs` page uses `@netlify/blobs` which requires Netlify infrastructure; it will not work in local dev without `netlify dev`. The home page and most other routes work fine with plain `next dev`.
- Middleware deprecation warning ("use proxy instead") is expected in Next.js 16 and non-blocking.
- No external secrets required to boot.
