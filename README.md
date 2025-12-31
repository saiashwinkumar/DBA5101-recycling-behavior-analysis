# Analyzing Recycling Behavior at NUS

This repository contains the code and analysis for evaluating whether **new recycling bin designs** improved recycling behavior at the National University of Singapore (NUS), measured via **contamination rates** for paper, plastic, and cans across two locations (ENGINE, UTOWN). 
## Objective
Assess whether two interventions reduced contamination rates:
- **Phase 2:** Shaped openings (bin design “nudge”)
- **Phase 3:** Informational banners (visual instructions)
compared to **Phase 1 baseline**.

## Data
Dataset: `Project2Data.xls`

Key columns:
- `Area`: ENGINE / UTOWN
- `Date`: observation date
- `PaperContaminant`, `PlasticContaminant`, `CanContaminant`: contamination rates (%)
- `FirstTrialPhase`: Phase 1 (baseline), Phase 2 (shaped openings), Phase 3 (banners)

## Preprocessing
- Dropped rows where all contamination variables were missing
- Treated isolated missing values (e.g., in `CanContaminant`) without removing entire rows
- Outliers were retained due to small sample size; robustness methods were used instead 

## Methodology
- **Exploratory analysis:** phase-wise and area-wise contamination trends and distributions
- **Difference-in-Differences (DiD):** estimated separately for paper, plastic, and cans to isolate intervention effects
- **Robustness checks:**
  - Bootstrap confidence intervals (10,000 iterations; seed=123)
  - Mean-based vs median-based DiD (median preferred for outlier robustness)
  - Zero-contamination sensitivity check (Phase 1 zeros)
  - Interrupted Time Series (ITS) to examine level/slope changes across phases 

## Key Findings
- **Overall (DiD):** Interventions did not produce consistent, statistically reliable improvements across all materials and phases.
- **Plastic is the biggest problem:** highest contamination levels (~35–60%), making it the top priority target.
- **UTOWN worse than ENGINE:** higher baseline contamination → needs more focused intervention effort.
- **Phase 2 > Phase 3:** shaped openings generally performed better than banners; Phase 3 improvements were not robust (bootstrap CIs often included 0). 

## Recommendations
- Do **not** scale shaped openings + banners as a default campus-wide solution (limited cost-effectiveness).
- Use a **plastic-first strategy** (highest ROI):
  - better plastic receptacles, anti-overflow inserts, clearer lid affordances
  - co-locate trash + recycling with high-salience labels
  - simple feedback loops (photo audits, red/amber/green scorecards)
- Apply **location-specific strategies**:
  - UTOWN: peer-led nudges, micro-incentives, high-traffic interventions
  - ENGINE: ops SOPs, bin placement resets, custodian training, incident reporting 

## Reproducibility
All analysis is implemented in Python (pandas + statsmodels) with scripts/notebooks to reproduce:
- EDA plots
- DiD estimates (mean + median)
- bootstrap CIs
- ITS outputs

Run the notebooks end-to-end with `Project2Data.xls` to reproduce results. 

