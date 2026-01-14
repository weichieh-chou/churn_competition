# User Churn Analysis & Early-Warning Signals (10-Day Horizon)
## Overview

This project builds a user-level churn prediction model based on large-scale event logs, with the objective of identifying users at risk of churn within a short future window (10 days).
The focus is on behavioral signals, engagement dynamics, and temporal patterns, rather than static user attributes.

The project was completed as part of the Python for Data Science course at École Polytechnique.

## Problem Statement

User churn is costly and often preceded by subtle behavioral changes rather than abrupt inactivity.
The goal of this project is to:

**Predict whether a user will churn within the next 10 days**

Capture early warning signals from behavioral and engagement data

Balance predictive performance and business interpretability

## Data & Methodology
### Data Source

Large-scale event-level user logs

Each row represents a user interaction (page views, sessions, actions, timestamps)

### Data Processing

Removed irrelevant or redundant fields (e.g. HTTP status, names, raw timestamps)

Transformed event-level logs into user-level features

Ensured clean temporal alignment and avoided data leakage

### Feature Engineering

Features were grouped into six interpretable categories:

**User Attributes**
Baseline user context (e.g. subscription level, lifecycle stage)

**Usage Volume**
Total activity intensity (sessions, songs, actions)

**Engagement Intensity**
Consistency and depth of usage over time

**Time Context & Recency**
Time since last activity, lifecycle duration, weekend effects

**Preference & Friction Signals**
Ads exposure, errors, thumbs up/down ratios

**Behavioral Trends**
Changes between early vs. late periods within a fixed window
(e.g. accelerating disengagement vs. stable usage)

## Labeling Strategy: Sliding Window

To simulate realistic prediction scenarios:

Aggregated user behavior up to day T

Defined churn label based on activity in [T+1, T+10]

Excluded users who churned before T

Combined multiple snapshot dates to capture different lifecycle stages

This approach enables early churn detection rather than post-hoc analysis.

## Modeling & Evaluation
### Models Tested

Logistic Regression

Random Forest

XGBoost

LightGBM

### Handling Class Imbalance

SMOTE (Logistic Regression)

Class weighting (tree-based models)

### Model Selection

The final model chosen was Logistic Regression (L2 regularization) for its balance between:

- Predictive performance

- Stability

- Interpretability for business use

### Performance (Final Model)

- AUC: ~0.73

- Recall: ~0.64 (prioritized to minimize missed churners)

- Precision: lower by design, reflecting a recall-focused strategy

### Key Insights

- Churn is more strongly associated with behavioral volatility than low usage

- Sudden changes (downgrades, ads exposure, interruptions) are strong churn signals

- Stable, consistent engagement is a key indicator of user loyalty

- Paid users can still be high churn risk when friction increases

## Tech Stack

- Python (pandas, numpy, scikit-learn, imbalanced-learn)

- SQL-style aggregations (via pandas)

- Matplotlib / Seaborn / Plotly for analysis and diagnostics

## Why This Project Matters

This project emphasizes:

- User-level analytics

- Metric definition under temporal constraints

- Data quality and leakage control

- Business-aware trade-offs between recall and precision

It reflects how analytics can support product, growth, and retention decisions through robust behavioral modeling.
