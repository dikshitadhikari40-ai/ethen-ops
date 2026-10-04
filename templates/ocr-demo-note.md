# OCR Demo Note — Photograph a Bill, Get Ledger Data

**A field guide from a live deployment.** This is the exact pattern ETHEN runs daily inside a Nepali manufacturing company: supplier bills arrive as photos, and land as structured rows — no typing.

## The pipeline

```
photo (WhatsApp / scan)
   ↓ deskew + denoise
   ↓ vision model (layout-aware, not plain OCR)
   ↓ field extraction: party, invoice no, date, line items, totals, tax
   ↓ confidence scoring per field
   ↓ ✅ auto-accept ≥ 98% · ⚠️ human review below
   ↓ structured draft → approval popup → ledger
```

## Why it works when naive OCR doesn't

1. **Layout-aware extraction** — totals and tax fields are located by document structure, not string-guessing
2. **Confidence gates** — anything below threshold is parked for a human, never silently posted
3. **Party matching** — extracted vendor names are fuzzy-matched against your existing ledger parties before insertion
4. **Approval chain** — the OCR never writes to the ledger directly; every entry is a draft until a named human taps Approve (see [`approval-popup.html`](./approval-popup.html))

## Try it in your business (1-hour test)

1. Photograph 5 of last month's supplier bills
2. Extract: party, invoice number, date, subtotal, tax, total
3. Compare against what your bookkeeper typed
4. Count the minutes saved × bills per month — that's your payback math

## Want the installed version?

ETHEN installs this pipeline live in 7–14 days, wired to your ledger, with approval gates included. → [Offers & pricing](../offers/pricing.md)

---
⭐ **Star this repo** if the guide was useful · 🍴 fork the templates · MIT licensed.
