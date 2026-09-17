# Task 1, 2, 4, 5, 6 Results — Data Profiling, Prediction, Anomaly, Scenario, Explainability

## Data Loaded
- Training file: `data/sim_train.csv`
- Shape: 16889 rows, 34 columns

## Data Cleaning (Task 1)

- Found and fixed **437 rows** with negative `current_balance` (invalid).
- Found and filled **5200 rows** with missing `interest_rate` (filled with median).

## Feature Engineering
- 19 features used

## Time-Aware Train/Validation Split (Task 2)

- Train rows: 13875
- Validation rows: 3014
- Cutoff date: 2024-05-01
- Split by date (not random) so future information never leaks into training.

## Model Results (predicting `next_12m_default_flag`)

- **ROC-AUC: 0.600**

```
              precision    recall  f1-score   support

           0       0.96      0.87      0.91      2876
           1       0.08      0.24      0.12       138

    accuracy                           0.84      3014
   macro avg       0.52      0.55      0.52      3014
weighted avg       0.92      0.84      0.88      3014

```

## Top 10 Features Driving Predictions (Task 6)

|                       |      0 |
|:----------------------|-------:|
| current_balance       | 0.1217 |
| interest_rate         | 0.1206 |
| ltv_band_enc          | 0.1195 |
| remaining_term_months | 0.0952 |
| credit_score_band_enc | 0.0833 |
| dti_band_enc          | 0.0706 |
| state_enc             | 0.0675 |
| loan_age_months       | 0.0653 |
| original_balance      | 0.041  |
| servicer_name_enc     | 0.0348 |

## Anomaly Detection (Task 4)

- Anomalies flagged: **507** out of 16889 rows (3.0%)

### Sample anomalous records

| loan_id   |   current_balance |   interest_rate |   days_past_due |
|:----------|------------------:|----------------:|----------------:|
| L100000   |                 0 |           7.152 |             120 |
| L100013   |            240657 |           7.044 |             120 |
| L100028   |            143240 |           6.517 |             120 |
| L100031   |            195834 |           7.62  |             120 |
| L100041   |                 0 |           4.298 |              60 |

## Scenario Simulation (Task 5)

| Scenario        |   Avg Predicted Default Probability |
|:----------------|------------------------------------:|
| Base            |                              0.4111 |
| Adverse-credit  |                              0.3781 |
| High-prepayment |                              0.3968 |

## Final Predictions
- Loading official test file: `data/sim_test.csv`

- Saved `outputs/submission.csv` with **4246 rows**

### Sample predictions

| loan_id   |   predicted_default_prob |   anomaly_score | top_driver      | action   | confidence   |
|:----------|-------------------------:|----------------:|:----------------|:---------|:-------------|
| L100001   |                 0.230698 |               0 | current_balance | monitor  | low          |
| L100001   |                 0.248061 |               0 | current_balance | monitor  | low          |
| L100001   |                 0.265866 |               0 | current_balance | monitor  | low          |
| L100001   |                 0.248173 |               0 | current_balance | monitor  | low          |
| L100001   |                 0.26011  |               0 | current_balance | monitor  | low          |