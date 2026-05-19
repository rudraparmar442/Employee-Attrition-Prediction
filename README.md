# Employee Attrition Prediction

> End-to-end ML pipeline predicting which employees are likely to leave,
> with SHAP explainability, a $30.8M cost model, and an interactive
> HTML dashboard. Built on the IBM HR Analytics dataset.



## Key results
- **390 employees flagged at risk** — 26.5% of the workforce
- **$30.8M total replacement cost exposure** identified
- **ROC-AUC: 0.777 | Recall: 0.68** — catches 68% of actual leavers
- **Overtime is the #1 attrition driver** — 30.5% rate vs 10.4% without

## Live dashboard
Open `outputs/attrition_dashboard.html` in any browser — no server needed.

## ML pipeline summary
| Stage | Decision | Reason |
|-------|----------|--------|
| Imbalance handling | `scale_pos_weight=5.2` | Avoids SMOTE overfitting on small dataset |
| Model selection | XGBoost | Best test ROC-AUC across 3 models |
| Threshold | 0.32 (F2-optimised) | Maximises Recall — missing a leaver costs more than a false alarm |
| Explainability | SHAP TreeExplainer | Industry standard for tree-based models |

## Model performance
| Metric | Value |
|--------|-------|
| ROC-AUC | 0.777 |
| Recall (Left) | 0.68 |
| Precision (Left) | 0.38 |
| Accuracy | 0.77 |
| Decision threshold | 0.32 |

## Cost model assumptions
- Replacement cost = 1.5x annual salary (industry standard)
- Expected cost = attrition probability × replacement cost per employee
- Sales dept highest exposure: $15.1M across 148 at-risk employees

## Tech stack
`Python` `pandas` `scikit-learn` `XGBoost` `SHAP` `imbalanced-learn`
`matplotlib` `seaborn` `DuckDB` `Chart.js` `SQL`

## Business recommendations
1. Audit overtime policies — single strongest signal, 3x attrition lift
2. Prioritise Sales department — highest rate (20.6%) and $15M exposure
3. Review compensation for below-median earners in at-risk segments
4. Retrain model quarterly — monitor Recall, flag if it drops below 0.55

## Ethical considerations
See `reports/model_card.md` for full details. Key points:
- Model should inform HR conversations, not replace them
- Do not use for disciplinary or termination decisions
- Audit for demographic bias before any real deployment
