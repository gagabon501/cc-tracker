# CC Budget Tracker

A lightweight Progressive Web App (PWA) for tracking fortnightly credit card expenses against a fixed budget of **$1,170.05**. Built to support a debt payoff strategy by keeping recurring and variable CC charges visible and under control.

## What It Does

This app helps you monitor credit card spending within each fortnightly pay cycle. All known recurring charges (subscriptions, bills, utilities) are pre-loaded. You tick them off as they appear in your bank app and log any unplanned expenses. A visual gauge warns you when spending approaches or exceeds the budget — because every dollar over the limit delays your CC debt payoff.

### Key Features

- **Budget ring gauge** — shows percentage of $1,170.05 used, with colour-coded thresholds (green → amber at 85% → red at 100%+)
- **Charged vs Pending split** — tick off expenses as they clear in your ASB app to see what's left to come through
- **Unplanned expense logging** — add unexpected charges on the fly with category tagging
- **Automatic period detection** — anchored to a fortnightly pay cycle starting 27 March 2026, the app always knows which period you're in
- **Days remaining countdown** — shows how many days are left in the current fortnight
- **Persistent local storage** — data saves per-period on your device and carries over between visits
- **Offline support** — service worker caches the app after first load
- **Installable on Android** — add to home screen for a full-screen, native-app experience with no browser chrome

## Pre-loaded Expenses

| Expense                  | Amount   | Category      | Type     |
|--------------------------|----------|---------------|----------|
| One NZ (Mobile/Internet) | $421.62  | Bills         | Fixed    |
| LBR                      | $300.00  | Bills         | Fixed    |
| Contact (Electric)       | $200.93  | Bills         | Fixed    |
| Fuel                     | $130.00  | Transport     | Variable |
| MongoDB                  | $40.00   | Subscriptions | Fixed    |
| Heroku                   | $30.00   | Subscriptions | Fixed    |
| Netflix                  | $17.50   | Subscriptions | Fixed    |
| MyLotto                  | $15.00   | Subscriptions | Fixed    |
| Spotify                  | $7.50    | Subscriptions | Fixed    |
| Amazon Prime             | $7.50    | Subscriptions | Fixed    |

**Total pre-loaded: $1,170.05**

Fixed charges auto-bill and can only be ticked off. Variable charges (currently just Fuel) can be removed or adjusted, and new unplanned expenses can be added in any category.

## Installation

### Host on GitHub Pages (free)

1. Create a GitHub account or sign in at [github.com](https://github.com)
2. Create a new repository (e.g. `cc-tracker`)
3. Upload `cc-budget-tracker.html` and rename it to `index.html`
4. Go to **Settings → Pages → Source** → select **main branch** → Save
5. The app will be live at `https://<your-username>.github.io/cc-tracker/`

### Install on Android

1. Open the hosted URL in **Chrome**
2. Tap the **three-dot menu (⋮)** → **"Add to Home screen"**
3. The app installs with its own icon and opens full-screen without a browser bar

### Install on iPhone

1. Open the hosted URL in **Safari**
2. Tap the **Share button** → **"Add to Home Screen"**

### Run locally

No build step required. Open `cc-budget-tracker.html` directly in any browser. Note that localStorage will still work, but the service worker requires HTTPS to function (this only affects offline caching — all other features work fine locally).

## How to Use

1. **Each payday**, open the app — it automatically detects the current fortnightly period
2. **Check your ASB app** for which CC charges have posted
3. **Tick off** each charge as it appears — the Charged/Pending counters update live
4. **Log unplanned expenses** (extra fuel, one-off purchases) using the "+ Add Unplanned Expense" button
5. **Watch the ring gauge**:
   - **Green** — on track, spending within budget
   - **Amber (85%+)** — approaching limit, avoid non-essential CC spending
   - **Red (100%+)** — over budget, the excess directly delays your debt payoff
6. **Reset** at any time to restore defaults for the current period

## Technical Details

- **Single HTML file** — no dependencies, no build tools, no framework
- **~400 lines** of vanilla HTML, CSS, and JavaScript
- **localStorage** — data persists per fortnightly period using the key format `cc-budget-tracker:YYYY-MM-DD`
- **Service Worker** — inline blob-registered worker for basic offline caching
- **Fonts** — DM Sans (UI) and DM Mono (numbers) loaded from Google Fonts
- **Responsive** — designed for mobile-first with safe area insets for notched devices

## Customisation

To change the budget limit, edit this line near the top of the file:

```javascript
const BUDGET = 1170.05;
```

To change the pay cycle anchor date, edit this line in the `getFortnightDates()` function:

```javascript
const anchor = new Date(2026, 2, 27); // Month is 0-indexed: 2 = March
```

To add, remove, or edit default expenses, modify the `DEFAULT_EXPENSES` array. Set `fixed: true` for charges that shouldn't be removable, and `fixed: false` for variable ones.

## Privacy

All data stays on your device. Nothing is sent to any server. The hosted HTML file is completely static.
