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
| GitHub (LivelyWalk org) | Source hosting, private repos, Teams, Projects v2 board | org settings | Unknown tier (Free/Team/Enterprise) | ❓ unconfirmed |
| Cloudflare Workers | Hosts `livewalk-marketplace-api` at `api.livelywalk.com` | `livewalk-marketplace-api/wrangler.toml`, `CLOUDFLARE_API_TOKEN` secret | Unknown tier | ❓ unconfirmed |
| Cloudflare Registrar | Owns the `livelywalk.com` domain | n/a (registrar account) | Annual registration fee, amount/renewal date unknown | ❓ unconfirmed |
| Neon (Postgres) | Database behind the API, via Cloudflare Hyperdrive | `wrangler.toml` `[[hyperdrive]]` binding | Hit a hard usage limit on 2026-11-10 that reset the next day — behavior consistent with a free/low tier, not confirmed | ❓ unconfirmed — **this already caused a real outage once, worth checking first** |
| LiveKit Cloud | Video/audio for live guide↔traveler sessions | `LIVEKIT_API_KEY` / `LIVEKIT_API_SECRET` secrets, `LIVEKIT_WS_URL` in app configs | Unknown tier; usage-based beyond free minutes | ❓ unconfirmed |
| Mapbox | Place search / map rendering in both apps | `MAPBOX_TOKEN_MOBILE`, `MAPBOX_TOKEN_WEB`, `VITE_MAPBOX_TOKEN` | Unknown tier | ❓ unconfirmed |
| Geoapify | Points-of-interest / route attraction lookups (replaced Overpass, TICKET-43) | `GEOAPIFY_API_KEY`, `livewalk-marketplace-api/src/places.js` | Unknown tier | ❓ unconfirmed |
| Expo EAS | Builds guide + traveler Android APKs (frequent — every test-build cycle) | `eas.json` in both app repos | Unknown tier — **high-frequency use, worth checking this isn't already past a free-tier cap** | ❓ unconfirmed |
| AssemblyAI | Speech-to-text for the voice-command-recognition epic (TICKET-47+) | Not yet wired into code — decision made 2026-11-11 | Arsham has an existing account/usage; plan tier not logged here yet | ❓ unconfirmed |

## Open questions for the account owner

- What plan is GitHub org billing on? (Free orgs can still use private repos + Teams up to a point, but confirm.)
- What plan/usage tier is Neon actually on — the usage-limit outage on 2026-11-10 suggests this needs attention regardless of logging.
- What plan is Cloudflare Workers on, and is Hyperdrive itself billed separately from the Worker?
- What plan is LiveKit Cloud on, and roughly how many session-minutes/month are we using?
- What plan is Expo EAS on — given how often builds are triggered in this project, confirm this isn't throttled or about to hit a cap.
- What AssemblyAI plan/account is being used for the voice epic, and what's the expected per-minute cost at anticipated usage?
- Domain renewal date and cost for `livelywalk.com`.

## History

- 2026-11-11: File created. Inventoried every third-party API key/token found across all three app repos' config; no dollar figures or plan tiers were available from code, so everything above is logged as unconfirmed pending the account owner's input.
