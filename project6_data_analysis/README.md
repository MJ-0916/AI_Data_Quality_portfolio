# Project 6 — Football Player Scores (Data Cleaning + EDA)

## Overview
This project focuses on a football player scores dataset and demonstrates end-to-end data preparation and exploratory analysis.
My goal was to investigate what factors are most related to player Rating.
This analysis supports real-world stakeholder needs such as scouting, team building, and performance evaluation.

## Dataset
- ~18,979 players, 78 variables (mix of numeric + categorical)
- Target variable: **Rating (scale 0–100)**
- Example features: BestOverall, Age, MarketValue, WeeklyWage, Height, Weight, Position-related stats

## Process 
## 1) Data Ingestion
- Loaded raw CSV into Python (pandas) and performed initial QA checks (nulls/duplicates/value counts)

## 2) Data Quality Assurance & Cleaning
- Removed irrelevant columns (index-like / URL fields)
- Fixed formatting issues (escape characters, extra spaces, inconsistent strings)
- Corrected scaling errors (values exceeding 100 where applicable)
- Standardized units:
  - Height → cm
  - Weight → kg
- Parsed currency-like columns into numeric:
  - MarketValue, WeeklyWage, ReleaseClause (€, K/M conversions)
- Resolved overlapping contract information by creating a clear **OnLoan** indicator
- Handled missing values and cleaned wide-range popularity signals

## 3) Exploratory Data Analysis (EDA)
## Insight 1 — Rating is strongly associated with BestOverall
A clear upward trend indicates that higher BestOverall scores correspond to higher Rating.

## Insight 2 — Rating relates to MarketValue and Age
MarketValue increases sharply for players with Rating above ~80.
High-rated players are concentrated around peak performance ages (mid-20s to early-30s).

## Files
- `Football_player_dataset.csv` — cleaned dataset used for analysis
- `figures/` — exported EDA charts



