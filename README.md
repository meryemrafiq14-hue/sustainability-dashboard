# Gies Impact Command Center

> **AI-powered sustainability research intelligence for the Gies College of Business, University of Illinois Urbana-Champaign**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-agatafietko.github.io-brightgreen?style=flat-square)](https://agatafietko.github.io/sustainability-dashboard/)
[![Built With](https://img.shields.io/badge/Built%20with-React%20%2F%20HTML-orange?style=flat-square)](#)
[![Team](https://img.shields.io/badge/Team-Silly%20Gies-blueviolet?style=flat-square)](#team)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](#license)

---

## Overview

The **Gies Impact Command Center** maps 2,022 Gies College of Business faculty publications (2010–2020) to the United Nations' 17 Sustainable Development Goals, surfacing research gaps, collaboration opportunities, and strategic intelligence for academic leadership, faculty, donors, and institutional partners.

A two-stage AI classification pipeline processes the raw dataset: LLMs handle relevance detection, and FAISS vector search handles SDG assignment. The dashboard makes that output immediately actionable — without a 40-page PDF.

**[agatafietko.github.io/sustainability-dashboard](https://agatafietko.github.io/sustainability-dashboard/)**

---

## Key Findings

- **2,022** total indexed publications — **426** meet sustainability criteria (21.1%)
- **15 of 17 SDGs** covered — SDG 14 and SDG 15 at zero publications
- **+347% growth** in sustainable research output from 2010 to 2020
- **Largest gaps:** SDG 14 (Life Below Water) and SDG 15 (Life on Land) each at 0 vs. ~5.7% global benchmark
- **Top SDGs:** SDG 3 — 141 papers, SDG 10 — 105 papers, SDG 8 — 87 papers
- **Top researchers:** Lough (53 papers, SDG 17), Fullerton (35, SDG 13), Ahsen (29, SDG 3)
- **Departments:** Business Admin 250 papers, Finance 121, Accountancy 34, Gies Affiliates 21

---

## Features

### Hero Banner
The first thing visible on load. Includes the "Moving from Information to Action." headline, a data provenance strip linking all four sources inline, and the Research Intelligence Assistant panel — key findings surface automatically without any button click.

### Analytics & Visualization
- **SDG Wheel:** Interactive radial chart mapping institutional coverage across all 17 SDGs, with a toggle to overlay the UN global benchmark
- **Gap Index:** Most under-indexed SDGs relative to global averages, surfaced as actionable priority areas
- **Department Breakdown:** Sustainability contribution analysis across Business Administration, Finance, Accountancy, and Gies Affiliates
- **KPI Cards:** Sustainability rate, paper counts, SDG coverage, and largest gap — updated live when SDGs are filtered
- **Publication Trend Chart:** Year-over-year research output from 2010 to 2020
- **Keyword Cloud:** Research topic frequency mapped to SDGs

### AI Classification Pipeline
The dataset was processed through a two-stage automated pipeline before appearing in the dashboard.

**Stage 1 — Relevance Detection:** LLM-based binary classification determines whether each publication contributes to any sustainability goal, directly or foundationally.

**Stage 2 — SDG Assignment:** FAISS vector similarity search assigns the top 3 most relevant SDGs per publication with weighted relevance scores, accounting for interdisciplinary research spanning multiple goals.

All insights labeled "AI-assisted" in the dashboard are deterministic rules-based synthesis of the dataset, not generative predictions.

### Research Intelligence Assistant
The assistant is surfaced inline on the Overview tab — no button click required to see its value. An auto-surfaced insight highlights the most significant finding in the current view. Four quick-prompt pills let users ask pre-formed questions that open the full chat drawer pre-loaded. The full assistant answers natural language questions about SDG gaps, researchers, departments, collaboration opportunities, and strategic recommendations.

### Faculty Profile Modals
Click any researcher card in the Overview or Network tab to open a full profile. Each profile shows department, total sustainable paper count, SDG coverage (primary and secondary with official SDG colors), research keywords sourced from the dataset, and any collaboration pairings the researcher appears in. All data is sourced directly from the Illinois Experts API — no fabricated titles, bios, or publication lists.

### Collaboration Network
- **Named pairings:** Researchers sharing SDG indexing are surfaced as potential collaborators, with both names visible, shared SDGs, combined paper counts, and a concrete outcome description
- **Methodology transparency:** Pairings are based on bibliometric co-indexing only. No numeric compatibility scores are assigned — predicting collaboration success requires qualitative assessment beyond this data
- **Department nodes:** Clickable department graph surfaces pairings with sourced rationale

### Collaboration Hub
A dedicated tab connecting Gies research gaps directly to external funding and partnership opportunities.

- Sustainability Case Competition portal embedded via iframe with full interactivity
- Quick-jump navigation links to Sponsor a Priority, SDG Gaps, Research Partnerships, and Case Competition tracks
- Gap-to-sponsorship mapping: SDGs 14, 15, and 2 — Gies' most under-indexed goals — surface as open sponsorship tracks in the portal
- Context strip explains the connection between the dashboard's gap analysis and the embedded portal

### User Journey Maps
The "Who Uses This" tab contains full visual journey maps for two primary personas. Each map includes a before/after comparison showing how the dashboard improves on the status quo, a 5-step journey with emotion labels per stage, features used, time-to-value, and a plain-language improvement summary.

**Eleanor, 58 — University Donor.** Goal: verify research impact before renewing a major pledge. Before: calls the development office, receives a 40-page PDF, defers decision. With dashboard: filters SDG 13, reads Fullerton's work in the AI snapshot, renews pledge — under 3 minutes.

**Marcus, 22 — Student Researcher.** Goal: find the right Gies professor for a climate finance RA role. Before: emails the department, waits days, cold-emails 10 professors. With dashboard: filters by keyword, identifies Fullerton via the Network tab, emails with context — under 5 minutes.

---

## Data Sources

| Source | Role |
|---|---|
| Illinois Experts API (Elsevier) | Faculty profiles and publication metadata |
| Elsevier Scopus | Bibliometric indexing and DOI resolution |
| UN SDG 2023 Report | Global benchmark distribution (normalized) |
| FT50 / UTD24 Journal Lists | Journal quality classification |

Full methodology is accessible via the "Methodology" link in the dashboard footer and the provenance strip on the Overview tab.

---

## Design Decisions

**No numeric collaboration scores.** Earlier prototypes included a compatibility score per pairing. This was removed after judge feedback that predicting collaboration success from bibliometric data alone is methodologically unsound. Pairings are now presented as data-driven suggestions with explicit sourcing, not ranked predictions.

**No fabricated researcher data.** Faculty profiles display only what is present in the dataset: name, department, paper count, SDG assignments, and keywords. Job titles, bios, and publication lists were removed to preserve data integrity.

**AI transparency.** All "AI-assisted" labels refer to deterministic rules-based synthesis of the dataset. The assistant does not generate predictions or inferences beyond what the data supports.

---

## Navigation

| Tab | Contents |
|---|---|
| Overview | Hero banner, data provenance, AI assistant, KPI cards, SDG wheel, gap index, department breakdown, keyword cloud, AI snapshot |
| Network | Collaboration pairings by department, researcher nodes, faculty profile grid, methodology disclaimer |
| Global Impact | World map, geospatial research reach, full SDG coverage by region |
| Collaboration Hub | Embedded Case Competition portal, SDG gap-to-sponsorship mapping, partner links |
| Who Uses This | Visual journey maps for Donor and Student personas with before/after status quo comparison |

---

## Technical Stack

| Layer | Technology |
|---|---|
| Frontend | React (single-file, CDN-loaded, no build step) |
| AI Classification | LLM-based binary relevance detection — Stage 1 |
| Vector Search | FAISS — top-3 SDG assignment per publication — Stage 2 |
| Data Pipeline | Python, Illinois Experts API, rate-limited scraping |
| Collaboration Hub | Streamlit iframe embed |
| Deployment | GitHub Pages |

---

## Repository Structure

```
sustainability-dashboard/
├── index.html        # Single-file React dashboard — all components, styles, and logic
└── .gitignore
```

Everything lives in `index.html`. No dependencies, no build process, no npm install.

---

## Getting Started

### View Locally

```bash
git clone https://github.com/agatafietko/sustainability-dashboard.git
cd sustainability-dashboard
open index.html
```

### Deploy to GitHub Pages

1. Go to **Settings > Pages** in your forked repo
2. Set source to `main` branch, `/ (root)`
3. Live at `https://<your-username>.github.io/sustainability-dashboard/`

---

## Team

**Silly Gies** — Gies College of Business, University of Illinois Urbana-Champaign

Agata Fietko · Yuri Chen · Meryem Hassan Rafiq · Yuliia Koreiba · Prateek Verma

---

## Changelog

| Version | Changes |
|---|---|
| v1.0 | Initial fork — base SDG dashboard from prattkk11 |
| v1.1 | Collaboration Hub tab with Streamlit iframe embed and gap-to-sponsorship mapping |
| v1.2 | Hero banner — "Moving from Information to Action." |
| v1.3 | Faculty profile modals with verified dataset-only data |
| v1.4 | Data provenance strip, inline AI assistant panel, quick-prompt pills |
| v1.5 | Full visual user journey maps with before/after status quo comparison |
| v1.5.1 | Removed numeric compatibility scores; added methodology disclaimer |
| v1.5.2 | Fixed AI chatbot responses to remove fabricated statistics |

---

## Roadmap

- [x] Two-stage AI classification pipeline (LLM + FAISS)
- [x] Interactive SDG wheel with global benchmark toggle
- [x] Hero banner with inline data provenance
- [x] Research Intelligence Assistant with auto-surfaced insights
- [x] Faculty profile modals (verified data only)
- [x] Collaboration Hub with embedded Case Competition portal
- [x] SDG gap-to-sponsorship mapping
- [x] Visual user journey maps (Donor + Student personas)
- [ ] Confidence score display per publication classification
- [ ] Semantic / natural language publication search
- [ ] Research similarity recommendations for collaboration discovery
- [ ] Year-over-year growth rate callouts on trend charts
- [ ] Data freshness timestamps and source attribution

---

## Forked From

[prattkk11/sustainability-dashboard](https://github.com/prattkk11/sustainability-dashboard)

---

## License

MIT
