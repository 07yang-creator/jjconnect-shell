# jjconnect-shell

Landing page and reverse-proxy shell for `jjconnect.online`.

This project is the umbrella that hosts the three-tool launcher at the apex domain and (eventually) proxies the underlying tools:

- `/jsmono` → JSmono (poster maker) — currently lives at `jjconnect.online`
- `/rakusat` → Rakusat / monopages — currently lives at `monos.jjconnect.online`
- `/diary` → Diary — not yet deployed

## Phase status (as of 2026-05-15)

- ✅ **Phase 1** — landing page scaffold (this commit). Deployed to a Vercel preview URL only; **no DNS changes**.
- ⏳ **Phase 2** — strip Auth0 from JSmono and monopages repos.
- ⏳ **Phase 3** — make each tool path-aware (so `/jsmono`, `/rakusat`, `/diary` proxies actually render correctly); add `rewrites` to this `vercel.json`; switch DNS for `jjconnect.online` to point here.
- ⏳ **Phase 4** — create diary repo, deploy, wire in.
- ⏳ **Phase 5** — redirect `monos.jjconnect.online` → `jjconnect.online/rakusat`; retire old domains.

## Local dev

This is a plain static site. Open `public/index.html` directly, or:

```bash
npx serve public
```

## Deploy

Vercel project setup:

- **Framework Preset:** Other
- **Build Command:** (leave empty)
- **Output Directory:** `public`
- **Install Command:** (leave empty)

No environment variables yet.

## Why the rewrites are not in this commit

Each underlying tool serves its static assets at root-relative paths (`/static/...`, `/api/...`). Proxying through `/rakusat/*` without first making monopages path-aware would result in broken asset loading. Phase 3 will add path-prefix awareness to each tool before flipping the rewrites on.
