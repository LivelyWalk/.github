# External services and costs

Every third-party service LivelyWalk pays for or could incur usage charges
on, in one place. This file is the source of truth for "what are we running,
and on whose dime."

**Rule: any new paid service, API, or hosting provider added to any repo
must be logged here in the same change that adds it** — update this table
and the "Open questions" section (if the plan/cost isn't yet confirmed)
before merging. Confirmed cost info, including actual plan tiers and
monthly figures, is intentionally not written here from guesses — use the
`✅`/`❓` status to tell confirmed facts from agent-inferred guesses, and ask
the account owner rather than assume.

## Active services

| Service | Used for | Where configured | Plan / cost | Status |
|---|---|---|---|---|
| GitHub (LivelyWalk org) | Source hosting, private repos, Teams, Projects v2 board | org settings | Free plan | ✅ confirmed |
| Cloudflare Workers | Hosts `livewalk-marketplace-api` at `api.livelywalk.com` | `livewalk-marketplace-api/wrangler.toml`, `CLOUDFLARE_API_TOKEN` secret | Free plan | ✅ confirmed |
| Cloudflare Registrar | Owns the `livelywalk.com` domain | n/a (registrar account) | ~€11, believed to be the annual renewal (seen on last invoice; billing cadence not separately verified) | ✅ confirmed (cadence: best guess) |
| Neon (Postgres) | Database behind the API, via Cloudflare Hyperdrive | `wrangler.toml` `[[hyperdrive]]` binding | Free plan — **this is why it hit a hard usage limit and caused a real outage on 2026-11-10**; expected behavior on this tier, not a bug. Worth an upgrade if it recurs. | ✅ confirmed |
| LiveKit Cloud | Video/audio for live guide↔traveler sessions | `LIVEKIT_API_KEY` / `LIVEKIT_API_SECRET` secrets, `LIVEKIT_WS_URL` in app configs | Free plan | ✅ confirmed |
| Mapbox | Place search / map rendering in both apps | `MAPBOX_TOKEN_MOBILE`, `MAPBOX_TOKEN_WEB`, `VITE_MAPBOX_TOKEN` | Free plan | ✅ confirmed |
| Geoapify | Points-of-interest / route attraction lookups (replaced Overpass, TICKET-43) | `GEOAPIFY_API_KEY`, `livewalk-marketplace-api/src/places.js` | Free plan | ✅ confirmed |
| Expo EAS | Builds guide + traveler Android APKs (frequent — every test-build cycle) | `eas.json` in both app repos | Starter plan, $19/month | ✅ confirmed |
| AssemblyAI | Speech-to-text for the voice-command-recognition epic (TICKET-47+), provider decided 2026-11-11 | Not yet wired into code | **Not configured yet** — no account/plan set up; needs doing before TICKET-48 implementation starts | ✅ confirmed (as: not set up) |

## Open questions for the account owner

- Confirm the €11 Cloudflare Registrar charge is actually annual (not some other cadence) next time it's convenient to check.
- AssemblyAI plan/account still needs to be set up for real before the voice epic's implementation tickets (TICKET-48+) can use it live.

## History

- 2026-11-11: File created, every service inventoried as unconfirmed.
- 2026-11-11: Account owner confirmed plan/cost for every service. All on free tiers except Expo EAS (Starter, $19/mo) and the Cloudflare-registered domain (~€11, believed annual). AssemblyAI confirmed not yet configured.
