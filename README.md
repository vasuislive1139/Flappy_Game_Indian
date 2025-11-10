# Flappy — Custom (PWA-ready)

Files:
- `index.html` — the Flappy game (supports uploading sprite PNG and background/death sounds).
- `manifest.json` — PWA manifest.
- `sw.js` — simple service worker providing basic offline fallback.
- `icons/` — placeholder folder (you should supply 192x192 and 512x512 icons if you want a nicer install icon).

## Quick: make it an installable web app (PWA)
1. Host the folder on any static hosting (GitHub Pages, Netlify, Vercel, Firebase Hosting, S3 + CloudFront).
2. Ensure `manifest.json` and `sw.js` are served from the web root.
3. Open the site in Chrome/Edge on Android or modern desktop browsers — you will see "Install app" or browser menu -> "Install".
4. The site will be installable. The uploaded assets are local to the browser (File API) — they won't persist after closing unless manually reloaded by the user (consider adding file persistence via IndexedDB if needed).

## Make a downloadable Android APK (two simple ways)

### A) PWABuilder (easiest, no local tooling)
1. Go to https://pwabuilder.com and enter your hosted URL.
2. Follow steps to generate an Android package (it uses Trusted Web Activity).
3. Download the generated APK / App Bundle and distribute the link.

### B) Bubblewrap CLI (recommended for more control)
1. Install Node.js and Java (JDK 11+).
2. `npm install -g @bubblewrap/cli`
3. `bubblewrap init --manifest=https://your-site/manifest.json`
4. `bubblewrap build` -> this creates a TWA project. Open with Android Studio, sign the app and produce an APK/AAB.

## Make native apps via Capacitor (more native features)
1. Install Node.js.
2. `npm init` and put `index.html` and assets in the `www/` folder.
3. `npm i @capacitor/cli @capacitor/core`
4. `npx cap init`
5. `npx cap add android` (and/or `ios`)
6. Open Android Studio / Xcode to build, sign, and export.

## Host suggestions
- GitHub Pages — free and simple for static sites.
- Netlify — drag & drop folder or connect repo.
- Vercel — connect repo, deploy.
- Firebase Hosting — fast and supports PWAs well.

## Notes about assets & permissions
- Audio/video playback is subject to browser autoplay policy — user gesture required.
- Files uploaded via the page are not uploaded to the server — they stay in the page's memory. If you need persistence across sessions, store them in IndexedDB or upload to a server.
- Replace icons in `icons/` for a polished install icon.

## Need help?
Tell me:
- Where do you want to host (GitHub Pages / Netlify / other)?
- Do you want me to produce a ready-to-download APK (I can give step-by-step commands for Bubblewrap or a Capacitor project)?
