# MoneyMemo

> **Track what's owed, simply.**

A single-file, offline-first personal ledger app built with vanilla HTML, CSS, and JavaScript. No server, no sign-up, no internet required — runs entirely in your browser.

---

## Features

### Core Ledger
- **Profiles** — Create profiles for people you exchange money with (Dad, Friend, Vendor, etc.)
- **Transactions** — Log money sent or received with amount, note, and date
- **Balance Tracking** — Auto-calculated balance per profile: total sent − total received
- **Summary Dashboard** — Overall "Owed to You", "You Owe", and net balance at a glance
- **Duplicate Prevention** — Blocks creating profiles with the same name

### Transaction Management
- **Edit Transactions** — Modify type, amount, note, or date of any transaction
- **Edit Profiles** — Rename existing profiles
- **Delete with Undo** — Deleting a transaction or profile shows a 5-second undo button
- **Date Picker** — Backdate transactions or default to today
- **Date Grouping** — Transactions grouped by date headers in the ledger

### Search, Filter & Sort
- **Search** — Filter transactions by note text
- **Type Filter** — Show All, Sent only, or Received only
- **Date Sort** — Toggle between newest-first and oldest-first

### Settlement
- **Settle Up** — One-tap adds a zeroing transaction to bring balance to ₹0

### Data Management
- **Export (JSON)** — Download all profiles and transactions as `data.json`
- **Import (JSON)** — Restore data from a previously exported file
- **CSV Export** — Export a single profile's transactions as a spreadsheet-friendly CSV
- **Reset** — Restore built-in seed data (with confirmation)

### UX & Preferences
- **Dark Mode** — Moon/sun toggle with saved preference
- **Help Guide** — In-app help via the **?** button
- **Indian Currency** — Amounts with ₹ and Indian comma grouping (e.g. ₹1,20,000)
- **Mobile-First** — Responsive design optimised for phones; works on desktop too
- **Success Popups** — Visual confirmation on transaction add and settle
- **Toast Notifications** — Contextual feedback for all actions

---

## Quick Start

1. Open `flowledger.html` in any modern browser (Chrome, Safari, Firefox, Edge)
2. Add a profile name and tap **+ Add**
3. Tap the profile card to open its transaction ledger
4. Add transactions — choose Sent or Received, enter amount, note, and date
5. View balances on the dashboard summary bar

No build tools, dependencies, or installation needed.

---

## How It Works

| Term | Meaning |
|------|---------|
| **Sent** | Money you gave to the person → they owe you |
| **Received** | Money they gave back to you → reduces what they owe |
| **Balance** | `Σ sent − Σ received` — positive means they owe you, negative means you owe them |
| **Settle** | Adds a single transaction that zeros the balance |

---

## Technical Details

| Aspect | Detail |
|--------|--------|
| **Architecture** | Single HTML file — HTML + CSS + JS, no build step, no framework |
| **Storage** | `localStorage` with key `moneymemo_data` |
| **Theme** | Stored in `moneymemo_theme` (`"dark"` or `"light"`) |
| **Currency** | Indian Rupee (₹) with Indian comma grouping |
| **Rendering** | Imperative DOM updates — no virtual DOM, no library |
| **Security** | Input sanitized with `escapeHtml()` / `escapeAttr()`. All data stays local |
| **Font** | System font stack (SF Pro, Segoe UI, Roboto) |

---

## Data Schema

All data is stored as a single JSON object in `localStorage`:

```json
{
  "profiles": [
    { "id": "1774370664675", "name": "Dad" }
  ],
  "transactions": [
    {
      "id": "1774393944352",
      "profileId": "1774370664675",
      "date": "25-03-2026",
      "type": "sent",
      "amount": 80000,
      "note": "My Savings"
    }
  ]
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `profiles[].id` | string | Unique ID (timestamp-based) |
| `profiles[].name` | string | Display name (max 50 chars) |
| `transactions[].id` | string | Unique ID |
| `transactions[].profileId` | string | Links to a profile |
| `transactions[].date` | string | `dd-mm-yyyy` format |
| `transactions[].type` | string | `"sent"` or `"received"` |
| `transactions[].amount` | number | Positive value |
| `transactions[].note` | string | Optional description (max 100 chars) |

---

## localStorage Keys

| Key | Purpose |
|-----|---------|
| `moneymemo_data` | All profiles and transactions (JSON) |
| `moneymemo_theme` | Dark mode preference (`"dark"` or `"light"`) |

---

## Seed Data

The app includes embedded seed data in the `SEED_DATA` object inside the HTML file. On first load (no localStorage), seed data is used. Edit `SEED_DATA` to customise the starting state for a new device. Tap **Reset** to restore it at any time.

---

## File Structure

```
flowledger.html         ← The entire MoneyMemo app (single file)
README-moneymemo.md     ← This documentation
```

---

## Browser Support

- Chrome / Edge 80+
- Firefox 78+
- Safari 13+
- Mobile browsers (iOS Safari, Chrome for Android)

---

## Privacy

- **Zero tracking** — no analytics, no telemetry, no cookies
- **Fully offline** — works without internet
- **Data stays local** — everything lives in your browser's `localStorage`
- **No server** — no backend, no API calls, no cloud
- Clearing browser data will erase everything — use **Export** to keep backups

---

## Version

**v1.0** — May 2026
