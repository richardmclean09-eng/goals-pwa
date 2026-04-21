# Goals Tracker PWA

Personal weekly goal tracker — April 21 to June 8, 2026.

## Deploy to Vercel

1. Push this folder to a GitHub repo (or use Vercel CLI)
2. Go to [vercel.com](https://vercel.com) → New Project → Import the repo
3. Vercel will auto-detect the config. Just click Deploy.

**Or via Vercel CLI:**
```bash
cd goals-pwa
npx vercel --prod
```

## Add to iPhone Home Screen

1. Open the deployed URL in Safari on your iPhone
2. Tap the Share button (square with arrow)
3. Scroll down and tap "Add to Home Screen"
4. Name it "Goals" and tap Add

The app will now appear on your home screen and open full-screen without Safari's browser chrome.

## How it works

- Pure HTML/CSS/JS — no build step, no framework, no backend
- Data stored in localStorage (on-device only)
- Service worker for offline support
- PWA manifest for home screen install

## Data

All data stays on your phone in localStorage. No server, no sync. 
If you clear Safari data, you'll lose your tracking history.
