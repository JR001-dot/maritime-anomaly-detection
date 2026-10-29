# Ship Engine Anomaly Detection

Comparison of a statistical rule and two unsupervised models for flagging abnormal readings in ship-engine sensor data.

**Origin:** University of Cambridge Data Science Career Accelerator coursework (2024-25). **Data:** source anonymised and not included in this repository. Notebook outputs are cleared to protect the source data; the figures below come from the original run.

## What was done
- 19,535 readings across 6 sensors (engine rpm, lubricating-oil pressure and temperature, fuel pressure, coolant pressure and temperature); no missing or duplicate rows.
- **IQR rule:** a reading is flagged when at least two sensors fall outside their IQR bounds.
- **One-Class SVM** (RBF kernel) and **Isolation Forest** on standardised sensor values.
- PCA used only to plot the results in two dimensions.

## Results
| Method | Setting | Readings flagged |
|---|---|---|
| IQR rule (2+ sensors out of range) | - | 422 (2.16%) |
| One-Class SVM | nu = 0.05, gamma = 'scale' | 980 (5.02%) |
| One-Class SVM | nu = 0.05, gamma = 0.5 | 1,043 (5.34%) |
| Isolation Forest | contamination = 'auto' | 2,892 (14.8%) |
| Isolation Forest | contamination = 0.05 | 977 (5.0%) |

## Interpretation and limitations
- The IQR rule is the only result not fixed in advance: for One-Class SVM and Isolation Forest, `nu` and `contamination` set the share of readings flagged, so the 5% figures reflect the chosen setting, not a discovery.
- There are no labelled faults, so none of the methods can be scored for accuracy; they are candidate anomalies for engineering review.
- Readings are treated independently (no time ordering).

## Tech stack
Python, pandas, NumPy, scikit-learn (One-Class SVM, Isolation Forest, PCA, StandardScaler), Matplotlib, Seaborn

## Repository
- `maritime_anomaly_detection.ipynb` - full analysis
- `requirements.txt`

---

**Author:** Raquel J. | [rjdatavoyage.co.uk](https://rjdatavoyage.co.uk)
