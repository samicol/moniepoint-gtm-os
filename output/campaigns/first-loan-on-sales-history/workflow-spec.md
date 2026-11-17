# First Loan on Your Sales History

**Status:** STRUCTURE-APPROVED 2026-11-17 · copy pending

Outbound (cross-sell) workflow spec. Structure only; no copy. Built with `build-workflow-spec` from `context/icp/` (icp, personas, signal-matrix) and `context/docs/gtm-system.md`. This is Workflow A (W1) from `context/icp/signal-matrix.md`: the first-party loan cross-sell.

Note: `context/messaging/facts.md` does not exist yet, so every specific number or claim is a `{{placeholder}}` for `/campaign-copy` to fill from an authorized facts file. Tooling beyond the declared stack (Clay, HubSpot, n8n) is INFERRED.

Section tags: [ENGINE] = reusable; [ICP] = the only part that changes when replicated.

---

## 1. Mother Intent (Trigger) [ENGINE]

An active Moniepoint merchant with a qualifying transaction history who has never taken a Moniepoint loan.

Signal-led and first-party. Catalog match: CRM cross-sell / lookalike-of-customers (the trigger is internal usage, not an external event). Grounds in the research wedge: "75% of entrepreneurs received their first-ever loan from Moniepoint" (`context/docs/research/customers.md`).

## 2. Inclusion / Exclusion [ICP]

**Include:**
- ICP box: Nigeria, MSME merchant, active on Moniepoint payments (any tier). (`context/icp/icp.md`)
- Trigger definition: transacting at or above `{{txn_threshold}}` over the trailing `{{txn_window}}` days (a count), AND loan status = none (boolean).
- Recipient: the registered account owner / primary contact, i.e. the economic buyer. (`context/icp/personas.md`)

**Exclude:**
- Merchants with an active or past Moniepoint loan (already converted).
- Merchants in arrears, default, or flagged credit risk.
- Dormant merchants (below the activity threshold).
- Marketing opt-outs, and anyone contacted in the last `{{suppression_days}}` days (suppression).

## 3. Sources [ENGINE]

All first-party. No external scrape, which is the advantage (clean data, near-zero bounce).
- Trigger + enrichments: Moniepoint transaction ledger / merchant data warehouse to HubSpot. (tooling INFERRED; declared CRM is HubSpot)
- Fields pulled: trailing transaction count and value, transaction trend, tenure, loan status, pre-qualified amount (internal credit model), primary product, outlet count / tier, contact details.

## 4. Signals table [ENGINE]

| # | Signal | Role | How it's read | Output |
|---|---|---|---|---|
| 1 | Active transacting merchant | trigger | count of txns in trailing `{{txn_window}}` >= `{{txn_threshold}}` | boolean |
| 2 | No loan ever / none active | trigger | loan_status enum == none | boolean |
| 3 | Pre-qualified loan amount | router | internal credit model output, banded | enum: Small / Mid / Large |
| 4 | Transaction trend | router | value delta vs prior window, banded | enum: Growing / Steady |
| 5 | Tenure on platform | context-clause | months since onboarding | number |
| 6 | Primary product (POS / transfers / Moniebook) | context-clause | product field | enum |
| 7 | Tier (T2 multi-outlet vs T3 single) | context-clause | outlet count / segment field | enum |

**Routers = two axes:** pre-qualified amount (3 bands) x transaction trend (2 bands) = 6 cells. Amount band sets how much capital the angle may name; trend sets the "why now." Tenure, product and tier are context-clauses and never route.

**Cluster definitions (numbers are placeholders, none invented):**
- Amount: Small `< {{band_1}}` / Mid `{{band_1}}–{{band_2}}` / Large `> {{band_2}}`
- Trend: Growing (value up >= `{{growth_pct}}` vs prior window) / Steady (within band)

## 5. Routing matrix WITH angles [ENGINE]

Routing: 6 cells (amount x trend). Inference stops at what the merchant is doing, not how it feels.

| Cell | Deterministic read | What it tells us (inferred situation) | The angle it earns |
|---|---|---|---|
| Small x Growing | band = Small, value up >= `{{growth_pct}}` | A small merchant whose sales are climbing and who restocks more often than their float comfortably allows; self-funding the climb | A starter loan sized to their rising sales so they can stock up ahead of demand, with the line growing as their sales do |
| Small x Steady | band = Small, trend flat | A steady small merchant running purely on daily takings, no buffer | A first working-capital cushion off takings they already have, to buy stock in bulk or ride a slow week without stalling |
| Mid x Growing | band = Mid, value up >= `{{growth_pct}}` | A growing merchant actively expanding stock or outlets and paying for it out of cash flow | Fund the expansion they are already making with capital priced off their own growing sales, instead of pacing it to match cash |
| Mid x Steady | band = Mid, trend flat | An established merchant with a proven history and credit sitting unused | They have earned a sizeable line on their track record; put it to work on bulk buying or better supplier terms rather than leaving it on the table |
| Large x Growing | band = Large, value up >= `{{growth_pct}}` | A top merchant scaling fast, often multi-outlet, self-funding growth their sales clearly justify | A large facility to fund the next location or big stock order now, matched to how fast they are already growing (if tier = T2, pair with Moniebook for multi-branch) |
| Large x Steady | band = Large, trend flat | A large, stable, high-volume merchant who has never borrowed; strong history, untapped | A substantial line they qualify for on volume alone, to win better supplier pricing or expand on their own terms without touching reserves |

**Branch coverage:** every cell routes on amount band + trend only, both of which exist for all first-party records. `{{prequalified_amount}}` exists in every cell (it is the band). Growing cells may reference the upward trend; Steady cells never claim growth. Context-clauses (`{{tenure_months}}`, `{{primary_product}}`, tier) exist for all records and ride along without routing.

## 6. Variables contract [ENGINE]

| Variable | Source field | Exists in branches |
|---|---|---|
| `{{first_name}}` | contact first name (HubSpot) | all |
| `{{business_name}}` | merchant business name | all |
| `{{prequalified_amount}}` | internal credit model, banded | all |
| `{{tenure_months}}` | months since onboarding | all |
| `{{primary_product}}` | primary product field | all |
| `{{trend_descriptor}}` | transaction trend enum (Growing/Steady) | all (value differs) |
| `{{txn_window}}` | trailing window length | all |
| `{{band_1}}`, `{{band_2}}` | amount band thresholds | all (cluster definition) |
| `{{growth_pct}}` | growth threshold for Growing | Growing cells |

Data-must-exist: copy may only reference a variable listed here. Numbers resolve from `context/messaging/facts.md` when it exists; until then they stay placeholders.

## 7. Cadence & channel [ENGINE]

- **Cadence:** always-on. Eligibility is continuous; merchants enter as they cross the trigger and are suppressed for `{{suppression_days}}` after contact, re-entering only on a materially new signal (new band or trend flip).
- **Channel:** owned channels, because these are existing customers with a relationship: in-app message, email, and SMS/WhatsApp. Not cold email. (channel mix INFERRED; confirm against compliance and the gtm-system reply-handling step)
- **Reply handling / CRM:** per `context/docs/gtm-system.md`, positive replies route to the loan application / self-serve flow; HubSpot logs band, trend, angle, channel and outcome, and holds suppression.

---

## Definition of done (for /campaign-copy GATE 1)

- [x] Mother intent: one sentence, signal-led, catalog-matched
- [x] Inclusion (ICP box + trigger + recipient) and Exclusion
- [x] Sources: trigger + enrichments
- [x] Signals table: every read deterministic, every role declared
- [x] Count clusters declared (amount, trend)
- [x] Routing matrix with angle column complete (6 cells)
- [x] Branch coverage stated
- [x] Variables contract mapped
- [x] Engine/ICP markers on every section
- [x] Cadence & channel declared

## Open questions (carry to copy and launch)

- Whether first-party transaction data can legally/operationally drive outbound cross-sell (the gating question from the signal matrix). INFERRED
- Final channel set and any compliance limits on SMS/WhatsApp to merchants.
- Real values for every `{{placeholder}}` (thresholds, bands, growth %), to live in `context/messaging/facts.md`.

## Next step

`/campaign-copy` reads this file, confirms the angles, and writes the narrative under its own line laws. Any angle flaw gets fixed here and re-approved, never patched inline in copy.
