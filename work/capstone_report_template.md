# Capstone Report — <your lane>

- **Author:** Ruchita Mohan Barhate 
- **Lane:** Content Performance Analysis
- **Repo:** Ruchi74/flyrank-ml-internship
- **Date:** 25 October 2026

> Copy this file to `work/capstone_report.md` and fill it in as you build. Sections 1–8
> mirror the Pass / Needs-Work rubric axes, so nothing here is optional. Sections 0 and 9
> are **paper sections**: your deployed research paper must carry both, and they're here so
> you never rebuild them from memory at ship time.

## 0. Abstract

Five sentences, written last, placed first: question → data → method → headline result →
what the output is for. This is the top of your deployed paper.

## 1. Problem framing

This project analyzes anonymized content performance data to identify pages that may need improvement. The unit of analysis is an individual content page. The analysis uses available metrics such as impressions, clicks, sessions, content age, and engagement to identify potential opportunities. FlyRank editors can use these findings to prioritize pages for review, investigate low click-through rates, and assess whether content may need updating. The analysis supports human decision-making; it does not guarantee future performance or prove that any single factor causes a change in traffic. Incorrect recommendations could waste editing time or lead to unnecessary content changes, so findings should be reviewed before action. Machine learning and data analysis help organize large datasets and identify patterns that would be difficult to review manually.

## 2. Data safety

The project uses an anonymized content performance dataset containing 30,000 rows and 44 columns. The analysis reviewed content metrics, including impressions, clicks, sessions, content age, and engagement-related fields.

Potential leakage fields such as `trend_direction` and `trend_pct` were identified and excluded from the selected model features because they describe performance outcomes and could reveal information related to the target. Identifier columns such as `content_id` and `client_id` were also excluded from model features to avoid memorizing individual pages or clients. Time-window performance metrics were reviewed carefully before feature selection.

The feature-preparation workflow selected 19 original features and produced 42 encoded feature columns. Missing numeric values were handled through median imputation, and categorical features were encoded. The workflow reported no missing values in the prepared feature matrix.

The dataset is described as anonymized, but the repository should still be checked for client-identifying information before submission. The leakage review helps reduce the risk of using information that would not be legitimately available at prediction time.

## 3. Baseline

A simple rule-based approach is used as a transparent starting point for content performance analysis. Pages with at least 500 impressions and an average position between 1 and 20 are checked for low click-through rate (CTR). Pages with CTR below 0.5 are flagged for editorial review. This rule is easy to understand and provides a practical way to prioritize pages for investigation.

In the signal audit, 12,023 pages met the eligibility criteria, and 9,759 (81.17%) had CTR below 0.5. The median CTR was 0.21, and the median average position was 8.2. These results show that many eligible pages could be reviewed for potential improvement, but they do not prove that changing a page will increase traffic.

This rule is a preliminary baseline, not a validated predictive model. A fair model comparison requires both approaches to be evaluated on the same held-out data using the same target and metrics. Those comparative results must be added only after the model evaluation has been completed.

## 4. Model / analysis

Your method and why it fits the lane. The exact feature list (and what you left out on
purpose). The target or proxy definition, in one sentence.

## 5. Evaluation

Your split (grouped by client? time-aware?) and why. Metrics, model vs baseline **on the same
split**. What the errors look like — a short error analysis beats a big metric table.

## 6. Interpretation

What the model/clusters actually found. Feature importances or cluster profiles in plain
words. Surprises and negative results — a well-understood "no effect" is a valid result.

## 7. Recommendation

The ranked actions or decisions your output supports, and how a FlyRank editor would use them
tomorrow. State your confidence and the limits explicitly.

## 8. Reproducibility

The exact commands to re-run everything from a fresh clone, your random seeds, and your
environment (`pip freeze` highlights or `requirements.txt` deltas). If you claim a sealed or
holdout evaluation, two things must be committed: the cell/script that builds the sealed
frame, and the metrics file it produced — "evaluated once, blind" should be checkable from
your repo, not taken on faith.

## 9. Acknowledgments & data credit

One short section at the bottom of the deployed paper: "Built on the FlyRank ML Internship
dataset" **linking to https://flyrank.ai**. Crediting your data source is standard research
practice — and it's on the capstone's required-section list, so a paper without it isn't done.

---

> **Claims checklist before submitting:** observed / measured / directional / decision-support
> **Metrics vs. base rate:** report your task's base rate (majority-class %) next to any
> precision@K or accuracy — a high score can just be a high base rate. AUC / lift over
> baseline are the honest discrimination numbers.
> language everywhere · no causal claims without an experiment or causal design · no
> "predicted Google's algorithm" · no client-identifying details · numbers in this report
> match a fresh re-run.
