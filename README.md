# BranchLens — Banking Branch Performance Analytics

**An end-to-end Business Analytics portfolio project simulating a real-world banking operations problem.**

---

## Project Overview

Indian banks operate hundreds of branches across geographies and tiers — but most performance tracking stops at deposits and loan volumes. The real inefficiencies lie deeper: tellers sitting idle, ATMs loaded with cash nobody withdraws, relationship managers who log zero customer interactions for months.

BranchLens is a full-cycle analytics project that surfaces these hidden inefficiencies across 120 branches using synthetic but realistic data from four core banking systems.

---

## Problem Statement

> *"A branch can look profitable on deposits while being operationally broken. How do you find those branches — and quantify the waste?"*

Most branch scorecards only track revenue metrics. This project builds an operational efficiency framework that identifies underperforming branches using four KPIs that revenue metrics cannot capture.

---

## Key Findings

- **40 of 120 branches require immediate intervention** — failing on 3 or 4 operational KPIs simultaneously
- **Average teller utilisation is only 29.1%** — tellers are idle more than 70% of their working day
- **₹197 average cost per branch transaction** — with a 2.3x gap between Metro (₹139) and Rural (₹317)
- **37.2% of ATM cash sits unused on average** — on a Metro branch loading ₹200L/month, that is ₹74L locked in a machine every month
- **46 branches had at least one zero-CRM month** — RMs logged no customer interactions despite hundreds of walk-ins
- **Performance is seasonal, not improving** — costs peak at ₹217 in Nov/Dec, drop to ₹176 in July, indicating a structural staffing problem not a gradual improvement trend
- **West region has the highest critical rate at 42.3%** — 11 of 26 branches require immediate action
- **Semi-Urban tier has the highest cash idle ratio** — more idle cash than even Rural branches despite higher footfall

---

## Data Architecture

Synthetic data generated for four systems across 120 branches over 12 months (FY2024):

| System | Rows | What it contains |
|--------|------|-----------------|
| CBS (Core Banking) | 1,437 | Branch transactions, digital transactions, deposits, fee income |
| HRMS | 1,440 | Staff count, attendance, salary cost, overhead |
| CRM | 1,440 | RM interactions, follow-ups, product conversions, loan value |
| ATM | 1,020 | Cash loaded, dispensed, idle, downtime hours |
| Master Table | 1,437 | All four systems joined, with 4 engineered KPIs |

---

## Four Core KPIs

| KPI | Formula | What it reveals |
|-----|---------|----------------|
| **Teller Utilisation Rate** | Branch transactions ÷ (Tellers × Days worked × 25) | Whether teller headcount matches actual footfall |
| **Cost Per Transaction** | (Salary + Overhead) ÷ Branch transactions | Operational efficiency of each branch |
| **Cash Idle Ratio** | Cash idle ÷ Cash loaded | Wasted capital locked in ATMs |
| **RM Activity Rate** | RM interactions logged ÷ Footfall | Whether RMs are actually engaging customers |

---

## Methodology

### Phase 1 — Data Generation
Synthetic data built to mirror real Indian banking operations — tier-based transaction volumes, realistic salary structures, seasonal demand patterns, and probabilistic ATM coverage by geography.

### Phase 2 — Data Quality Simulation and Cleaning
15 deliberate data quality issues introduced across all four systems — missing values, duplicate rows, impossible values, format inconsistencies. Each issue reflects a real-world root cause (ETL failures, manual entry errors, timezone mismatches). Cleaned systematically with documented fixes.

### Phase 3 — Master Table and KPI Engineering
All four systems joined on `branch_id` and `month`. Four operational KPIs engineered on top of the joined dataset.

### Phase 4 — Performance Analysis
Each branch benchmarked against its tier median (not the network average) — a Rural branch is not comparable to a Metro branch. Branches scored 0–4 based on how many KPIs fall below their tier benchmark. Labels: Immediate Action (3–4 flags), Monitor (2 flags), Healthy (0–1 flags).

### Phase 5 — Power BI Dashboard
Four-page interactive dashboard built for three audiences — COO (executive summary), Operations Head (cost and teller efficiency), Sales Head (RM activity), Cash Management (ATM efficiency).

---

## Dashboard Pages

| Page | Audience | Key Visuals |
|------|----------|------------|
| Executive Summary | COO | KPI cards, performance by region, cost by tier, underperformance table |
| Cost & Teller | Operations Head | Teller utilisation vs cost scatter, lowest utilisation branches, monthly cost trend |
| RM Activity | Sales Head | RM activity by region, activity vs products sold scatter, zero-CRM branch table |
| ATM Cash Efficiency | Cash Management | Cash idle ratio by tier, loaded vs dispensed by tier, highest downtime branches |

---

## Dashboard Preview

### Page 1 — Executive Summary
- 40 branches flagged for Immediate Action
- North region has 12 critical branches — highest count across all regions
- Rural branches cost ₹317 per transaction vs Metro at ₹139

### Page 2 — Cost & Teller Efficiency
- Clear seasonal U-curve — costs highest in Jan (₹215) and Nov/Dec (₹217), lowest in July (₹176)
- Scatter plot shows Immediate Action branches cluster at low utilisation + high cost (top-left danger zone)

### Page 3 — RM Activity
- South region leads with 22.17% RM activity rate, West is lowest at 20.93%
- 46 branches had at least 1 month of zero RM activity — customers walked in, nobody engaged them
- Positive correlation visible between RM activity rate and products sold

### Page 4 — ATM Cash Efficiency
- 84 of 120 branches have ATMs
- Rural ATMs have highest cash idle ratio at 40.48% — cash loaded far exceeds demand
- Mumbai Main Branch has highest downtime at 6.25 hours/month despite being Metro

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy) | Data generation, cleaning, KPI engineering, analysis |
| Jupyter Notebook | Development environment |
| Power BI Desktop | Dashboard and visualisation |

---

## Repository Structure

```
BranchLens/
├── notebooks/
│   └── 01_data_generation.ipynb    # All code — generation, cleaning, analysis
├── outputs/
│   ├── branch_annual_performance.csv   # 120 branches scored and labelled
│   ├── monthly_trend.csv               # 12-month KPI trends
│   ├── region_analysis.csv             # Performance by region
│   ├── tier_analysis.csv               # Performance by tier
│   └── deposit_trap_branches.csv       # Branches hiding behind deposits
└── README.md
```

---

## How to Run

1. Clone the repository
2. Install dependencies: `pip install pandas numpy faker`
3. Open `notebooks/01_data_generation.ipynb` in Jupyter
4. Run all cells in order (Cells 1–19, skip cells 20–23)
5. Open Power BI Desktop and connect to the `outputs/` folder

---

## About

**Vivek Agarwal** — Aspiring Business Analyst

This project was built to demonstrate end-to-end analytics capability — from understanding a business problem, designing a data model, cleaning messy data, engineering meaningful metrics, and communicating findings through a dashboard.

---

*BranchLens is a portfolio project. All data is synthetically generated and does not represent any real institution.*
