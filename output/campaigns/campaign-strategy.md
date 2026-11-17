# Campaign Strategy for Moniepoint

Generated with the campaign-strategy skill from `CLAUDE.md`, `context/` (icp, personas, signal-matrix, positioning, messaging, case-studies, research) and `knowledge-base/playbooks/workflow-anatomy.md`. Every claim traces to a context file. Tags: [icp], [personas], [matrix], [customers], [company], [competitors], [market], [voice].

**Core value proposition:** reliable in-person payments, and a merchant's first loan built on their own sales. [positioning], [customers]
**Market reality carried from the signal matrix:** Tier 1 dense-market traders are the heartland by count but are won by field agents, not programmatic email. Programmatic outbound is strongest for Tier 2 (multi-outlet), the online-merchant slice, and Moniepoint's first-party base. [matrix]

Volumes below are **directional bands (High / Med / Low), not counted figures** (house rule: never invent numbers). The only hard anchors are sourced: 1.5M+ businesses [customers] and ~11,321 live Paystack sites per BuiltWith [matrix].

---

## Customer Discovery Analysis

| Customer | Industry | Size | Problem | Result | Source |
|---|---|---|---|---|---|
| Oluremikun | Hospitality (hotel), Lagos | Not found | Needed capital to expand/renovate | Expanded with a working-capital loan | [customers] |
| Mr Collins | Beverage, Onitsha | Not found | Needed trade support/credit | "Moniepoint isn't scared to support me" | [customers] |
| Obinna (Obaino Fabrics) | Textiles, Onitsha (4 stalls) | Micro/small | Runs multi-stall market business | Operates 4 stalls | [customers] |
| Chukwuka | Market trade, Onitsha | Not found | Took over late father's business | Runs it on digital payments | [customers] |
| Okeke Desmond (DMAX shoes) | Shoemaking, Benin City | Not found | Building a business as a wheelchair user | Runs DMAX shoes | [customers] |
| Joseph | Provision store, Akwa Ibom | Not found | Recovery story | Business success | [customers] |

**Patterns:** all are informal or semi-formal physical merchants; the repeated wins are payments reliability and first-time credit. [customers]
**Targeting challenge:** the case studies confirm the informal heartland, but they are field-won, and none carry firmographic detail to build a clean programmatic lookalike. Lookalikes work better one layer up, at the semi-formal multi-outlet merchants (hotels, multi-stall traders, retail chains) that do have Google Maps and registry footprints. [matrix], [customers]
**Best lookalike seeds:** the hotel (hospitality, multi-location) and Obaino Fabrics (multi-stall textile trader). Note: copy may only name a customer once it is authorized in `context/messaging/facts.md` (which does not exist yet), so names stay `{{placeholder}}` for now.

---

## Campaign Ideas (ranked within tiers; broad to niche)

| # | Campaign | Targeting | Mother Intent | Segment + Persona | Signal + Data Source | Angle | Volume/mo | Difficulty | Tier |
|---|---|---|---|---|---|---|---|---|---|
| 1 | First Loan on Your Sales | Broad | Lookalike / CRM cross-sell | All tiers / owner (economic buyer) | Active merchant, no loan yet; Moniepoint transaction data (first-party) | Based on your sales, you qualify for your first loan | High (base 1.5M+ [customers]) | Low* (gated on data-use OK) | Tier 1: best data, highest volume, proven wedge |
| 2 | Just Registered with CAC | Focused | Recently incorporated | Tier 2/3 / owner | New BN/RC filing; CAC public search via Apify | Congrats on registering; here is your account and a 48-hour POS | High | Low-Med | Tier 1: high volume, public source, greenfield |
| 3 | Switch Your Gateway | Focused | Competitor customers | Online merchants / owner + dev | Paystack/Flutterwave at checkout; BuiltWith/Wappalyzer /checkout scan | You already take online payments; add Monnify, pay only on success | Med (~11,321 Paystack sites global [matrix]) | Med | Tier 1: web-facing data, clear switch reason |
| 4 | You Opened Another Branch | Focused | Expansion / new location | Tier 2 / ops manager + owner | New Google Places listing under an existing brand; Places API via Clay | Unify payments and books across branches; fund the next one off your sales | Med (fresh) | Med | Tier 2: true timing signal, Places noisy |
| 5 | Multi-Outlet Operators | Focused | Lookalike of customers | Tier 2 / owner | 2+ Google Maps locations under one brand; Places API | One system for every branch (Moniebook + working capital) | Med | Med | Tier 2: needs a timing pair |
| 6 | Hiring to Expand | Focused | Hiring specific roles / hiring velocity | Tier 2 / owner + ops manager | Multiple open store/branch/restaurant roles; Jobberman, LinkedIn Jobs, Indeed NG via Apify | You are expanding; capital and one system to run the new sites | Med (formal employers) | Med | Tier 2: formal-sector only |
| 7 | New Ops/Finance Manager (New Hire) | Focused | New leadership (past 90 days) | Tier 2 / champion + influencer | Started in role <90 days at a multi-outlet merchant; LinkedIn/Apollo job-change | New in the role: get payments and books on one system fast | Low-Med | Med | Tier 2: low volume, reliable signal |
| 8 | Dormant Merchant Reactivation | Focused | Closed lost reactivation | First-party / owner | Previously active merchant now below threshold; internal data | Your terminal is quiet; here is what is new and a reason to come back | Med-High | Low* (first-party) | Tier 1: owned data, warm |
| 9 | Lookalike: Hotels & Guesthouses | Focused | Lookalike of customers | Tier 2 hospitality / owner | Hospitality category on Google Maps; Places API | Hotels like {{case_study}} funded renovations off their sales | Med | Med | Tier 2: category source clean, copy name gated |
| 10 | Lookalike: Market Textile Traders | Niche | Lookalike of customers | Tier 1/2 textile traders / owner | Named textile markets/lines; market directories + field | Traders like {{case_study}} stock up faster with credit on their sales | Med (aggregate) | High (part field) | Tier 3: mostly field-reachable |
| 11 | Seasonal Stock-Up | Focused | Niche-specific play (timing) | First-party + Tier 2/3 / owner | Pre-festive window + eligible merchant; internal data + calendar | Stock up for the season now with a loan off your sales | High (seasonal) | Low* (first-party) | Tier 2: timing overlay on signal 1 |
| 12 | Low Ratings, Slow Checkout | Niche | Niche-specific play (reviews) | Tier 2 retail/hospitality / owner | Google reviews mentioning queues/payment issues; reviews scrape | Faster checkout and fewer payment disputes at your counter | Med | Med-High | Tier 3: review mining is fiddly |
| 13 | Cards-Only Online Stores | Niche | Competitor customers / technographic | Online merchants / owner | Checkout takes cards but not local transfer; checkout scan | Add bank transfer and local methods your buyers prefer, via Monnify | Low-Med | Med | Tier 3: narrower slice |
| 14 | New Plaza / Market Opening | Niche | Niche-specific play (physical) | Tier 2/3 tenants / owner | New shopping complex/market opens; news + Places | Onboard the whole plaza: every tenant paid from day one | Low-Med | High | Tier 3: hard to detect at scale |
| 15 | Creative Ideas (base ICP) | Broad | Niche-specific play | Tier 2/3 / owner | Base merchant list; website/Google Maps analysis | I had an idea for {{business}}: three ways to get paid and grow | High | Med (contactability) | Tier 2: no signal, needs strong AI |
| 16 | Creative non-ICP: Accountants & Bookkeepers | Focused | Niche-specific play (partner) | Non-ICP adjacent / accountant (influencer) | Accounting/bookkeeping firms serving MSMEs; LinkedIn + directories | Put your SME clients on Moniebook; cleaner books, you look good | Med | Med | Tier 2: referral channel, fresh audience |
| 17 | Creative non-ICP: Market & Trade Associations | Focused | Niche-specific play (partner) | Non-ICP adjacent / association lead | Market unions and trade associations; directories | Get your members paid and funded; a bridge into the field motion | Low-Med | Med | Tier 2: partner path into Tier 1 |
| 18 | Compliance Deadline Watch | Broad | Regulatory changes | POS agents + merchants / owner | CBN deadlines (POS geo-tagging Apr 2026, data localisation Jan 2027); market-wide | Stay compliant on a partner built for the new rules | High (as overlay) | High (not a list) | Tier 3: timing hook, not a list-builder |

\*Low difficulty on first-party campaigns assumes the open question is cleared: whether first-party transaction data can legally/operationally drive outbound. [matrix]

### Required campaign types (coverage check)
- **Creative Ideas:** #15. **New Hire:** #7. **Lookalike:** #9 and #10. **Creative (non-ICP):** #16 and #17.

---

## Ranked by signal strength + data ease (build order)

1. **#1 First Loan on Your Sales** — strongest signal, in-house data, near-zero bounce (clear data-use first).
2. **#2 Just Registered with CAC** — high volume, public verified source, clean greenfield story.
3. **#3 Switch Your Gateway** — best external data quality, clear switch reason.
4. **#8 Dormant Reactivation** — owned data, warm, low lift.
5. **#4 You Opened Another Branch** — genuine timing trigger, Places data gettable.

These five are the Tier 1 / strong Tier 2 shortlist. Everything below depends on noisier data (reviews, physical mapping) or is a timing overlay.

---

## No-AI campaign

**48-Hour POS, No Upfront Cost** (to newly registered CAC businesses, #2 list)
- Why it works without AI: the offer is the whole message. A just-registered business needs to get paid; a terminal delivered in 48 hours with no upfront cost is a concrete, static promise. [company]
- Core message: You just registered {{business}}. Get a Moniepoint POS delivered in 48 hours, no upfront cost, and start taking card and transfer this week. (Delivery-in-48-hours and no-upfront-registration claims are from the research; confirm current terms before send. [company])

---

## Front-end offer suggestions

1. **Free pre-qualified loan amount.** Show an eligible merchant the figure they already qualify for off their sales. It delivers value before any pitch and is the natural top of #1. [customers]
2. **48-hour POS trial / fast onboarding.** Let a new merchant experience getting paid this week. [company]
3. **Moniebook setup for one branch.** Prove the unified payments-and-books value at a single location before a multi-branch rollout. [company]

---

## Next step

Pick one Tier 1 idea and run `/build-workflow-spec`. #1 (First Loan on Your Sales) is already specced at `output/campaigns/first-loan-on-sales-history/workflow-spec.md`; the natural next builds are #2 (CAC) or #3 (gateway switch). Do not build all 18 at once: build one, launch, learn, then pick the next. Note that `context/messaging/facts.md` is still missing, so any copy step will run on placeholders until it exists.
