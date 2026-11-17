# Moniepoint ICP

Scope: the businesses Moniepoint sells to. Every claim traces to a file in `context/docs/research/`. Claims the research does not support are listed under Open questions, not asserted. Source tags: [customers], [company], [signals], [market], [competitors], [voice].

## The five layers

### 1. Firmographic

"Nigerian MSME" is too broad to target: 1.5 million+ businesses already use Moniepoint [customers]. The segments below are ranked by how strong the research evidence is, so a rep knows who to call first.

| Priority | Segment | List-building markers | Why this rank / evidence | Source |
|---|---|---|---|---|
| Tier 1 (beachhead) | Traders in dense physical markets and trading clusters (Onitsha-type) | A stall or shop in a named market; in-person cash trade; often several stalls under one owner | Strongest evidence in the research: Moniepoint "powers two out of three in-person payments" in Onitsha, West Africa's largest market; peer adoption is already high and traders use transaction history to secure fast loans | [customers] |
| Tier 2 | Multi-outlet retail, hospitality or health operators | 2+ locations, branches or stalls under one owner | Moniebook's stated target; fragmented POS and books is the pain. Concrete references: Obinna (4 stalls), Oluremikun (hotel, loan-funded expansion) | [signals], [company], [customers] |
| Tier 3 | Single-outlet micro and small merchants in retail, hospitality or health | One shop; cash-heavy or already on a POS; informal sector | The core base, but least differentiated: highest volume, lowest targeting signal, so call last | [customers], [competitors] |

Discriminator across all tiers: Nigeria, in-person / in-store trade, cash-heavy or already running a POS. [company], [customers]

Note: research gives no revenue or employee-count thresholds, so tiers use outlet count and market context, not size bands. Tier ranking is a sales-prioritisation judgment based on evidence strength, not a figure from the research. See Open questions.

### 2. Technographic

| Attribute | Fit | Source |
|---|---|---|
| Payments today | Cash-heavy trade, or already running a POS terminal | [customers], [signals] |
| Likely current setup | Agency-banking / in-store POS; may accept online payments via a gateway | [company] |
| Software gap | Multi-location merchants lacking a unified POS + bookkeeping system (Moniebook's stated target: retail, hospitality, health) | [signals], [company] |
| Data footprint | Has (or can build) a digital transaction history, which Moniepoint uses to underwrite fast loans | [customers], [signals] |

### 3. Intent signals

| Signal | Why it indicates need | Source |
|---|---|---|
| Never accessed formal credit | Moniepoint's wedge is first-time lending off transaction data | [customers], [signals] |
| High cash volume / cash-handling risk | Cash-heavy trade carries theft and reconciliation risk that digital payments reduce | [signals], [customers] |
| Multi-location without unified POS + bookkeeping | Matches Moniebook's target buyer | [signals] |
| Facing a CBN compliance deadline | Data localisation (Jan 2027), POS geo-tagging (from Apr 2026), AML roadmap create pressure to be on a compliant partner | [market], [signals] |
| Growth stage needing working capital | Loan-funded expansion and renovations are the documented use case (e.g. Oluremikun) | [customers] |

### 4. Persona (buying unit)

| Role | Who | Source |
|---|---|---|
| Owner-operator | For micro/small merchants, usually one person is champion, buyer and user | [customers] |
| Operations / store manager | Separates out at multi-outlet businesses (Moniebook's multi-location target) | [signals] |
| Finance / accounting (or cashier) | Handles reconciliation and books at larger merchants | [signals] |

Detail in [personas.md](personas.md).

### 5. Engagement readiness (highest to lowest)

| Readiness | Marker | Source |
|---|---|---|
| Hot | Already has a digital transaction history and is seeking credit for the first time | [customers], [signals] |
| Hot | Multi-outlet merchant feeling the pain of fragmented POS + books | [signals] |
| Warm | Cash-heavy business newly exposed to cash risk or a compliance deadline | [market], [signals] |
| Warm | Growth-stage business planning expansion or renovation needing working capital | [customers] |

## Who is NOT a fit (and why)

| Not a fit | Why | Source |
|---|---|---|
| Large enterprise / big-account buyers | No enterprise or mid-market customers found; positioning is SMB/MSME-led | [customers] |
| Businesses outside Nigeria / core African markets | ~90% of business is Nigeria; the UK diaspora play (MonieWorld) is reportedly being wound down toward core African markets | [company], [signals] |
| Merchants with no digital footprint and unwilling to digitize | The credit wedge depends on transaction-history underwriting | [customers], [signals] |
| Pure online-only / cross-border B2B that wants a payments brand like Flutterwave | Moniepoint's strength and reference customers are in-store / in-person payments | [competitors], [customers] |

## Open questions (research does not yet support)

- Revenue / employee-count bands to segment micro vs small vs mid merchants. [not in research]
- Which POS hardware or bookkeeping tools target merchants use today (to size switching cost). [not in research]
- Whether personal-banking (consumer) customers should be a separate ICP; research notes the push but not a defined segment. [company]
- Independent verification of the impact percentages used as intent evidence; all are Moniepoint self-reported. [customers]
