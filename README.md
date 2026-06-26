# 🏆 World Cup 2026 — Cobbers Sweepstake

A live group-stage table, knockout bracket, leaderboard and "Hall of Shame" for the Cobbers World Cup 2026 sweepstake. Every team is labelled with the person who drew it, so you can see at a glance how your team — and your rivals — are doing.

**Live site:** `https://<your-username>.github.io/worldcup-sweepstake/`

---

## What it does

- **Groups** — all 12 group tables (A–L), each team showing its flag, name and the sweepstake owner(s), colour-coded by position (green = top two, amber = third/bubble, red = bottom).
- **Bracket** — the full 48-team knockout tree (Round of 32 → Round of 16 → Quarter-finals → Semi-finals → Final, plus the third-place playoff). Group winners and runners-up fill in automatically from the live tables; third-place slots lock once the group stage ends.
- **Leaderboard** — every participant and whether their team is still alive, qualifying, on the bubble, or knocked out.
- **Loser Board** — the ten most miserable performances, ranked by fewest points then worst goal difference, as a full league table (P / W / D / L / GF / GA / GD / Pts).

## How it works

The page is a single self-contained `index.html` — no build step, no server. It loads React and Tailwind from CDNs and renders entirely in the browser.

Results are computed from **real match scores** pulled from a public, CORS-enabled World Cup JSON feed:

1. It first tries a fast-updating community feed, falling back to the upstream [openfootball](https://github.com/openfootball/worldcup.json) dataset if that's unavailable.
2. Group tables are calculated from the actual scorelines (points, goal difference, ranking).
3. Where the feed hasn't yet caught up with a group, a **curated snapshot** (25 Jun 2026) is shown instead, and live data takes over group-by-group as the feed updates.

It refreshes automatically when the page is opened, on the **Refresh** button, and once a day at 06:00 UK time if left open.

### Knockouts

Once both teams in a knockout tie are known, results flow in from the feed automatically. You can also **tap either team to advance them manually** — handy for penalty shootouts the feed can't resolve. Manual picks are saved in your own browser (`localStorage`), so they persist for you between visits.

## Hosting (GitHub Pages)

1. Create a **public** repository.
2. Add `index.html` (and this `README.md`) and commit.
3. **Settings → Pages → Source: Deploy from a branch → `main` / `root` → Save.**
4. After ~1 minute the site is live at `https://<your-username>.github.io/<repo-name>/`.

## Updating

Edit `index.html` in the repo (pencil icon → edit → **Commit changes**). GitHub Pages redeploys automatically within a minute.

## Notes & caveats

- **Feed freshness:** live data is only as current as the community feed, which can run a few hours (or more) behind. The curated snapshot keeps the board sensible in the meantime.
- **Manual picks are per-browser:** because this is a static site with no shared backend, tap-to-advance overrides are local to each viewer. The underlying live results stay consistent for everyone, since all visitors read the same feed.

## Credits

Match data from the [openfootball / world.cup.json](https://github.com/openfootball/worldcup.json) open dataset (public domain) and its live-updating community fork. Built for the Cobbers sweepstake.
