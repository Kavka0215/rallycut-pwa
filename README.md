# RallyCut AI — mobile PWA

Installable tennis rally auto-clip demo. Static site, no build step.

## Files
- `index.html` — the app (single file). **Edit this to change the app.**
- `manifest.webmanifest`, `sw.js`, `icons/` — PWA shell (installable, auto-updating).
- `vercel.json` — headers (no-cache service worker, manifest MIME).

## Deploy workflow (GitHub + Vercel)
- **Production** = the `main` branch. Push to `main` → Vercel auto-deploys to the stable URL.
- **Preview** = any other branch or PR → Vercel builds an independent preview URL.
- **Rollback** = Vercel dashboard → Deployments → pick an older one → "Promote to Production".

### Ship a change
```bash
git checkout -b change-x        # work on a branch → get a preview link
# edit index.html ...
git commit -am "describe change"
git push -u origin change-x     # Vercel comments a preview URL on the PR
# happy? merge to main → auto-deploys to production (stable URL unchanged)
```

## Update behaviour
`sw.js` is network-first for same-origin requests, so a new deploy shows up on
the next load — no stale app. The mp4box CDN (used only for large-file audio
extraction) is never cached and always loaded fresh.
