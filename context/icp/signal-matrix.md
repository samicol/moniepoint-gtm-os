# Moniepoint Signal Matrix

Work in progress, for strategic alignment. Built with the signal-matrix framework (`knowledge-base/playbooks/signal-matrix-framework.md`) and the Mother Intent Catalog (`knowledge-base/playbooks/workflow-anatomy.md`). Inputs: `context/icp/icp.md`, `context/icp/personas.md`, `context/docs/research/`.

Source tags point to the research file that supports a claim: [customers], [company], [signals], [market], [competitors], [voice]. INFERRED marks anything the research does not support, including the entire outbound tooling layer (the research files describe Moniepoint the company, not its outbound data stack, so every data source and tool in Matrix 2 is a reasoned choice, not a research fact; two were spot-checked, noted inline).

## Reality check before the matrices

Moniepoint's cheapest, highest-volume segment (Tier 1 dense-market traders) is mostly unreachable by programmatic email or LinkedIn outbound: informal traders have little digital footprint. That segment is won by field agents and peer density, not Clay. The programmatic signal matrix is therefore strongest for Tier 2 (multi-outlet operators) and the online-merchant slice, plus Moniepoint's own first-party transaction data, which is the single biggest advantage. This is INFERRED from the informal-sector focus [competitors], [customers] and standard data-availability realities for emerging-market SMBs.

---

## Matrix 1: Segments x Personas (the angle per cell)

Rows = ICP tiers from `icp.md`. Columns = personas from `personas.md`. For micro merchants (Tier 1 and Tier 3) the three roles usually collapse into one owner-operator [customers], so the influencer column there is marked INFERRED.

| Segment | Champion (owner-operator / ops or store manager) | Economic buyer (owner / MD) | Influencer (cashier / bookkeeper / accountant) |
|---|---|---|---|
| **Tier 1: Dense-market traders (Onitsha-type)** | Your neighbours in the market already take card and transfer and get loans off their sales, stop losing sales when a customer has no cash. [customers], [signals] | Turn your daily takings into a track record that gets you fast stock-up loans when prices move. [customers] | Close out the day's money without counting cash by hand. [signals] INFERRED (role rarely separate here) |
| **Tier 2: Multi-outlet retail / hospitality / health** | One system for payments and books across every branch, instead of reconciling each location by hand. [signals], [company] | Fund your next location with working capital built on your own sales, the way a Lagos hotel owner did. [customers] | Payments and bookkeeping in one place, so month-end across branches stops being manual. [signals] |
| **Tier 3: Single-outlet micro / small merchants** | Take card and transfer, get your first business loan off your sales, run it all from one app. [customers] | Your first formal business loan, priced off what you actually sell, not collateral. [customers] | Faster checkout and fewer payment disputes at the counter. [customers] INFERRED (role often the owner) |

Note: angles are message hypotheses in buyer language, to validate with sales. Pain language is drawn from research narratives, not verbatim customer quotes (only one verbatim quote exists: Mr Collins, "Moniepoint isn't scared to support me" [customers]).

---

## Matrix 2: Buying signals per segment

Each signal is scored on the four mother-intent tests from `workflow-anatomy.md` (the user's four tests): **Reason** (clear buying reason), **Volume** (enough of them), **Data** (data you can actually get), **Story** (natural narrative). Scale: High / Med / Low. Status follows the Iron Law: VERIFIED, VERIFIED (COMPOUND), VERIFIED (PARTIAL), or KILLED.

All data sources and tools below are INFERRED (not in the research). Two were spot-checked on 2026-11-17: CAC public search exists at search.cac.gov.ng with Apify scraper actors available; BuiltWith tracks Paystack (~11,300 live sites) and Flutterwave, though checkout gateways need a cart/checkout-page scan, not homepage-only.

### Tier 2: Multi-outlet retail / hospitality / health (primary programmatic cell)

| Signal | Mother intent | Data source | Tool | Reason | Volume | Data | Story | Status |
|---|---|---|---|---|---|---|---|---|
| New outlet / branch opening | Expansion / new location | Google Places new-listing delta | Google Places API via Clay HTTP or Apify | High | Med | Med | High | VERIFIED (PARTIAL) |
| Operates 2+ locations (footprint count) | Lookalike / ICP physical identifier | Google Maps location count under one brand | Google Places API via Clay | High | Med | Med | Med | VERIFIED (COMPOUND, pair with a timing signal) |
| Hiring branch/store/restaurant staff | Hiring specific roles / hiring velocity | Jobberman, LinkedIn Jobs, Indeed NG | Apify / Clay "Find Jobs" | Med | Med | Med | High | VERIFIED (PARTIAL, formal employers only) |
| Newly registered multi-owner company | Recently incorporated | CAC public search (search.cac.gov.ng) | Apify CAC actor / Clay HTTP | Med | High | Med | High | VERIFIED |

### Online-merchant slice (cuts across Tier 2/3)

| Signal | Mother intent | Data source | Tool | Reason | Volume | Data | Story | Status |
|---|---|---|---|---|---|---|---|---|
| Uses a competitor gateway (Paystack / Flutterwave) at checkout | Competitor customers / technographic | Checkout-page script detection | BuiltWith / Wappalyzer via Clay (scan /checkout) | High | Med | High | High | VERIFIED (pitch Monnify) [competitors]; Paystack-as-rival is INFERRED |

### Tier 3: Single-outlet micro / small merchants

| Signal | Mother intent | Data source | Tool | Reason | Volume | Data | Story | Status |
|---|---|---|---|---|---|---|---|---|
| Newly registered business name (BN) | Recently incorporated | CAC public search (BN filings) | Apify CAC actor / Clay HTTP | High | High | Med | High | VERIFIED |
| Single storefront on Google Maps, no card-payment note | Physical-world greenfield | Google Places listing attributes | Google Places API via Clay | Med | High | Low | Med | VERIFIED (PARTIAL, contactability weak) |

### Tier 1: Dense-market traders (field motion, not programmatic)

| Signal | Mother intent | Data source | Tool | Reason | Volume | Data | Story | Status |
|---|---|---|---|---|---|---|---|---|
| Trader in a named market / trade cluster | Niche physical / peer density | Market and trade-association directories; physical mapping | Field agents; Apify where directories exist | High | High | Low | High | VERIFIED (PARTIAL, agent-led not email) [customers], [signals] |
| Compliance pressure on POS agents | Regulatory change (timing overlay) | CBN circulars (geo-tagging from Apr 2026) | Narrative hook, not a list-builder | Med | High | Low | Med | VERIFIED (PARTIAL) [market] |

### First-party (strongest, cuts across all tiers)

| Signal | Mother intent | Data source | Tool | Reason | Volume | Data | Story | Status |
|---|---|---|---|---|---|---|---|---|
| Active Moniepoint merchant with no loan yet / rising transaction volume | Lookalike / CRM cross-sell | Moniepoint's own transaction data | Internal data to HubSpot | High | High | High | High | VERIFIED (first-party) [customers], [signals]; tooling INFERRED |

### Signals considered and KILLED (framework guardrails applied)

| Signal | Why killed |
|---|---|
| Fundraising / recent funding | Micro and informal merchants do not raise VC; Crunchbase returns nothing for this base. Framework kills fundraising in non-VC SMB markets. [competitors] |
| Backend technographics (POS/ERP detection) | BuiltWith cannot see backend tools; only web-facing checkout scripts are usable (see online-merchant signal). |
| New-leadership / C-suite change | Volume too low for owner-run SMBs; decision-maker rarely changes. INFERRED |

---

## Top signals to build first (ranked by the four tests)

1. **First-party: active merchants with no loan yet.** Highest volume, best data (Moniepoint already holds the transaction history), clearest reason, and the most natural story, "based on your sales, you qualify." It is the research's own wedge: "75% of entrepreneurs received their first-ever loan from Moniepoint" [customers]. Cross-sell, not new-logo, but the strongest play on every test.
2. **New outlet / branch opening (Google Places delta) for Tier 2.** A true timing signal (not a static attribute) and the framework's "physical-world alpha" in a weak-data market. Routes to Moniebook plus working capital. [signals], [company]
3. **Competitor-gateway merchants (Paystack/Flutterwave at checkout).** Best data quality of any new-logo signal (web-facing, verifiable) and a clear switch reason: they already accept online payments, so pitch Monnify. [competitors]
4. **Newly registered businesses (CAC).** High volume and greenfield, with a natural "congrats on registering, here is your business account and POS" opener. Verified public source. [company]
5. **Hiring/expansion at multi-outlet retail/hospitality/health (Jobberman/LinkedIn).** Medium volume but a strong expansion story for Tier 2 Moniebook; universal build (keyword swap off signal 2's segment).

Deliberately NOT in the build-first list: Tier 1 market-trader acquisition. It is the biggest segment by count but is a field-agent and peer-density motion, not a programmatic email/Clay workflow, so it does not fit an outbound build sprint. Serve it with physical signals and agents instead. [customers], [signals] INFERRED

---

## Matrix 3: Workflow tracker (pre-filled, Planned)

| W # | Status | Workflow Name | Mother Intent | Segment |
|---|---|---|---|---|
| W1 | Planned | First loan on transaction history | Lookalike / CRM cross-sell | All tiers (first-party) |
| W2 | Planned | New branch opening | Expansion / new location | Tier 2 |
| W3 | Planned | Switch from competitor gateway | Competitor customers | Online merchants |
| W4 | Planned | Just registered with CAC | Recently incorporated | Tier 2 / Tier 3 |
| W5 | Planned | Multi-outlet hiring | Hiring specific roles | Tier 2 |

All other tracker columns (campaigns, launch date, Clay URL, copy URL, leads, bounce) are filled as campaigns launch, per the framework.

---

## Open questions

- Whether Moniepoint's first-party data can legally and operationally feed outbound cross-sell (assumed yes; not in research). INFERRED
- Real volume estimates per signal in the Nigerian market; none are in the research, so Volume scores are directional. INFERRED
- Verbatim buyer pain language for the angles (only one quote exists). [customers]
- Confirm Wappalyzer/BuiltWith fingerprint coverage for Paystack and Flutterwave by testing a known merchant's checkout page.
