# Gies Impact Command Center

> **AI-powered sustainability research intelligence for the Gies College of Business, University of Illinois Urbana-Champaign**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-prattkk11.github.io-brightgreen?style=flat-square)](https://prattkk11.github.io/sustainability-dashboard/)
[![HTML](https://img.shields.io/badge/Built%20with-HTML%2FJS-orange?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](#license)

---

## Overview

The **Gies Impact Command Center** is an intelligent analytics dashboard that tracks and visualizes sustainability research contributions from Gies College of Business faculty. It automatically maps academic publications to the United Nations' 17 Sustainable Development Goals (SDGs) and surfaces insights for academic leadership, faculty, and institutional reporting.

The system combines a two-stage AI classification pipeline — using large language models for relevance detection and FAISS vector search for SDG assignment — with a clean, interactive frontend that makes research impact immediately legible.

---

## Live Demo

**[prattkk11.github.io/sustainability-dashboard](https://prattkk11.github.io/sustainability-dashboard/)**

---

## Features

### Analytics & Visualization
- **SDG Distribution** — Visual breakdown of research alignment across all 17 UN Sustainable Development Goals
- **Department Comparisons** — Side-by-side sustainability contribution analysis by academic department
- **Publication Trend Analysis** — Year-over-year research output and growth rate tracking
- **Impact KPI Cards** — At-a-glance metrics for sustainability ratios and faculty engagement counts

### AI-Powered Classification
- **Stage 1 — Relevance Detection:** LLM-based binary classification determining whether a publication contributes to any sustainability goal
- **Stage 2 — SDG Identification:** FAISS vector similarity search assigning the top 3 most relevant SDGs per publication, with weighted relevance scores
- Considers both direct sustainability applications and foundational research that supports SDG progress

### Search & Discovery
- **Advanced Filtering** — Filter publications by department, year, SDG goal, and journal tier
- **Journal Impact Tracking** — Cross-references publications against Financial Times and UT Dallas top-journal lists

### Data Sources
- **Illinois Experts API** — Direct integration with the university's research database for faculty profiles and publication metadata
- **Web-Based Enhancement** — Automated scraping with rate-limiting for supplemental research metadata
- **Journal Rankings Database** — Classification of publications by academic impact and business domain

---

## Technical Stack

| Layer | Technology |
|---|---|
| Frontend | React (single-file, GitHub Pages hosted) |
| AI Classification | OpenAI GPT models |
| Vector Search | FAISS + Pinecone |
| Data Pipeline | Python |
| Deployment | GitHub Pages |

---

## Data Architecture

The backend pipeline structures data across three primary layers:

**Faculty Records** — identifiers, department affiliations, active status, research keyword profiles

**Publication Database** — article metadata, DOIs, journal classifications, sustainability scores, SDG mappings

**Sustainability Analytics** — binary sustainability flags, ranked SDG assignments (top 3 per publication), temporal trends, department-level aggregations

---

## Repository Structure

```
sustainability-dashboard/
├── index.html        # Single-file React dashboard (all components, styles, and logic)
└── .gitignore
```

The entire frontend is contained in `index.html` — no build step required.

---

## Getting Started

### View Locally

Clone the repo and open `index.html` directly in a browser:

```bash
git clone https://github.com/agatafietko/sustainability-dashboard.git
cd sustainability-dashboard
open index.html
```

No dependencies, no build process, no npm install needed.

### Deploy to GitHub Pages

1. Go to **Settings → Pages** in your forked repo
2. Set source to `main` branch, `/ (root)`
3. Your dashboard will be live at `https://<your-username>.github.io/sustainability-dashboard/`

---

## Use Cases

**Academic Leadership** — Evidence-based insights for sustainability planning, metrics for accreditation reporting, identification of emerging research strengths

**Faculty** — Recognition of SDG contributions, discovery of potential collaborators working on related goals

**Institutional Reporting** — Quantifiable data for sustainability rankings, grant applications, and transparent documentation of research impact

---

## Roadmap

Planned enhancements based on the original system documentation:

- [ ] Faculty-level drill-down profiles with individual SDG breakdowns
- [ ] Confidence score display per publication classification
- [ ] Semantic search with natural language query support
- [ ] Research similarity recommendations for collaboration discovery
- [ ] Year-over-year growth rate callouts on trend charts
- [ ] Data freshness timestamps and source attribution panel

---

## Forked From

[prattkk11/sustainability-dashboard](https://github.com/prattkk11/sustainability-dashboard) — original build by the Gies consulting team.

---

## License

MIT
