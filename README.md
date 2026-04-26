# Productivity Planner

A full-featured goal planning app with monthly calendar, weekly time-block scheduling, habit tracking, and achievement statistics.

Works as a **PWA** (installable on mobile/desktop via browser), a **web app** (hosted on any server), and a **desktop .exe** (via Electron).

---

## Quick Start Options

### Option A — Open Locally (Simplest)

Just double-click `index.html` to preview. Note: the PWA service worker requires a server to function, but the app itself works fine opened directly.

### Option B — Run a Local Web Server

Using Python (pre-installed on most systems):

```bash
cd planner-pwa
python -m http.server 8080
```

Then open **http://localhost:8080** in your browser. On mobile, use your PC's local IP (e.g. `http://192.168.0.10:8080`) while on the same Wi-Fi.

Using Node.js:

```bash
npx serve .
```

### Option C — Build Desktop .exe (Electron)

Requires **Node.js 18+** installed.

```bash
cd planner-pwa
npm install
npm start          # Launch in dev mode
npm run build:win  # Build Windows .exe installer → dist/
npm run build:mac  # Build macOS .dmg
npm run build:linux # Build Linux AppImage
```

The packaged installer will appear in the `dist/` folder.

---

## Deploy as a Web App (Access from Phone)

### Free Hosting Options

**Netlify (Recommended — Easiest)**

1. Go to [netlify.com](https://netlify.com) and sign up
2. Drag and drop the entire `planner-pwa` folder onto the deploy area
3. Done — you get a URL like `https://your-planner.netlify.app`

**Vercel**

1. Install Vercel CLI: `npm i -g vercel`
2. Run `vercel` inside the project folder
3. Follow the prompts

**GitHub Pages**

1. Push the project to a GitHub repository
2. Go to Settings → Pages → Source: Deploy from branch (main)
3. Your app will be at `https://username.github.io/repo-name`

### Install as PWA on Your Phone

Once deployed to any of the above:

1. Open the URL in Chrome (Android) or Safari (iOS)
2. **Android**: Tap the browser menu → "Add to Home Screen" or "Install App"
3. **iOS**: Tap the Share button → "Add to Home Screen"

The app will appear as a standalone icon and work offline.

---

## Project Structure

```
planner-pwa/
├── index.html          # Main app (self-contained React + Babel)
├── manifest.json       # PWA manifest (name, icons, theme)
├── sw.js               # Service worker (offline caching)
├── package.json        # Electron build configuration
├── icons/
│   ├── icon-192.png    # PWA icon (small)
│   └── icon-512.png    # PWA icon (large)
├── electron/
│   └── main.js         # Electron main process
└── README.md
```

---

## Features

| Tab        | Functionality                                                        |
|------------|----------------------------------------------------------------------|
| Monthly    | Calendar view, add/edit events with time, color, and notes           |
| Weekly     | Time grid with 10/30/60-minute blocks, fixed schedules & habits      |
| Statistics | 7-day / 30-day achievement rates, streaks, per-habit heatmaps       |

- All data is saved to **localStorage** — persists across sessions
- **Responsive design** — optimized layout for both desktop and mobile
- **Offline-capable** — service worker caches all assets
- Mobile weekly view shows **single-day swipe mode** for usability

---

## Customization Tips

- **Change colors**: Edit the `HABIT_COLORS` array near the top of the `<script>` block in `index.html`
- **Change fonts**: Swap the Google Fonts import in the `<head>` section
- **Add more hours**: Modify the `hours` array in `WeeklyTab` (currently 6:00–23:00)
- **Change start day**: Modify `getWeekDates()` to start on Monday instead of Sunday

---

## Troubleshooting

| Issue                          | Solution                                                    |
|--------------------------------|-------------------------------------------------------------|
| PWA won't install              | Must be served over HTTPS (or localhost). Use Netlify/Vercel |
| Fonts not loading              | Ensure internet connection on first load (fonts are cached)  |
| Electron build fails           | Make sure Node.js 18+ is installed. Run `npm install` first  |
| Data disappeared               | Data is per-browser localStorage. Different browser = fresh  |
