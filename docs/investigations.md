# Technical Investigation Report

## Investigation Overview

The investigation covered model performance, classification issues, Federated Averaging, differential privacy, dataset distribution, and software engineering practices.
The review was read-only. No project files were modified or models retrained.

## Centralized vs Federated Learning

The agent compared the saved evaluation metrics of centralized and federated learning.

| Metric | Centralized | Federated |
|---|---:|---:|
| Accuracy | 0.5109 | 0.6709 |
| Macro-F1 | 0.3380 | 0.4008 |
| Weighted-F1 | 0.5347 | 0.6348 |
| Macro Recall | 0.3598 | 0.4032 |
| QWK | 0.4889 | 0.6867 |

**Finding:** The saved federated results show improvements across all five aggregate metrics.

**Limitation:** The training configurations differ, and federated learning starts from an existing global checkpoint. Therefore, the improvement cannot be attributed to federated learning alone.

**Evidence:** `reports/metrics/centralized.json`, `reports/federated/evaluation.json`.

## Severe Diabetic Retinopathy Zero-Recall Investigation

The agent investigated why the federated model failed to predict Severe Diabetic Retinopathy (class 3).

**Confirmed observations:**
- 29 Severe samples were present in the test set.
- Severe class recall and F1-score were both zero.
- The model made zero predictions for class 3.
- 14 Severe samples were classified as Moderate and 15 as Proliferative.
- The starting global checkpoint also showed zero Severe recall in its saved evaluation results.

**Possible contributing factors:**
- Significant class imbalance.
- Uneven Severe sample distribution across clients.
- Absence of class weighting in federated training.
- Limited local training duration.
- Differential privacy noise.
- Limited model feature adaptation.

These factors are hypotheses and require further experiments for confirmation.

**Evidence:** `reports/federated/evaluation.json`, `models/global/metadata.json`, `reports/validation/dataset_analysis.json`, `reports/federated/client_distribution.csv`.

## Federated Averaging Review

The agent examined the FedAvg implementation and identified four simulated clients.

| Client | Samples | Contribution |
|---|---:|---:|
| A | 1026 | 40.0% |
| B | 378 | 14.7% |
| C | 643 | 25.1% |
| D | 516 | 20.1% |

**Findings:**
- Client updates are aggregated using sample-count-weighted averaging.
- No arithmetic defect was identified in the normal aggregation path.
- Potential improvements include validating sample counts and tensor shapes and handling empty client partitions.

**Evidence:** `backend/app/federated/server.py`, `backend/app/federated/fedavg.py`.

## Differential Privacy Review

The agent examined the implementation of privacy-related mechanisms.

**Findings:**
- Model updates undergo L2 norm clipping with a threshold of 1.0.
- Gaussian noise is added before aggregation.
- The saved federated run uses a noise multiplier of 0.1.
- The noise-generation function reinitializes its random generator with seed 42 when no generator is supplied.

**Limitation:** The reviewed implementation does not establish a formal differential privacy guarantee or provide a calculated privacy budget.

**Evidence:** `backend/app/federated/differential_privacy.py`, `backend/app/federated/server.py`, `reports/federated/status.json`.

## Dataset Distribution Analysis

The investigation identified substantial class imbalance.

| DR Class | Training Samples | Test Samples |
|---|---:|---:|
| No DR | 1263 | 271 |
| Mild | 259 | 56 |
| Moderate | 699 | 150 |
| Severe | 135 | 29 |
| Proliferative | 207 | 44 |

The Severe class also has an uneven distribution across the four simulated clients, with client-level counts of 93, 25, 15, and 2.

**Finding:** Class imbalance and client heterogeneity are confirmed observations, but their individual effects on model performance have not been experimentally established.

**Evidence:** `reports/validation/dataset_analysis.json`, `reports/federated/client_distribution.csv`.

## Software Engineering Review

The agent identified several areas for improvement:

- Expand automated test coverage.
- Strengthen dataset label validation.
- Improve API input and uploaded-image validation.
- Avoid using test accuracy for model checkpoint selection.
- Improve background training coordination for multi-worker deployment.

These are potential reliability improvements identified during source-code review.

## Recommended Improvements

Based on the investigation, the agent recommended:

1. Evaluate Severe class performance at every federated training round.
2. Compare class-weighted loss and balanced sampling.
3. Compare frozen-backbone training with selected-layer fine-tuning.
4. Evaluate IID and non-IID client distributions.
5. Compare different noise configurations.
6. Improve input validation, automated testing, and training diagnostics.

## Conclusion

The investigation demonstrated how an AI agent can examine an existing machine learning project, identify performance issues, review implementation details, and generate evidence-based technical recommendations.

The findings provide useful directions for further experimentation while highlighting the importance of human review and validation.
