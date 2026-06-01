# Staybook 🏨

A guest-first web app for collecting hotel keycards and tracking your stays, loyalty progress, and world footprint across Marriott, Hilton, and Hyatt.

**Live:** https://staybook-myself.netlify.app

## Features

- 🗂️ **Keycard wallet** — collect cards by chain; upload real keycard photos or auto-generate brand-styled card faces
- 🏆 **Loyalty tracking** — qualifying nights and tier progress per program, computed automatically
- 🌍 **Unlock the Earth** — visualize the countries & cities you've stayed in, with an exportable share card
- 👤 **Guest-first** — browse instantly with no login; sign in (email or Google) to sync across devices
- ☁️ **Cloud sync** — cards, photos, and memberships stored per-user with row-level security

## Stack

- **Frontend** — a single `index.html` (vanilla HTML/CSS/JS, no build step)
- **Backend** — [Supabase](https://supabase.com) (Auth + Postgres + Storage)
- **Hosting** — [Netlify](https://netlify.com)

## Deploy / Update

Edit `index.html`, then:

```bash
# A — when GitHub is reachable (auto-deploys via Netlify)
git add . && git commit -m "…" && git push

# B — direct deploy (bypasses GitHub)
netlify deploy --prod --dir .
```

## Backend notes

- **Auth** — email/password (instant signup) + Google OAuth
- **Tables** — `profiles`, `cards`, `memberships`, all with Row-Level Security (each user sees only their own rows)
- **Storage** — `keycards` bucket for uploaded card photos
- **Keep-alive** — a daily `pg_cron` job writes to a `keepalive` table so the free-tier project never pauses

## Security

The repo ships only the Supabase **public anon key** and the **Google client ID** — both safe to expose. The Google client secret lives server-side in Supabase, never in the code. RLS protects all user data.

## Author

Built and maintained by [@klaywang24](https://github.com/klaywang24).

This is open infrastructure: a guest-first app shell, a Supabase auth / data / storage schema, and a hotel-brand & loyalty data model. If it's useful to your project / startup / team, fork it and make it yours.

If you add a hotel brand, a loyalty program, or a new card design, submit a PR.
