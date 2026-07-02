# vibecreative-dev.github.io

Personal landing page for Nurzhan — a links hub and a list of apps/projects, hosted on GitHub Pages.

**Live site:** https://vibecreative-dev.github.io/

---

## What this repo contains

| File | Purpose |
|------|---------|
| `index.html` | The landing page (hero, links, apps grid, footer). |
| `styles.css` | All styling — dark theme, gradient background, hover animations, responsive grid. |
| `app-ads.txt` | Google AdMob authorized-sellers file (required for showing ads in the app). |
| `.nojekyll` | Tells GitHub Pages to skip Jekyll processing (faster, simpler static builds). |
| `README.md` | This file. |

---

## Work log (what was built)

1. **Landing page created** (`index.html` + `styles.css`)
   - Hero section with name, avatar, and tagline.
   - **Telegram button** → https://t.me/nurzhqnn
   - **GitHub button** → https://github.com/vibecreative-dev
   - **Apps & Projects** grid of cards.
   - Footer with the Telegram link.

2. **Apps list**
   - Added the first approved app: **Mood.exe — Desktop Vibes**
     → https://apps.apple.com/kg/app/mood-exe-desktop-vibes/id6784635548
   - Two placeholder cards remain for future apps (edit them in `index.html`).

3. **AdMob `app-ads.txt`**
   - Added the authorized-sellers line requested by Google AdMob:
     ```
     google.com, pub-9262277756136498, DIRECT, f08c47fec0942fa0
     ```

4. **Repository migration (important)**
   - The site originally went to `vibecoding.dev.github.io`, which GitHub serves in a **subfolder**
     (`https://…github.io/vibecoding.dev.github.io/`). AdMob only checks `app-ads.txt` at the **root
     domain**, so it wouldn't have found the file there.
   - Moved everything to a **user site** repo named `vibecreative-dev.github.io`, which serves at the
     root: `https://vibecreative-dev.github.io/`. Now `app-ads.txt` lives where AdMob looks.

5. **GitHub Pages deployment**
   - Source set to **Deploy from a branch → `main` → `/ (root)`**.
   - Added `.nojekyll` to avoid Jekyll build stalls.

---

## Why `app-ads.txt` must be at the domain root

AdMob's crawler takes the **developer website** from the App Store listing, strips it down to the
**root domain**, and fetches `/app-ads.txt` from there. So the file must resolve at:

```
https://vibecreative-dev.github.io/app-ads.txt   ✅ (where it is now)
```

not in a subfolder. That's why the project moved to the `vibecreative-dev.github.io` user-site repo.

**Action needed in App Store Connect:** set the app's **developer / marketing website** to
`https://vibecreative-dev.github.io` so AdMob crawls the correct domain. Verification can take a day or two.

---

## How to edit

- **Add / change apps** — edit the `.app-card` blocks in `index.html`. Update the emoji icon,
  the `<h3>` title, the description, and the `href`.
- **Links** — the Telegram button uses `https://t.me/nurzhqnn`; the GitHub button uses
  `https://github.com/vibecreative-dev`.
- **Styling** — everything lives in `styles.css`.

After editing:

```bash
git add -A
git commit -m "Update site"
git push
```

GitHub Pages redeploys automatically on push (usually live within ~1 minute).

---

## GitHub Pages setup (one-time)

1. Repo **Settings → Pages**.
2. **Build and deployment → Source:** *Deploy from a branch* (not "GitHub Actions").
3. Branch **`main`**, folder **`/ (root)`** → **Save**.

### Troubleshooting a stuck deploy

If a deployment hangs on `deployment_queued` and times out:

- Check **Settings → Environments → `github-pages`** and remove any **Required reviewers**,
  **Wait timer**, or **Deployment branches** restriction that excludes `main`.
- Reset the source: set it to **None**, save, then back to **Deploy from a branch / main / root**, save.
- Cancel any stuck run in the **Actions** tab, then push again to trigger a fresh build.
- Confirm GitHub isn't having an incident: https://www.githubstatus.com/
