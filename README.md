# gasman-march-mania-2026-rnd-v1

> **GasMan's R&D Notebook — Kaggle March Machine Learning Mania 2026**  
> NCAA Basketball Tournament Win Probability Prediction (Men + Women)

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue)](https://www.kaggle.com/code/gastondana/gasman-march-mania-2026-rnd-v1)
[![Python](https://img.shields.io/badge/Python-3.12-green)]()
[![License](https://img.shields.io/badge/License-MIT-yellow)]()

---

## Overview

This notebook builds a full end-to-end pipeline for the [March Machine Learning Mania 2026](https://www.kaggle.com/competitions/march-machine-learning-mania-2026) competition. It covers both Men's and Women's tournament prediction using historical NCAA data going back to 1985.

---

## Notebook Structure (Cell-by-Cell)

| Cell | Title | Description |
|------|-------|-------------|
| 1 | Imports & Config | Libraries, seed, data path setup, file validation |
| 2 | Data Loading + EDA | Load 11 CSV files, parse seeds, compute win rates by seed |
| 3 | Feature Engineering | Season-level team stats, matchup differentials (5 features) |
| 4 | Plotly Visualizations | 4 interactive charts (seed win rates, point dist, correlation, scatter) |
| 5 | Model Training | 5-fold CV with Logistic Regression + LightGBM, log-loss evaluation |
| 6 | Submission Generation | Predict all Stage 2 matchups, export `submission.csv` |

---

## Features Used

| Feature | Description |
|---------|-------------|
| `SeedDiff` | Team1 seed minus Team2 seed |
| `WRDiff` | Win rate differential (regular season) |
| `PDDiff` | Point differential differential |
| `APDiff` | Average points differential |
| `FGDiff` | Field goal % differential |

---

## Model Results (5-Fold CV Log-Loss)

| Gender | Logistic Regression | LightGBM |
|--------|--------------------|-----------|
| Men | **0.55819** | 0.57655 |
| Women | **0.42520** | 0.45103 |

Logistic Regression outperforms LightGBM on this compact feature set — seed differential is a dominant linear signal.

---

## Key EDA Findings

- **Seed 1 teams** win ~80% of all tourney games historically
- **SeedDiff** has the strongest negative correlation with win probability (-0.48)
- **PDDiff** and **WRDiff** are highly correlated (0.84), suggesting multicollinearity worth addressing in v2
- Women's predictions are tighter (lower log-loss) due to stronger chalk (higher-seed dominance)

---

## Submission

- **132,133 matchup predictions** (66,430 Men + 65,703 Women)
- Predictions clipped to `[0.025, 0.975]` to avoid log-loss extremes
- Mean prediction: ~0.503 (well-calibrated)

---

## Stack

```
Python 3.12 | Kaggle Notebooks
pandas, numpy, scikit-learn
lightgbm
plotly (iframe renderer)
```

---

## Roadmap (v2)

- [ ] Elo rating system per team
- [ ] Massey Ordinals feature integration
- [ ] Coach tenure + continuity features
- [ ] Conference strength weighting
- [ ] Ensemble blending (LR + LGB + Ridge)
- [ ] Stage 2 update with final regular season data

---

## Author

**GasMan** (gastondana627) — [@gastondana.tech](https://gastondana.tech)  
Built with Kaggle Notebooks | Competition closes April 2026
