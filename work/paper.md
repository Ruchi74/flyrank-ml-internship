# A Machine-Learning Approach to Identifying Content Refresh Opportunities

## Abstract

This study investigates whether machine learning can help prioritize existing content for refresh review. It uses the anonymized FlyRank ML Internship starter dataset containing 30,000 content-item rows and compares several models with a rule-based baseline. The Random Forest model achieved a ROC AUC of 0.750, average precision of 0.618, Precision@50 of 0.740, and F1-score of 0.640 in the reported evaluation. These results suggest that the model may help rank content for human review, but they do not establish that refreshing the selected content will improve performance. Further validation and careful monitoring are needed before operational use.

## 1. Introduction and Problem Statement

Websites contain many existing content items that may need updating, improvement, or closer review. Manually reviewing every item can require substantial effort.

This project investigates whether a machine-learning model can rank content items according to their potential risk of decline and help reviewers prioritize their work.

The objective is to support editorial decision-making, not to automatically modify or publish content.

## 2. Data

### Dataset and scope

The model report identifies the source as the bundled anonymized starter dataset, `data/raw/content_refresh_anonymized.csv`.

The report records 30,000 rows and 16,262 rows with the declining-content label, corresponding to a reported label rate of 0.542.

The exact date window, source-table lineage, and release details must be confirmed from the project documentation before publication.

### Privacy and exclusions

The report states that the model does not use titles, URLs, client names, domains, or keywords. The public paper reports aggregate results and avoids exposing private client information.

## 3. Methodology

### Target

The target is `is_declining_label`, as specified in the model report.

### Models

The reported comparison includes a decision tree, logistic regression, Random Forest, and a rule-based baseline.

The Random Forest was selected using Precision@50, which measures precision among the 50 highest-ranked items.

### Validation

The report identifies the validation strategy as `client_holdout`. The detailed split configuration, held-out client count, and preprocessing procedure should be confirmed against the experiment artifacts before publication.

### Leakage checks

The experiment should be checked to ensure that target-derived fields are excluded from predictive features, identifiers are used only where appropriate for grouping, and preprocessing is fitted without using held-out test information.

## 4. Results

### Model comparison

The following metrics are transcribed from the repository's model report.

| Model | ROC AUC | Average precision | Precision@50 | Recall | F1 |
|---|---:|---:|---:|---:|---:|
| Decision tree | 0.742 | 0.575 | 0.540 | 0.716 | 0.634 |
| Logistic regression | 0.700 | 0.522 | 0.400 | 0.567 | 0.566 |
| Random Forest | 0.750 | 0.618 | 0.740 | 0.744 | 0.640 |
| Rule-based baseline | 0.627 | 0.468 | 0.240 | Not reported | Not reported |

The Random Forest has the highest reported ROC AUC, average precision, Precision@50, and F1-score among the listed models. Its Precision@50 of 0.740 indicates that 37 of the top 50 ranked items were positive under the evaluation definition, if the reported precision was calculated on exactly 50 items.

These results support further investigation of the ranking approach. They do not demonstrate that the model's recommendations cause improvements in traffic, engagement, or business outcomes.

### Supporting charts

The repository contains these chart artifacts:

- `outputs/charts/action_mix.svg`
- `outputs/charts/confidence_mix.svg`
- `outputs/charts/top_reason_codes.svg`
- `outputs/charts/top_feature_importance.svg`
- `outputs/charts/trend_distribution.svg`

Embed the charts in the deployed paper and verify that each chart's values and labels match the intended experiment.

## 5. Limitations

- The reported results apply to the bundled anonymized starter dataset and the evaluation documented by the repository.
- The exact date window and detailed validation configuration have not yet been confirmed in this paper.
- Model performance alone does not establish that a content refresh will improve outcomes.
- Feature importance indicates model reliance, not causation.
- Dataset missingness, label quality, and distribution changes may affect performance.
- Performance on other datasets, clients, or time periods has not been established.
- The rule-based baseline has no recall or F1 values in the report; these are not inferred here.

The model should therefore be treated as a prioritization aid, not as a proven automatic decision system.

## 6. Ranked Recommendations

These are proposed review actions, not guaranteed outcomes.

1. **Review high-priority items:** Inspect highly ranked content manually and confirm that a genuine issue exists.
2. **Check content relevance:** Verify accuracy, completeness, freshness, and alignment with audience needs.
3. **Investigate performance signals:** Review impressions, clicks, engagement, and position in context before deciding what to change.
4. **Check technical issues:** Investigate indexing, accessibility, broken links, and page performance where relevant.
5. **Measure changes:** Compare suitable metrics before and after approved updates and account for other factors that may affect results.

Human reviewers should approve every action. The illustrative action queue must not be presented as proof of actual business impact.

## 7. Reproducibility

The project repository contains the model report, source notebook, and chart artifacts. The deployed version of this paper should identify the exact experiment notebook and supporting output files used for its reported results.

Before final publication, verify the dataset release, date window, validation details, and source of every metric against the experiment artifacts.

## 8. Acknowledgments and Data Credit

Built on the FlyRank ML Internship dataset.

