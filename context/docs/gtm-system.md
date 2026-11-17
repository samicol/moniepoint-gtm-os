# Moniepoint Outbound GTM System

**Miro board:** https://miro.com/app/board/uXjVEMyzRWs=/ (flow chart of this system, built from `context/docs/gtm-system.flowchart.json`).

End-to-end design of the outbound motion, built from `context/icp/icp.md`, `context/icp/personas.md` and `context/icp/signal-matrix.md`. Source tags: [icp], [personas], [matrix] point to those files. INFERRED marks tooling or logic not fixed by those files (the declared stack is Clay, HubSpot, n8n per CLAUDE.md; sourcing/sending tools come from the signal matrix and skills, and specific vendors below are reasoned choices to confirm).

## Scope and honest boundary

This system is the **programmatic** outbound motion. It serves the segments that are reachable by data and channel: Tier 2 (multi-outlet operators), the online-merchant slice, and Moniepoint's first-party base. **Tier 1 dense-market traders are deliberately routed OUT of this system to a field-agent motion**, because informal traders have little digital footprint and are won by agents and peer density, not Clay and email. [matrix], [icp] This boundary is enforced at the ICP fit check (Step 4).

The pipeline runs in order. Each step says what happens, the tool, and every decision with where each answer leads.

---

## Step 0: The Context OS (foundation)

**What happens:** The `context/` folder is the single source of truth every step reads from: `icp.md` (tiers, discriminator, not-a-fit), `personas.md` (who to find, their pains and objections), `signal-matrix.md` (which signals, tools, scores), plus research and positioning. Nothing downstream invents targeting; it reads these files.

**Tool:** Git-versioned Markdown in this repo (GitHub = source of truth). Clay/HubSpot/n8n configs reference it.

**Decisions:**
- Is the target definition observable and filterable? Yes leads to build a workflow. No leads back to refine `icp.md` first. [icp]
- Does a signal already have a verified status in `signal-matrix.md`? Yes leads to Step 1. No (or KILLED) leads to leave it out until validated. [matrix]

---

## Step 1: Buying signals (always-on triggers)

**What happens:** Each workflow starts from a signal, not a static list (signal-first, then ICP filter). The five build-first signals from the matrix each run on a schedule. [matrix]

**Tool:** n8n schedules the runs; Clay tables hold each signal's build.

**Decisions (which signal fired routes the whole workflow):**
| Signal | Leads to sourcing path (Step 2) |
|---|---|
| W1 First-party: active merchant, no loan yet | Internal data path (cross-sell lifecycle, not cold) |
| W2 New branch / outlet opening | Google Places delta path |
| W3 Uses competitor gateway (Paystack/Flutterwave) | Checkout-script path |
| W4 Newly registered business (CAC) | CAC registry path |
| W5 Multi-outlet hiring | Job-board path |

Velocity sets frequency: first-party continuous; CAC and Places weekly; hiring weekly; competitor-gateway monthly. INFERRED from signal velocity in workflow-anatomy.

---

## Step 2: Finding companies

**What happens:** The fired signal pulls a raw company list from its source.

**Tool by path:**
- First-party: Moniepoint transaction data to HubSpot. [matrix] (tooling INFERRED)
- Google Places delta: Google Places API via Clay HTTP or Apify. [matrix]
- Competitor gateway: BuiltWith / Wappalyzer scan of the /checkout page via Clay. [matrix]
- CAC: Apify CAC actor (search.cac.gov.ng) via Clay HTTP. [matrix]
- Hiring: Jobberman / LinkedIn Jobs / Indeed NG via Apify into Clay. [matrix]

**Decisions:**
- Did the source return a usable company identity (name + domain or location)? Yes leads to Step 3. No leads to park the row (retry next run) or drop.
- Is this already a Moniepoint customer (domain/name match against HubSpot)? Yes leads to route to first-party lifecycle (W1), suppress from cold. No leads to continue as new-logo. (This is the first clean-data gate.)

---

## Step 3: Enrichment

**What happens:** Each company is enriched to the fields the fit check and routing need: firmographics, outlet count, tech stack, registration, contactability.

**Tool:** Clay enrichment waterfall. Google Places for outlet count; BuiltWith for gateway; CAC for registration type (RC vs BN); Apollo/Clay for size and industry.

**Decisions:**
- Enough data to classify the tier (outlet count, industry, in-person vs online)? Yes leads to Step 4. No leads to one more enrichment pass, then drop if still unknown (do not guess the tier).
- Is the data fresh (listing active, site live)? Yes leads to continue. No (closed/dead) leads to drop.

---

## Step 4: ICP fit check (the gate)

**What happens:** Apply the `icp.md` discriminator and not-a-fit list. This is a hard gate: fails exit the system.

**Tool:** Clay conditional columns (pass/fail), enforced before any person is sourced.

**Decisions (each "no/at-risk" exits):**
| Check | Pass | Fail leads to |
|---|---|---|
| In Nigeria / core market? | continue | DROP (outside core market) [icp] |
| SMB/MSME, not large enterprise? | continue | DROP (no enterprise fit) [icp] |
| In-person/in-store or online merchant, cash-heavy or on a POS? | continue | DROP (wrong buyer) [icp] |
| Has a reachable digital footprint? | continue to Step 5 | ROUTE OUT to field/agent queue (Tier 1 behaviour), not outbound [icp], [matrix] |

---

## Step 5: Routing by segment

**What happens:** Passing companies are routed to a tier + angle + lead product, from Matrix 1 and the signal that fired.

**Tool:** Clay routing (segment column) writing the angle/product; HubSpot holds the assignment.

**Decisions (tier and signal set the angle, Matrix 1):**
| Tier / slice | Lead product | Angle (champion-facing) |
|---|---|---|
| Tier 2 multi-outlet | Moniebook + working capital | One system for payments and books across every branch [matrix] |
| Online merchant (W3) | Monnify | You already take online payments; here is why merchants add Monnify [matrix] |
| Tier 3 single-outlet | Account + POS + first loan | Take card and transfer, get your first loan off your sales [matrix] |
| First-party (W1) | Credit / Moniebook cross-sell | Based on your sales, you qualify (lifecycle, not cold) [matrix] |
| Tier 1 | (field motion) | Exited at Step 4 |

Secondary enrichments (2 to 4) stack here to pick the narrative route: outlet count, gateway, registration recency, hiring. [personas], workflow-anatomy.

---

## Step 6: Finding people

**What happens:** Find the buying unit for the routed segment, by persona. [personas]

**Tool:** Apollo / Prospeo / LinkedIn Sales Navigator via Clay. (vendor mix INFERRED)

**Decisions:**
- Is this a single-owner micro business (Tier 3)? Yes leads to find the owner only (roles collapse). [personas]
- Multi-outlet (Tier 2)? Yes leads to find champion (ops/store manager) + economic buyer (owner/MD) + influencer (accountant). [personas]
- No contactable person found digitally? Leads to LinkedIn-only attempt, then route out to field if still none.

---

## Step 7: Finding and verifying emails

**What happens:** Get a deliverable email per contact, then verify it before any send (protects sender reputation).

**Tool:** Clay email waterfall (Prospeo / Findymail / Datagma) then verification (MillionVerifier / ZeroBounce) via Clay. (vendors INFERRED)

**Decisions:**
| Email result | Leads to channel (Step 8) |
|---|---|
| Found + valid | Email + LinkedIn (full multichannel) |
| Catch-all / risky | LinkedIn-first, email as secondary only after warm-up |
| Not found | LinkedIn-only; if no LinkedIn either, route out to field or drop |

Clean-data rule: never send to unverified or catch-all without downgrading the channel. [pillar: clean data]

---

## Step 8: The sequence (email + LinkedIn)

**What happens:** A multichannel cadence runs, with copy routed by the signal combination (narrative routing). Copy itself is written by `/campaign-copy` off an approved spec; this system defines the structure, not the words.

**Tool:** Email via Instantly or PlusVibe; LinkedIn via a LinkedIn automation tool or manual SDR touches; orchestration in n8n. (sending stack from campaign-qa skill; LinkedIn tool INFERRED)

**Decisions (narrative route by signal):**
- Competitor gateway (W3)? Leads to "switch from Paystack/Flutterwave" template. [matrix]
- New branch (W2)? Leads to "expansion / unify your branches" template.
- New registration (W4)? Leads to "welcome, here is your account + POS" template.
- Hiring (W5)? Leads to "you are expanding" template.
- No secondary signal? Leads to fallback template (tier angle only).

Cadence decision: reply at any step leads to Step 9 and suppress remaining steps. No reply after final step leads to mark nurture, re-enter only on a new signal (dedup/suppression). [pillar: clean data]

---

## Step 9: Reply handling

**What happens:** Every reply is classified and actioned. Given SMB scale, positive replies can go to self-serve onboarding rather than always booking an AE.

**Tool:** n8n + an AI classifier; HubSpot logs the outcome; a human reviews positives. (classifier INFERRED)

**Decisions:**
| Reply type | Leads to |
|---|---|
| Positive / interested | Self-serve onboarding link, or book a rep for Tier 2 larger accounts |
| Objection | Objection-handling reply from `personas.md` (cost, trust, switching) [personas] |
| Referral ("talk to my accountant") | Re-route to the influencer/economic buyer persona |
| Not now | Nurture, re-enter on next signal |
| Negative / unsubscribe | Suppress permanently [pillar: clean data] |
| Out of office | Pause, resume after return date |

---

## Step 10: The CRM

**What happens:** HubSpot is the system of record. Every company, contact, signal, segment, angle, channel, reply and outcome is written back. It also holds the master suppression and the existing-merchant list.

**Tool:** HubSpot (CRM per CLAUDE.md), synced from Clay and n8n.

**Decisions:**
- New or existing record (dedupe on domain/name/phone)? Existing leads to update + suppress from cold (lifecycle instead). New leads to create. [pillar: clean data]
- Is the contact an existing Moniepoint merchant? Yes leads to first-party lifecycle (W1), never cold outbound.
- Lifecycle stage change (replied, meeting, onboarded, closed)? Updates stage and triggers reporting.

---

## Step 11: Weekly feedback loop (back into the Context OS)

**What happens:** Once a week, per-workflow metrics are reviewed and the Context OS files are updated, closing the loop to Step 0.

**Tool:** HubSpot reporting + manual review; edits committed to `context/icp/*` in Git.

**Decisions per signal/workflow:**
| Metric read | Decision | Leads to |
|---|---|---|
| Positive-reply and onboarding rate high | Signal works | Scale volume; keep status VERIFIED in `signal-matrix.md` |
| Reply rate low, data clean | Angle weak | Iterate copy/angle; log in `learnings/` |
| Bounce high / data dirty | Data problem | Fix enrichment or verification; tighten gate |
| Dead after fair trial | Kill | Mark KILLED in `signal-matrix.md` with reason |
| New objection or pain heard in replies | Capture VoC | Update `personas.md` (fixes the one-quote gap) and `icp.md` |

This is the only step that writes back to the Context OS. New verbatim pains collected here replace the paraphrased persona pains flagged in `personas.md`.

---

## Four-pillar check

| Pillar | Where it lives in the system | Gaps / risks |
|---|---|---|
| **Clean data** | Existing-merchant dedupe (Steps 2, 10); hard ICP gate (Step 4); email verification with channel downgrade (Step 7); suppression on negative/unsubscribe (Steps 8, 9); CAC/Places as authoritative sources | Nigerian contact data is thinner than US; catch-all rate may be high, so LinkedIn-first fallback matters. INFERRED |
| **Always-on signals** | n8n schedules every signal (Step 1); first-party continuous; Places/CAC/hiring weekly; competitor-gateway monthly | Tier 1 has no always-on digital signal (field motion); first-party automation assumed, not confirmed [matrix] |
| **Composable workflows** | Universal builds (CAC, Places, hiring) reused across tiers by keyword swap; one Clay build spawns many campaigns; angle/product change per cell, structure stays (Matrix 1) | Competitor-gateway and first-party are more bespoke builds, less reusable |
| **Tight feedback loops** | Weekly review (Step 11) writes back to `signal-matrix.md`, `personas.md`, `icp.md`; kills/promotes signals; captures VoC | Loop depends on disciplined weekly cadence and logging to `learnings/`; no automated metric-to-file sync (manual) |

**Verdict:** The system satisfies all four pillars for Tier 2, online merchants and first-party. The known structural gap is Tier 1: the largest segment by count sits outside the programmatic pillars by design and needs a parallel field-agent system, which is out of scope here. [matrix], [icp]

---

## Open questions

- Can first-party transaction data legally and operationally drive outbound cross-sell? Assumed yes. INFERRED
- Confirm the sending/verification/LinkedIn vendors (Instantly vs PlusVibe, verification tool, LinkedIn automation). INFERRED
- Whether positive SMB replies should self-serve or always route to a rep (volume vs touch). INFERRED
- Real per-signal volumes, still directional from the matrix. [matrix]
