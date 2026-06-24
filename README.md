# High Court of the Maldives — Backlog Balancing Engine

A self-contained web app that allocates the backlog cohort (cases registered **2021 and earlier**) across the court's sections (B1–B11) according to a fixed, auditable methodology, then shows the case-by-case results.

It is a **single static page** — no build step, no server. Open `index.html` in any modern browser, or host it anywhere static.

---

## Deploy

**GitHub Pages (free):**
1. Push this repo to GitHub.
2. **Settings → Pages → Source: Deploy from a branch → `main` / `root` → Save.**
3. Your URL appears in about a minute. `index.html` at the root is served automatically.

**Vercel:**
1. At [vercel.com](https://vercel.com) → **Add New → Project → Import** this repo → **Deploy.**
2. Every push afterwards redeploys automatically.

Any other static host (Netlify, Cloudflare Pages) works the same way.

---

## What it does

The allocation engine applies four rules, in order:

1. **Annual cap (absolute).** Cap per section = cases ÷ active sections, per registration-year. A hard ceiling that overrides continuity — no section is ever loaded above it.
2. **Recusal (hard exclusion).** A section flagged as conflicted for a case is never assigned that case.
3. **Type rotation (selector).** Among eligible sections, the one holding the fewest cases of that class/type wins — so no section gets a second case of a type until every eligible section has one.
4. **Bench continuity (tiebreaker).** When type-counts are level, the presiding section is preferred, then a prior bench member.

Significantly-progressed (P1) cases stay with their presiding section *while that section is under cap*. A case that fits no eligible section is surfaced as **unassignable** rather than force-placed.

---

## Features

- **Allocation** tab — per-year caps, the section × year matrix, and unassignable cases.
- **Results** tab — every case grouped under the section it was assigned to, with the rule that placed it.
- **Cases / Justices & Sections / Users & Roles / Settings** — full admin CRUD; editable class/type list that grows as you add new types.
- **Save** — data auto-saves to the browser (persists across reloads once hosted).
- **Export / Import** — download or load the full state as a JSON file.
- **Share link** — a URL that carries a snapshot of the current data.
- **Print / PDF** — a clean report of the matrix and per-section assignments.

---

## Important notes (please read before using real data)

- **This is a pilot, not the system of record.** Data is stored **per browser/device** — it is *not* one shared court-wide database. Two people opening the same URL each have their own separate data.
- **The roles are a faithful model, not server-enforced security.** On a public URL, anyone with the link has admin access. Do not place live case data here.
- **If the data could ever be real, make the GitHub repo private.** A public repo exposes the committed contents to anyone.
- The seeded data is illustrative sample data only.

A shared, multi-user version — one database, real server-enforced login, and an audit log — is the intended next step. The data model and permission map in this app are built to port directly onto it.
