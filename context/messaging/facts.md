# Moniepoint - Authorized Copy Facts

> The ONLY source of names, numbers and claims for prospect-facing copy (`/campaign-copy` FACTS GATE). Anything not listed here renders as `{{placeholder}}` in copy, never from memory and never invented.
>
> Seeded 2026-11-17 from `context/docs/research/` (sourced) and `context/brand-kit/brand.md` (voice). Claims below are CANDIDATES, marked PENDING until someone signs them off. `TODO` fields must be filled before copy ships.

**Last updated:** 2026-11-17 (partial inputs from owner; see TODOs and BLOCKER)

---

## BLOCKER before any send

First-party-data clearance: this campaign's hook ("based on your sales, you qualify") puts internal transaction data into merchant-facing copy. **Not yet cleared.** Until data/compliance confirms it, keep every sales and loan figure as a per-lead `{{variable}}` and do not state it as a claim. (Carried from `output/campaigns/first-loan-on-sales-history/workflow-spec.md`.)

## Sender identity

| Field | Value |
|---|---|
| Sender email | samicol@gmail.com (provided 2026-11-17) |
| Sender name(s) | TODO (display name for the signature, needed before send) |
| Title | TODO |
| Signature format | TODO |
| Sender persona notes | owned-channel / lifecycle register, existing customers, not cold |

## What we do (locked value prop)

Candidate value-prop lines (from `context/positioning/`, PENDING sign-off):
- **Variant A:** "Moniepoint is a business payments and banking platform: get paid in person, and borrow against your own sales." [positioning], [voice]
- **Variant B:** "Moniepoint turns the sales you already make into your first business loan." [customers]

Product one-liner (context, not copy): business payments, POS/agency banking, credit and bookkeeping for Nigerian MSMEs. [company]

## Approved claims and numbers (CANDIDATES, PENDING sign-off)

| Claim | Candidate phrasing | Source | Approved by / date |
|---|---|---|---|
| First-time credit | "75% of entrepreneurs received their first-ever loan from Moniepoint" | context/docs/research/customers.md (impact.moniepoint.com) | PENDING |
| Earnings lift | "80% of merchants saw increased business earnings" | customers.md (impact.moniepoint.com) | PENDING |
| Loans disbursed | "over 700 million dollars in loans to MSMEs in 2025" | customers.md (guardian.ng) | PENDING |
| Market density | "Moniepoint powers two out of three in-person payments in Onitsha" | customers.md (moniepoint.com/blog) | PENDING |
| Scale | "the partner of choice for over 1.5 million businesses" | context/docs/research/voice.md (moniepoint.com/about) | PENDING |

**As of 2026-11-17 the owner approved NO claims (left blank). Every candidate above is NOT approved and must not appear in copy until signed off.**

**Formatting rules for proof:**
- Write company and product names as plain words, no domains (domains turn into links in sent email).
- Scraped per-lead counts are prefixed "at least", never stated as exact.
- Self-cited scale numbers conflict across sources; date any figure if used. [voice]

## Numbers to keep fuzzy (never quote as hard numbers)

- Total transaction value (sources conflict: 170bn run-rate vs 17bn monthly). [voice]
- Employee / team size (third-party figures disagree). [company]
- Any per-merchant loan amount outside the per-lead `{{prequalified_amount}}` variable.

## Authorized social-proof names

| Name | What it proves | Matches | Caveat |
|---|---|---|---|
| Dipo | Nothing approved yet | Not specified | Logo-drop / name-mention only. No result, segment or quote approved. Provide a one-line result to make it real proof (owner, 2026-11-17). |

No other customer name may appear in prospect-facing copy until added here with sign-off.

## Proof caveats

- All impact percentages are Moniepoint self-reported, not independently verified. [customers]
- Onitsha density proves in-person payments reach there; it does not prove loan outcomes. [customers]

## Banned

### Banned angles
- Diagnosing the merchant's business as failing (insult test / iron law 14).
- Investment or financial advice framing. [CLAUDE rules]
- Consumer-wallet positioning (that is OPay/PalmPay territory). [competitors]
- Price/discount framing and guarantees (no "X% approval", no guaranteed amounts).

### Banned words and phrasing (company-specific)
Global list: `knowledge-base/playbooks/copy-bans.yaml`. Company-specific additions:
- No em dashes, anywhere. [CLAUDE rules]
- Do not invent any number, metric or figure. [CLAUDE rules]
- Owner added no company-specific banned words on 2026-11-17 (left blank); global list applies.

### Never in copy, under any circumstance
- Internal transaction data stated as a claim before first-party clearance (see BLOCKER).

## Voice notes

- Register: warm, plain, benefit-led; playful around the "Monie / financial happiness" theme. [brand]
- House phrases (verbatim, from own copy): "financial happiness", "Inclusion + Progress", "power the dreams of SMBs", "Monie moves". [brand]
- Hedges about the prospect: "from what we can see", "looks like", "my guess is".
- Subjects: lowercase, 3 to 5 words, no variables, same subject across the thread.

## CTA ladder

- **Primary:** TODO (owned-channel equivalent, e.g. "Want to see your amount?" / self-serve link). Confirm with lifecycle owner.
- **Secondary (final email):** TODO.
- Never: calendar links or "book a call" in email 1; the word "free".

## Internal only (never in prospect copy)

- Exact eligibility thresholds, credit-model logic, reply rates, funnel metrics.
