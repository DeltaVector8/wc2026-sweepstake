# WC2026 Sweepstake Tracker

A lightweight World Cup 2026 sweepstake tracker for a private WhatsApp group.

The app shows:

* participant standings
* allocated teams
* team flags
* fixture list
* points by team
* live match data from football-data.org
* automatic scoring from match results

Live app:

```text
https://deltavector8.github.io/wc2026-sweepstake/
```

## How it works

The front-end is a static HTML app hosted on GitHub Pages.

Live football data is fetched through a Cloudflare Worker proxy:

```text
GitHub Pages app
        ↓
Cloudflare Worker
        ↓
football-data.org API
```

The proxy is used because direct browser calls to football-data.org are blocked by CORS. The API key is stored in Cloudflare, not in the public GitHub code.

## Scoring

Current scoring rules:

| Event               | Points |
| ------------------- | -----: |
| Win                 |     +3 |
| Draw                |     +1 |
| Clean sheet         |     +1 |
| Reach Round of 16   |     +3 |
| Reach Quarter Final |     +5 |
| Reach Semi Final    |     +8 |
| Reach Final         |    +12 |
| Win Tournament      |    +20 |

## Participants

| Participant     | Teams |
| --------------- | ----: |
| Zion & Megan    |    10 |
| Michael & Naomi |    10 |
| Ziggy & Deron   |    10 |
| Michael & Mary  |     9 |
| Kayla & Keria   |     9 |

## Data source

Match data is provided by:

```text
football-data.org
```

The Cloudflare Worker endpoint currently used by the app is:

```text
https://wc2026-api.oyediran.workers.dev/matches
```

## Deployment

The app is deployed using GitHub Pages from:

```text
index.html
```

To update the app:

1. Edit `index.html`
2. Commit changes to `main`
3. Wait for GitHub Pages to refresh
4. Reload the live app

## Cloudflare Worker

The Worker keeps the football-data.org API key out of the browser.

Required Worker environment variable:

```text
FOOTBALL_DATA_API_KEY
```

The Worker calls:

```text
https://api.football-data.org/v4/competitions/WC/matches?season=2026
```

and returns the result to the front-end with CORS headers enabled.

## Status

Working live-data version.

Demo data is retained as a fallback if the live API is unavailable.
