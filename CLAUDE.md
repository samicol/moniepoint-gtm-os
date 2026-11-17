# CLAUDE.md

GTM Context OS for Moniepoint. In-house GTM team workspace.

## Company

Moniepoint (moniepoint.com): a global business payments and banking platform, Nigeria's largest merchant acquirer, serving over 1.5 million businesses with payments, POS/agency banking, credit and bookkeeping; mission is "financial happiness." (Sources in `context/docs/research/`.)

Key context files:

- ICP: `context/icp/icp.md`
- Personas: `context/icp/personas.md`
- Research: `context/docs/research/` (company, customers, competitors, market, signals, voice)

## How this folder works

- `context/icp/`: ideal customer profiles and segments. Read before targeting or messaging work.
- `context/positioning/`: category, differentiation, competitive framing. Read before messaging or campaigns.
- `context/messaging/`: value props, pillars, proof points, copy blocks. Read before writing any external copy.
- `context/brand-kit/`: voice, tone, colours, logos, visual rules. Read before producing any branded asset.
- `context/docs/research/`: raw research and source notes. Read when verifying or citing a company fact.
- `knowledge-base/playbooks/`: repeatable GTM processes. Read before running a known workflow.
- `knowledge-base/learnings/`: what worked and what did not. Read before planning new work.
- `meetings/`: meeting notes and decisions. Read for context on past calls.
- `output/campaigns/`: finished campaign deliverables. Read to reuse or reference shipped work.
- `output/outbound/`: outbound sequences and email copy. Read before drafting outreach.
- `output/social/`: social posts and assets. Read before drafting social content.
- `output/data/`: exports and working data for campaigns. Read when a task needs campaign data.
- `inspiration/`: ads and examples to learn from. Read for reference before creating new creative.
- `tools/`: scripts and utilities. Read when automating a task.
- `weekly-priorities/`: one file per ISO week of planned work. Read at the start of each session.
- `work-log/`: one file per ISO week logging every change. Read and update whenever work is done.
- `.claude/skills/`: custom skills for this workspace. Read when a task matches a defined skill.

## Skills

In `.claude/skills/` (from the gtm-starter-kit repo). Invoke when a task matches.

- `agent-browser`: drive a browser to click, fill forms, log in, screenshot, and pull data from interactive sites.
- `build-clay`: build, audit, repair, or extend a production Clay outbound workbook (Companies and People tables).
- `build-workflow-spec`: turn one campaign idea into a fully gated outbound workflow spec in output/campaigns.
- `calculate-costs`: report the dollar spend and Clay credits used by a Clay table's AI and action columns.
- `campaign-contract`: write contract.md, the Markdown build sheet for one Clay campaign, from an approved decision.
- `campaign-copy`: write and QA outbound copy (cold emails and LinkedIn DMs) from an approved workflow spec.
- `campaign-qa`: QA a Clay table or Instantly/PlusVibe campaign against its workflow spec.
- `campaign-strategy`: generate 15 to 25 cold outbound campaign ideas with targeting, value prop, and priority.
- `clay-build-plan`: turn a workflow spec into a step-by-step Clay build guide plus a swimlane flow diagram.
- `crawl4ai`: crawl pages or whole sites into clean Markdown or JSON, free and local.
- `design-clay-table-json`: write the Clay table JSON (flow blueprint) for one campaign from its contract.
- `export-tables`: export one or more Clay tables to local CSV files.
- `import-clay-table`: import a Clay table JSON, prove paid columns on sample rows, then run within budget.
- `inbox-placement-test`: run an end-to-end cold email inbox placement test and score each sender pool.
- `miro-gtm-flowchart`: draw a GTM system as an editable flow chart on a Miro board.
- `prompt-builder`: build or repair a reusable prompt, such as a Clay AI column's per-row prompt.
- `save-clay-schema`: save an approved Clay table to the local registry as portable JSON.
- `signal-matrix`: build ICP and signal matrices that group buyers into targetable segments.
- `workspace-cost-audit`: report a whole Clay workspace's monthly spend by table, integration, and model.

## Rules

- Cite a source for every company fact.
- Never invent numbers, metrics, or figures.
- No em dashes in any copy.
- Ask before sending or publishing anything.
- Log every change in this week's work log.

## Tools

GTM stack I use:

- Clay: data enrichment and outbound list building.
- HubSpot: CRM and marketing automation.
- n8n: workflow automation and integrations.
- treg: CLI for paid data lookups. Check the price before every call.
- Miro: MCP for diagrams.
- Notion: MCP where we publish finished docs. GitHub stays the source of truth.

Local tool scripts live in `tools/`: agent-browser, crawl4ai, rex (unofficial Clay API client).
