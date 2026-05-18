# Model Card — Employee Attrition Predictor

## Model details
- **Algorithm:** XGBoost classifier
- **Version:** 1.0
- **Date:** 2024
- **Decision threshold:** 0.32 (optimised for Recall using F2 score)

## Intended use
- **Primary use:** Flag employees at high attrition risk for HR intervention
- **Intended users:** HR business partners, people analytics teams
- **Out-of-scope:** Disciplinary decisions, performance reviews, compensation

## Performance (test set, n=294)
- ROC-AUC:  0.777
- Recall:   0.68  (catches 68% of actual leavers)
- Precision: 0.38 (38% of flagged employees actually leave)
- F2 score: optimised — Recall weighted 2x over Precision

## Performance by department
| Department           | Attrition rate | Notes              |
|----------------------|----------------|--------------------|
| Sales                | 20.6%          | Highest risk       |
| Human Resources      | 19.0%          | Small sample (n=63)|
| Research & Development| 13.8%         | Largest group      |

## Key drivers (SHAP)
Top features predicting attrition (see outputs/06_shap_global.png):
Overtime, MonthlyIncome, Age, JobRole, YearsAtCompany

## Limitations
- Dataset size: 1,470 employees — predictions less reliable for rare subgroups
- Static snapshot — does not account for recent life events
- IBM synthetic dataset — may not generalise to all industries

## Ethical considerations
- Model should inform conversations, not replace them
- Do not use predictions for disciplinary or termination decisions
- Recommend quarterly retraining as workforce composition changes
- Audit for demographic bias before deployment in any real organisation

## Recommended review cadence
Retrain quarterly. Monitor Recall on new data — flag if it drops below 0.55.
