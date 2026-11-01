# Matchday Lab ⚽

A lightweight, mobile-friendly football app created as a father-and-son coding project.

**No build step, npm packages, hosting subscription, server or API key is required.** The entire app runs as a static website, ideal for **GitHub Pages**.

## Features

- **Match centre:** live Premier League fixtures, scores, match events, statistics and a Bundesliga option.
- **Head-to-head history:** up to 10 previous meetings where source results are available.
- **Dad vs Son predictions:** predict a score and earn points. Saved **in this browser on this device**.
- **Premier League season predictor:** actual standings, forecast final table and a matchweek-by-matchweek timeline.
- **Monte Carlo simulator:** run 1,000, 5,000 or 10,000 possible finishes and explore title, top-four, top-N and relegation probabilities for every team.
- **Install on a phone:** home-screen icon, standalone display and an offline app shell. Live football data still needs an internet connection.

## Publish on GitHub Pages — no terminal required

1. Log in to [GitHub](https://github.com/) and choose **New repository**.
2. Name it **`matchday-lab`** (or your preferred name). For GitHub Free hosting, set visibility to **Public**. Do not publish passwords, API keys or personal information.
3. Download the repository ZIP supplied with this project and **extract it** on your computer. GitHub does *not* unzip archives you upload.
4. In the new GitHub repository, select **Add file → Upload files**. Upload the **contents** of the extracted folder, preserving the `icons` folder and `index.html` at repository root. Commit directly to the `main` branch.
5. Open **Settings → Pages**. Under **Build and deployment**, select **Deploy from a branch**, **`main`**, **`/(root)`**, then **Save**.
6. After publishing, use the address shown by GitHub. For a standard project repository this is:

   `https://YOUR-GITHUB-USERNAME.github.io/matchday-lab/`

   Replace both the username and repository name to match yours. The final site URL is shown under **Settings → Pages**.

7. Open that HTTPS address. Try **Demo** in the Match centre; then open **Premier League predictor** and refresh the live data. External sports endpoints can be unavailable or delayed.

To update the website later, edit or replace `index.html` in the repository. Pushing to the published branch triggers a new GitHub Pages deployment. If the new interface doesn't appear straight away, close/reopen the app or refresh the page. If you change offline shell assets, increment the cache version in `sw.js`.

### Important upload tip

Upload the extracted files, **not the ZIP file itself**. Make sure the files are placed in the repository **root** (not inside an extra `matchday-lab-github-pages` folder). The project root must contain `index.html` and `sw.js`.

## Use on an iPhone

1. Open the deployed **HTTPS** address in **Safari**.
2. Tap **Share → Add to Home Screen** (on some iOS versions, choose **More** or **Add to Home Screen** from the Share sheet).
3. The app appears on the Home Screen with the Matchday Lab icon. It can open in a standalone web-app window.

The service worker caches the app interface for occasional offline use, but **does not cache external score data**. The season page may show a labelled *cached* snapshot if an API is unavailable. Match predictions are saved in local browser storage and do **not** synchronize across phones or browsers. iOS can remove website data to save space, so don't treat local predictions as a permanent backup.

## Run locally before publishing

Either open `index.html` directly to test **Demo mode**, or serve the folder on localhost to exercise the installable experience:

```bash
python -m http.server 8000
```

Visit `http://localhost:8000/`. When opening the file directly (`file://`), browser security rules may block some network requests and service workers.

## External data and caveats

| Source | Purpose | Notes |
| --- | --- | --- |
| ESPN (unofficial public endpoints) | Premier League scoreboard, results and standings | Not guaranteed stable; can change, be rate-limited or block browser CORS requests. |
| [OpenFootball](https://github.com/openfootball/football.json) | Historical football matches and backup season data | Public CC0 dataset; updates may lag and some seasons/fixtures may be missing. |
| [OpenLigaDB](https://www.openligadb.de/) | Bundesliga fixtures and historical results | Community maintained; licence/attribution details at [OpenLigaDB](https://www.openligadb.de/lizenz). |

**The site's hosting does not make third-party APIs more reliable or bypass cross-origin (CORS) restrictions.** If an endpoint refuses browser requests, a stable production version needs a permitted server-side proxy/edge function or a different licensed feed. GitHub Pages itself cannot execute a proxy.

This project has no server, paid credentials or personal account login. Public GitHub Pages is viewable by anyone. Do not add private API tokens to JavaScript, HTML, repository files or GitHub Pages settings expecting them to be hidden.

Monte Carlo projections are estimates, not betting advice. The top-N European-finish probability is a **league-position proxy**; actual European qualification depends on competition rules and cup results.

## File layout

```text
matchday-lab/
├── index.html              # Complete football app (Version 5)
├── manifest.webmanifest    # Installable app metadata
├── sw.js                   # Offline app shell; live API requests always network-only
├── favicon.svg             # Browser tab icon
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   └── apple-touch-icon.png
├── .nojekyll               # Disable Jekyll processing on Pages
├── .gitignore
└── README.md               # This guide
```

## Ideas to vibe code next

- Save a weekly snapshot of title probabilities and draw a changing-odds chart.
- Add a player goalscorer predictor.
- Build a persistent Dad vs Son leaderboard (with a backend if it should sync across devices).
- Add a user-selectable favourite club and a league fixtures calendar.

## Licensing

Football datasets and provider APIs remain subject to their own terms. No third-party logos or images are bundled in this repository; team badges may be loaded from external sources at runtime. Choose a repository licence if you want to offer the app code for reuse under specific terms.
