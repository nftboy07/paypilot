# PayPilot — AI invoicing & PayPal payment requests for freelancers

**Type an invoice in plain English. PayPilot builds it, sends a PayPal payment request, tracks it, and writes the follow-up for you.**

Built solo for the [PayPal AI Hackathon](https://paypalaihackathon.devpost.com/) on Devpost ($67,500+ in prizes, deadline 12 Nov 2026, 12:00pm PT / 13 Nov 01:30 IST).

![Status](https://img.shields.io/badge/hackathon-PayPal%20AI%20Hackathon-003087) ![License](https://img.shields.io/badge/license-MIT-green) ![Stack](https://img.shields.io/badge/stack-single--file%20HTML%20%2B%20vanilla%20JS-blue)

---

## The problem

Freelancers and small sellers lose hours — and money — to invoicing admin: re-typing line items into clunky forms, forgetting due dates, and awkwardly chasing late payments. Generic invoicing tools still start with a blank form. PayPilot starts with a sentence.

## What PayPilot does

1. **Plain-English invoice creation (AI parser).** Type *"Invoice Priya Nair at Bloom Studio for logo design $450 and business cards $80, due in 7 days"* and PayPilot extracts the client, email, line items, amounts, currency (USD/EUR/GBP/INR/AUD/CAD) and due date ("in 7 days", "net 14", "due 20 Nov"…). Review and edit before saving — nothing is sent anywhere.
2. **PayPal payment-request / checkout preview.** Every invoice generates a PayPal Checkout preview showing exactly what the client would pay, and runs the full create-order → approve → capture flow (sandbox simulation — see below).
3. **Invoice book with live statuses.** Draft / Sent / Paid / **Overdue (auto-detected from due dates)**, with totals: invoiced, collected, outstanding, overdue. Stored in `localStorage`, so the book survives reloads with zero backend.
4. **Smart follow-up & reminder drafts (AI writer).** Pick an invoice and a tone — friendly, polite, or firm (auto-suggested for overdue) — and PayPilot drafts a complete, ready-to-copy reminder email with the amount, items, due date and days overdue filled in.
5. **Smart insights.** A local insights engine reads your book and tells you the single best next action: which overdue invoice to chase first, what's falling due this week, your collection rate, and which drafts are sitting unsent.

## How to run it

No build step, no server, no dependencies, no API keys.

- **Option A (fastest):** download `index.html` and open it in any modern browser (`file://` works).
- **Option B (hosted):** enable GitHub Pages on this repo (Settings → Pages → `main` / root) and open the Pages URL — that URL is also the functional demo link for the Devpost submission.
- **Option C:** serve the folder with any static server, e.g. `python3 -m http.server 8000`, then visit `http://localhost:8000`.

Demo data (3 sample invoices) is seeded on first run so judges can explore immediately. Use **Reset demo data** or delete individual invoices to start clean. Everything is stored only in the browser's `localStorage` under the key `paypilot_invoices_v1`.

## How the AI works

The AI layer runs **entirely on-device** in vanilla JavaScript — deliberately, so judges need no API key and no account to evaluate the full flow:

- **Natural-language parsing** (`parsePlainEnglish()`): pattern- and grammar-based extraction of client names, emails, priced line items (including `2x …`, `8 hours … at $60/hr`), currencies and natural due-date expressions.
- **Reminder generation** (`draftReminder()`): context-aware template composition keyed to invoice status, tone and days overdue.
- **Insights** (`renderInsights()`): rule-based cash-flow analysis over the invoice book.

**Swapping in an LLM:** replace `parsePlainEnglish()` with a `fetch()` to the model of your choice (OpenAI, Claude, Gemini, an open-source endpoint…) that returns the same JSON shape — `{ client, email, currency, due, items: [{ desc, amount }] }` — and the rest of the app is unchanged. This is stated in the Devpost "Tools" field: the shipped AI is a deterministic on-device parser/writer designed by the entrant (with AI-assisted development), architected for a drop-in LLM upgrade.

## How the PayPal integration works — and going live with the real sandbox

The hackathon requires integrating the PayPal developer platform **using the free sandbox environment**. This build ships **without the entrant's personal sandbox credentials** (none are committed — never commit credentials), so the payment step runs as a **clearly-labelled sandbox-style simulation**. Every simulated step maps 1-to-1 to the real API, and the integration points are stubbed in one place in `index.html`:

| PayPilot step | Real PayPal call (sandbox) |
|---|---|
| `PayPalAdapter.createOrder()` | `POST https://api-m.sandbox.paypal.com/v2/checkout/orders` |
| Buyer approval dialog | PayPal JS SDK (`https://www.paypal.com/sdk/js?client-id=…`) `paypal.Buttons` approval flow |
| `PayPalAdapter.captureOrder()` | `POST https://api-m.sandbox.paypal.com/v2/checkout/orders/{order_id}/capture` |
| Send-as-invoice alternative | `POST /v2/invoicing/invoices` then `POST /v2/invoicing/invoices/{id}/send` |

**To go live (about 5 minutes, free):**

1. Create a free account at [developer.paypal.com](https://developer.paypal.com), go to **Apps & Credentials → Sandbox → Create App**, and copy the **Client ID**.
2. In `index.html`, find the `PAYPAL_CONFIG` block at the top of the script: paste the Client ID into `clientId` and set `mode: "sandbox-live"`.
3. Follow the `sandbox-live` note inside `PayPalAdapter` — load the PayPal JS SDK with that client-id and render `paypal.Buttons()` in place of the simulated approval step (a server-side OAuth token exchange is the production pattern for the Orders API calls). No other app code changes: statuses, receipts and tracking already consume real capture IDs identically to simulated ones.

## Tech / built with

HTML5 · CSS3 (custom properties, grid, no framework) · Vanilla JavaScript (ES2020) · Web `localStorage` API · `Intl.NumberFormat` currency formatting · PayPal Orders v2 API + Invoicing API (sandbox-mapped, simulated in this build) · GitHub Pages (hosting) · No external network calls in the shipped file.

## Project structure

```
paypal-ai-hackathon/
├── index.html       # the entire app (UI + AI parser + PayPal adapter + store)
├── README.md        # this file
├── SUBMISSION.md    # ready-to-paste Devpost submission fields
├── REQUIREMENTS.md  # official hackathon requirements, researched from Devpost
└── LICENSE          # MIT
```

## Devpost description draft

> **PayPilot — plain English in, paid invoice out.**
>
> Freelancers don't hate getting paid; they hate the admin around it. PayPilot removes the form entirely. Describe the job in one sentence and its on-device AI builds a structured invoice — client, line items, currency, due date — then generates a PayPal payment request your client can pay in one click. PayPilot tracks every invoice from draft to paid, flags overdue ones automatically, tells you the single best next action for your cash flow, and drafts the follow-up email (friendly, polite, or firm) so chasing payment takes seconds, not willpower.
>
> PayPilot is built around the PayPal Orders v2 and Invoicing APIs. This hackathon build runs the checkout as a clearly-labelled PayPal sandbox simulation with the live integration stubbed and documented — drop in a free sandbox client-id and the identical flow calls the real PayPal sandbox. The AI layer runs fully on-device (natural-language parsing + reminder writing), so anyone can judge the complete flow with no setup, no keys, and no account.
>
> **For:** freelancers, consultants, and small sellers who invoice from a phone between jobs. **Impact:** fewer unpaid invoices, faster payment, zero invoicing software to learn.

## Demo video script (~75 seconds, under the 3-minute limit)

Record screen + voiceover. Keep it public on YouTube, no copyrighted music (use none or YouTube's free library).

| Time | On screen | Say |
|---|---|---|
| 0:00–0:10 | PayPilot homepage, stats bar | "Freelancers lose hours to invoicing forms — and still get paid late. This is PayPilot: type what you did, and AI + PayPal handle the rest." |
| 0:10–0:30 | Click the "Logo + brand kit" example chip → **Parse with AI** → fields fill in | "One sentence in… client, items, amounts, currency and due date — all extracted automatically. I can tweak anything before saving." |
| 0:30–0:45 | **Save + PayPal checkout preview** → modal opens → **Pay with PayPal (simulated)** → steps run → PAID | "PayPilot creates a PayPal payment request. The client approves in PayPal, the payment is captured, and the invoice flips to Paid with its capture ID. This build runs PayPal's sandbox flow as a labelled simulation — the live sandbox integration is stubbed and documented in the README." |
| 0:45–1:00 | Invoice book: overdue invoice highlighted → **Draft reminder** | "This invoice is overdue — PayPilot flagged it automatically. One click drafts a firm-but-professional reminder with the PayPal link, ready to send." |
| 1:00–1:15 | Smart insights panel + stats | "And PayPilot always tells me my best next move for cash flow. Plain English in — paid invoice out. That's PayPilot, for the PayPal AI Hackathon." |

## License

MIT — see `LICENSE`. PayPal and the PayPal logo are trademarks of PayPal, Inc.; this project is a hackathon entry and is not affiliated with or endorsed by PayPal.
