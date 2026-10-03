# Base44 Dev Environment

## Project Overview
Next.js 16 (App Router) + Tailwind CSS v4. Originally a Netlify platform starter.

## Running the App
```bash
docker compose -f docker-compose.base44.yml up -d --build
```
The app is served on port 3000 by `next dev` (live-reload dev server, bind-mounted source).

## Key Notes
- **No external credentials needed.** The app runs entirely on local source.
- **Netlify Blobs** (`@netlify/blobs`): The blobs feature (`/blobs` page) only activates when `process.env.CONTEXT` is set (a Netlify environment variable). In local dev it is unset, so the blob editor is hidden — this is expected, not a bug.
- **`allowedDevOrigins`** is set in `next.config.js` using `BASE44_PUBLIC_HOST_SUFFIX` so the preview origin can access Next.js dev assets/HMR.
- **Healthcheck**: uses `node -e fetch(...)` (no curl in node:22-slim).
- **Dependencies**: `npm install` runs on container startup (node_modules in a named volume to avoid host overwrite).
