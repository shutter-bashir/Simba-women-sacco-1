<p align="center">
  <img src="icon-192.png" width="96" alt="Simba Women logo" />
</p>

<h1 align="center">Simba Women — SACCO Ledger</h1>

<p align="center">
  An offline-first, installable web app that replaces the paper ledger of a real Kenyan
  savings &amp; credit cooperative (SACCO / chama) — loan book, member savings,
  interest tracking, and year-end dividends, all on a phone.
</p>

<p align="center">
  <b>🔗 Live demo:</b> <a href="#">ADD-YOUR-NETLIFY-URL-HERE</a>
</p>

---

## Screenshots

| Loan book | Savings (Sengo) | Registry & analytics |
|---|---|---|
| ![Loan book](screenshots/loan-book.png) | ![Savings](screenshots/savings.png) | ![Records](screenshots/records.png) |

*(Screenshots show fictional demo data.)*

## The problem

Across Kenya, informal savings groups — chamas and SACCOs — manage significant
member money using handwritten ledgers and memory. Records get lost, interest
arithmetic goes wrong, disputes are hard to settle, and the treasurer carries the
entire burden. Commercial SACCO software assumes reliable internet, monthly fees,
and a desktop computer — none of which fit a community group meeting once a month.

This app digitizes the *actual rules* of a real cooperative, transcribed from its
ledgers, and runs entirely on the treasurer's phone — **no server, no account, no
internet required after install.**

## Features

- **Loan book** — issue loans, record repayments, see who is *Current* (paid this
  cycle), *At risk* (unpaid, cycle still open), or *Defaulted* (two missed cycles).
- **Faithful interest model** — 20% per 30-day cycle; unpaid interest carries
  forward **flat** onto the next cycle's due (never a compounding penalty), exactly
  as the co-op's paper records work.
- **Savings (Sengo)** — deposits, withdrawals, and per-member transaction history.
- **Year-end dividends** — two membership tiers pool the interest they paid in and
  split it among members who cleared their tier's threshold; defaulters are excluded.
- **Cycle engine** — "Close month" applies interest, rolls arrears forward, flags
  auto-defaults after two missed cycles.
- **Plain-language agent** — type *"Mary repaid 5000"* or *"Alice borrowed 15000"*
  and the books update, with an undo history.
- **Printable cooperative report** — one tap produces a clean, printable statement.
- **Backup / Restore** — export the entire books to a JSON file (email it, keep it
  on Drive, move to a new phone) and restore it anywhere.
- **Auto-save** — every change persists to the device instantly (localStorage);
  data survives refresh, restart, and going offline.
- **Installable PWA** — add to home screen on Android or iPhone; opens full-screen
  with its own icon and works with zero connectivity.

## Why vanilla JavaScript, one file, no framework?

A deliberate architecture decision, not a shortcut:

- **Target hardware is low-end Android on patchy 2G/3G.** The entire app is a
  single ~68 KB HTML file plus icons — smaller than most framework runtimes alone.
- **Zero build step, zero dependencies** — nothing to break, audit, or update; the
  file can be inspected end-to-end by anyone.
- **Offline is the default, not a feature.** A network-first service worker serves
  fresh code when online and the cached app when not, so updates arrive
  automatically without ever breaking offline use.
- **Privacy by architecture.** There is no backend. Member financial data never
  leaves the device it was entered on. This public repository contains **no real
  member data** — the app ships empty and each group enters its own records.

## How the money rules work

| Term | Meaning |
|---|---|
| **Due this cycle** | This cycle's 20% interest on the balance, plus any unpaid interest carried forward |
| **Current** | Member has paid at least the minimum due this cycle |
| **At risk** | Nothing paid yet this cycle — if the month closes unpaid, it counts as a missed cycle |
| **Defaulted** | Two missed cycles — deposits and dividends stop until manually cleared |
| **Carry-forward** | Unpaid interest (partial or fully missed) is added flat to next cycle's due — it never compounds |
| **Dividends** | Each tier's interest pool is split evenly among that tier's members who cleared the payment threshold |

## Run it

No install, no build:

```bash
# any static server works — for local development:
python3 -m http.server 8000
# then open http://localhost:8000
```

Or deploy the folder to any static host (Netlify, GitHub Pages, Cloudflare Pages).
Open the URL on a phone → **Install app** (Android/Chrome) or **Share → Add to
Home Screen** (iPhone/Safari).

## Project structure

```
index.html    the entire application — UI, styles, and logic
sw.js         service worker: network-first with offline cache fallback
manifest.json PWA manifest (installability, icons, theming)
icon-*.png    app icons
screenshots/  README images (fictional demo data)
```

## Roadmap

- Demo mode button (load sample data to explore the app)
- CSV export for spreadsheet users
- Unit tests for the interest / arrears / dividend math
- Optional PIN lock on open

## License

MIT — free to use and adapt for your own chama or SACCO. See [LICENSE](LICENSE).
