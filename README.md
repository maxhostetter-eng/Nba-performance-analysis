# NBA Team Performance Analysis

A Jupyter Notebook that uses 30 years of NBA team statistics (1996–2026) to answer one core question:

**Do teams win as many games as their stats suggest they should?**

Using Ridge Regression, this project predicts how many games each team *should* win based on 17 statistical inputs — both offensive metrics (shooting percentages, assists, rebounds, steals, turnovers, and blocks) and defensive/opponent metrics (opponent shooting percentages, opponent points, opponent assists, and opponent rebounds). The gap between what a team actually won and what the model predicted is called the **residual**. A consistently positive residual signals something beyond raw talent: great coaching, culture, or clutch performance. A consistently negative one suggests a team that underperformed its potential.

---

## What This Project Produces

1. **Pulls data** from the official NBA API — every team, every season from 1996–97 through 2025–26
2. **Trains a walk-forward model** that predicts wins using only stats from *past* seasons — no future information ever leaks in
3. **Calculates residuals** — the gap between actual wins and model predictions
4. **Shows 30-year franchise charts** with an interactive dropdown for any NBA team
5. **Ranks every NBA coach** by how much they consistently beat or missed the model's expectations
6. **Provides three interactive coaching views** — league-wide rankings, team-by-team history, and season-by-season career breakdowns

---

## Interactive Dropdown Menus

A key feature of this notebook is its use of **interactive dropdown menus** powered by `ipywidgets`. Rather than re-running cells manually, you can explore the data dynamically:

- **Team Performance Chart Dropdown** — Select any NBA franchise from a dropdown menu to instantly render a 30-year chart of that team's actual wins vs. model-predicted wins, along with their residual trend over time.
- **Team Coaching History Dropdown** — Choose a team to view the coaching history for that franchise, showing how each head coach's tenure affected the team's over/underperformance relative to the model.
- **Coach Career Breakdown Dropdown** — Select any individual coach to see a season-by-season breakdown of their career residuals across every team they coached.

These dropdowns make the notebook feel like an interactive dashboard — no code changes required to explore different teams or coaches.

---

## Tools Used

| Library | Purpose |
|---|---|
| `nba_api` | Fetches data directly from NBA.com |
| `pandas` | Stores and manipulates the dataset |
| `scikit-learn` | Builds the Ridge Regression model with automatic alpha tuning via `RidgeCV` |
| `matplotlib` | Generates all charts |
| `ipywidgets` | Powers the interactive dropdown menus |

---

## Why Ridge Regression?

NBA team statistics are highly correlated with each other — teams that shoot well tend to assist well, and teams that rebound well tend to defend well. Standard linear regression handles this poorly, assigning huge positive coefficients to some features and compensating negative coefficients to others in ways that don't generalize across seasons.

**Ridge Regression** solves this by adding a penalty for large coefficients, forcing the model to spread weight more evenly across all 17 inputs. The result is a more stable, interpretable model that generalizes honestly across 30 years of NBA data.

Rather than picking the penalty strength (alpha) manually, this project uses **RidgeCV**, which automatically tests eleven candidate values (`1e-4, 1e-3, 0.01, 0.05, 0.1, 0.5, 1.0, 5.0, 10.0, 50.0, 100.0`) and selects the best one via cross-validation on each training window.

---

## Table of Contents

1. Why Ridge Regression?
2. Data Collection and Model
3. Understanding the Model Metrics
4. Team Performance Charts
5. How to Draw Conclusions from These Charts
6. Coach Tenure Data
7. All-Seasons Model and Coach Residuals
8. League-Wide Coaching Rankings
9. Team Coaching History
10. Coach Career Breakdown
11. Most Surprising Seasons — Era Adjusted

---

## Getting Started

### Prerequisites

```bash
pip install nba_api pandas scikit-learn matplotlib ipywidgets
```

### Running the Notebook

1. Clone this repository
2. Open `NBA_Analysis_using_multiple_linear_regression-for-github.ipynb` in Jupyter Notebook or JupyterLab
3. Run all cells from top to bottom
4. Use the dropdown menus that appear in the interactive sections to explore teams and coaches

> **Note:** The notebook fetches live data from the NBA API on each run. An internet connection is required.

---

## Key Concepts

- **Residual**: Actual wins minus model-predicted wins. Positive = overperformed, negative = underperformed.
- **Walk-forward validation**: The model is trained only on seasons prior to the one being predicted, preventing data leakage.
- **RidgeCV alpha**: Printed at runtime for each training window so you can see exactly what penalty the model selected.
