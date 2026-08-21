# MMTrades — Period PnL

A companion page to [mmtrades-dashboard](https://github.com/munga068-ctrl/mmtrades-dashboard) that shows the trades broken down by period:

- **PnL by Day of Week** — cumulative P&L for Mon–Fri, all-time.
- **PnL by Month** — monthly P&L totals with a year selector.
- **PnL by Week** — an all-time weekly waterfall, one bar per Monday-starting trading week that had at least one trade, with the dollar value labeled on the bar.

It's synced from the same Notion `DASHBOARD` data source as `mmtrades-dashboard`, using the same `SYNC_MARKER` pattern.

## Setup

1. **Add the `NOTION_TOKEN` secret** to this repo: Settings → Secrets and variables → Actions → New repository secret. Use the same integration token you already use for `mmtrades-dashboard` (it needs read access to the same `DASHBOARD` database).
2. **Enable GitHub Pages**: Settings → Pages → Source: "Deploy from a branch" → Branch: `main`, folder `/ (root)`.
3. **Run the sync once manually**: Actions tab → "Sync Notion trades" → Run workflow. After that it runs automatically every 5 minutes.

Your page will be live at `https://<your-username>.github.io/<this-repo-name>/`.

## Files

- `index.html` — the page itself (self-contained, vendors nothing — pulls Chart.js from a CDN with mirror fallbacks).
- `sync.js` — pulls `{ date, pnl }` rows from Notion and rewrites the `TRADES` array between the `SYNC_MARKER_START` / `SYNC_MARKER_END` comments in `index.html`.
- `.github/workflows/sync.yml` — runs `sync.js` on a schedule and commits the result.
