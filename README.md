# Powerlife Inventory — Event POS System (Demo)

A self-contained, single-file Event POS + Inventory + Dashboard app. No build step, no backend — everything (React, Tailwind, Excel/CSV/PDF libraries) loads from CDN, and all data lives in-memory in the browser (resets on page reload).

This is a **demo / prototype**, intended for review and stakeholder testing before building the production version (Next.js + Supabase backend).

## What's inside

- **Inventory** — product catalog, smart Excel/CSV import (fuzzy header matching), stock adjustments with history, event stock allocation, promotions, export (Excel/CSV/PDF).
- **POS** — checkout flow (event/customer/sales person/payment method, cart, promotions, giveaways), Order History with edit/delete (single, bulk, with or without stock restock).
- **Dashboard** — KPIs, sales trend chart, top products, sales-person leaderboard, payment-method and promotion analytics, low-stock alerts, editable Recent Orders.
- **Settings** — manage Events, Sales People, and Payment Methods (add/edit/delete).

Login is gated by a fixed set of accounts (see `DEMO_USERS` near the top of the script). Credentials are not shown on the login screen — share them with your team out of band, not through this file.

## Files

- `index.html` — the entire app. This is the file GitHub Pages will serve.
- `inventory-app.html` — identical copy, kept as the working filename from development.
- `smoketest.js` — headless regression test suite (Node + jsdom) covering every major flow. Not needed for deployment; useful if you continue developing this file and want to catch regressions.

## Deploy to GitHub Pages

1. **Create a new repository** on GitHub (e.g. `powerlife-inventory`). Do not initialize it with a README (you already have one here).

2. **Push these files** from this folder:

   ```bash
   cd path/to/this/folder
   git init
   git add index.html README.md
   git commit -m "Initial commit: Powerlife Inventory demo"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```

   (Optionally also commit `inventory-app.html` and `smoketest.js` if you want the test suite in the repo — they aren't required for the site to work.)

3. **Enable Pages**: on GitHub, go to your repo → **Settings** → **Pages** → under "Build and deployment", set **Source** to "Deploy from a branch", branch `main`, folder `/ (root)` → **Save**.

4. Wait a minute or two, then your app will be live at:

   ```
   https://<your-username>.github.io/<your-repo>/
   ```

## Notes before sharing widely

- **Data does not persist.** Every reload resets to the seeded demo data (3,000 products, ~200 historical orders). This is expected for the demo phase — a real backend (Supabase/Postgres) is the next step for persistence, multi-user sync, and real auth.
- **Login is a front-end gate, not real authentication.** The username/password check happens in the browser, and the source code (including `index.html`) is publicly visible in the repo — anyone who reads the code can find the credentials. It's good enough to keep casual visitors out, but not to protect sensitive data. Treat the seeded data as non-confidential, and don't put real customer or payment info into this demo.
- If you want a real deployment (persistent data, real accounts, concurrent users), the next step is rebuilding this on the production stack (Next.js + TypeScript + Supabase/PostgreSQL) using this demo as the functional spec.
