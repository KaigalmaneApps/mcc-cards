# Indian Card MCCs

Indian card issuers often provide limited or unclear documentation about which Merchant Category Codes (MCCs) are eligible for cashback, reward points, or bonus categories. This makes it difficult for users to know whether a specific transaction will earn benefits.

This repository aims to solve that problem by offering a **centralized, transparent, and community-maintained database** of MCC rules for **Indian credit and debit cards**. It includes:

- A **single unified MCC definitions file** (`mcc_definitions.json`) with detailed descriptions for every MCC.
- **Bank-wise and card-wise folders**, each containing lightweight `included.json` and `excluded.json` files listing eligible and ineligible MCCs.
- A clear and simple structure that contributors can easily extend and verify.
- A public dataset developers can use for tooling, cashback calculators, browser extensions, or apps.

Whether you're a card optimizer, developer, researcher, or enthusiast, this repository provides a structured, verifiable reference to understand MCC eligibility across Indian payment cards.

---

## What this repo contains

- `mcc_definitions.json` — **authoritative MCC dictionary** with names/descriptions/examples.
- `data/` — **bank → card** folders, each card containing `included.json`, `excluded.json`, `meta.json`, and `card_overview.md`.

---

## Goals

1. Create a single, searchable, and verifiable source of truth for which MCCs are accepted or excluded for cashback/bonus categories by Indian cards.
2. Make it easy for cardholders to find whether a transaction's MCC will earn cashback/points.
3. Provide clear contribution guidelines so data can be added and verified collaboratively.

---

## Repository layout & file formats

### Root files
- **`mcc_definitions.json`** — single source of truth for MCC info.
  - Keys: 4-digit MCC codes as strings (e.g., `"5411"`).
  - Values: `{ name, description, examples, last_updated }`.

### Data folders
- **`data/<bank_slug>/<card_slug>/`** — one folder per card.
  - `included.json` — array of MCC strings that **earn** cashback/points.
  - `excluded.json` — array of MCC strings that **do not earn** cashback/points.
  - `meta.json` — metadata about the card (issuer, card_name, source_links, last_verified, notes etc).
  - `card_overview.md` — human-readable overview of benefits, caps, caveats, and FAQs for that card.

> Use strings for MCCs (e.g., `"4121"`) to avoid accidental numeric coercion or leading-zero issues.

---

## File / folder examples

```
/ (repo root)
├─ README.md
├─ mcc_definitions.json
├─ data/
│  ├─ hdfc/
│  │  ├─ millenia/
│  │  │  ├─ included.json
│  │  │  ├─ excluded.json
│  │  │  ├─ meta.json
│  │  │  └─ card_overview.md
│  │  └─ infinia/
│  │     ├─ included.json
│  │     ├─ excluded.json
│  │     ├─ meta.json
│  │     └─ card_overview.md
│  └─ sbi/
│     └─ cashback/
│        ├─ included.json
│        ├─ excluded.json
│        ├─ meta.json
│        └─ card_overview.md
└─
```

---

## Card folder example (`data/<bank_slug>/<card_slug>/`)

### `meta.json` (suggested)
```json
{
  "issuer": "HDFC",
  "bank_slug": "hdfc",
  "card_name": "HDFC Millenia",
  "card_slug": "millenia",
  "last_verified": "2025-11-09",
  "source_links": [
    "https://www.hdfcbank.com/personal/pay/cards/millennia-cards/millennia-cc-new"
  ],
  "notes": "Fuel spends eligible for surcharge waiver but no cashback. Online category has monthly cap."
}
```
> For debit cards, append `-debit` as some card names exist in both credit and debit linups.

### `card_overview.md`
Include a short narrative about benefits, caps, exclusions, and gotchas that are **not** obvious from MCC lists. Below is an example, it can have different structure.

```
# HDFC Millenia — Overview

**Categories & caps**
- Online: 5% up to ₹1,000 per month
- Wallet loads: excluded

**Key caveats**
- No cashback on fuel (MCC 5541, 5542)
- EMI transactions may not earn rewards

**Verification**
- T&Cs verified on 2025-11-09, see links in `meta.json`.
```

### `included.json`
```json
["5411", "5812", "5814", "4121"]
```

### `excluded.json`
```json
["6011", "6211", "7995"]
```

## CONTRIBUTING guidelines (summary)

- Always provide a source for changes (URL to T&C or screenshot). If you attach screenshots, explain which clause supports the change.
- Use one PR per issuer (or related small set of changes).
- When updating many rows, explain methodology in PR description (how you searched T&Cs, dates, sample transactions used).

---

## Verification workflow (recommended practice)

1. Contributor opens PR with change + source link.
2. Once approved, the PR is merged.

Consider adding a label like `needs-verification` for community review.

---

## Privacy & ethics
- Do **not** store or publish personally identifiable data or screenshots with full PAN/card numbers.
- For screenshots, redact personal info and only include the relevant clause.


