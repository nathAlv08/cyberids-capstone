#🚀 CIC-IDS2017 Intrusion Detection Capstone Project
📌 Project Overview

This capstone project develops and evaluates an Intrusion Detection System (IDS) using the CIC-IDS2017 dataset (mirrored from Kaggle).
The main objective is to accurately distinguish malicious network traffic (attacks) from benign traffic, ensuring robust anomaly detection for cybersecurity applications.

We follow a structured modeling approach:

Start with a linear baseline (Logistic Regression).

Advance to tree-based supervised models (RandomForest & XGBoost).

Experiment with an unsupervised anomaly detector (IsolationForest).

Evaluate feature importance with SHAP for explainability.

Summarize findings and give practical cybersecurity recommendations.

📊 Dataset

Source: CIC-IDS2017 dataset (Kaggle mirror).

Size: ~2.8M rows, 79 features.

Sampling Strategy: To handle large size and class imbalance, we used stratified random sampling (balanced ~300k rows for training).

Classes:

BENIGN (normal traffic)

ATTACK (aggregated malicious traffic)

🧪 Modelling Approach
1. Logistic Regression (Baseline)

Provides a simple linear benchmark.

Achieved decent accuracy but underperformed on recall compared to tree models.

Shows that non-linear relationships are crucial in intrusion detection.

2. RandomForest (Supervised, Ensemble)

Strong baseline for tabular IDS data.

Trained with class_weight="balanced_subsample".

Achieved near-perfect Precision, Recall, F1, and ROC-AUC (~0.998).

Robust against noise and imbalance.

3. XGBoost (Gradient Boosted Trees)

Gradient boosting enhanced decision boundaries further.

Slightly outperformed RandomForest in some metrics (higher recall for minority attacks).

Best candidate for deployment-ready IDS.

4. IsolationForest (Unsupervised Anomaly Detection)

Trained only on benign traffic to flag anomalies as attacks.

Tested contamination grid [0.001, 0.002, 0.005, 0.01, 0.02, 0.05, 0.1].

Best contamination = 0.1 → Recall = 0.0002, Precision = 0.0526.

Performed poorly → confirms that CIC-IDS2017 attacks are not strong statistical outliers but require labeled learning.

Conclusion: unsupervised anomaly detection is insufficient for this dataset.

📈 Results & Comparison
Model	Precision	Recall	F1-Score	ROC-AUC
Logistic Regression	~0.92	~0.90	~0.91	~0.94
RandomForest	0.9985	0.9985	0.9985	0.9986
XGBoost	0.9990	0.9991	0.9991	0.9992
IsolationForest	0.0526	0.0002	~0.0004	N/A

👉 XGBoost and RandomForest dominate, while Logistic Regression lags, and IsolationForest fails.

🔍 Explainability with SHAP

We applied SHAP (SHapley Additive exPlanations) to RandomForest to interpret feature impact.

Top-5 Most Important Features:

Flow Duration

Total Fwd Packets

Fwd Packet Length Mean

Bwd IAT Std

Packet Length Std

📌 Insight: Attack traffic often shows abnormal packet burstiness, irregular timing patterns, and extreme flow durations. These patterns were the strongest indicators of malicious behavior.

📝 Executive Summary (Granite-assisted)

Our IDS models on CIC-IDS2017 show that supervised ensemble methods (XGBoost/RandomForest) achieve near-perfect performance, far exceeding simpler models and anomaly detectors.

IsolationForest, while attractive for unlabeled data, performed poorly due to the dataset’s complex attack distribution.

Feature analysis with SHAP confirmed that network timing and packet size variability are the strongest predictors of intrusion.

✅ Recommendations

Deploy XGBoost/RandomForest for operational IDS.

Continuously monitor model drift as new attack patterns emerge.

Use SHAP insights to guide rule-based detection and firewall tuning.

Keep anomaly detectors like IsolationForest as lightweight pre-filters, but not as primary IDS.

⚠️ Limitations & Future Work

CIC-IDS2017 is a lab-collected dataset → may not fully reflect real-world traffic.

Models may overfit lab scenarios → need testing on live/streaming data.

IsolationForest confirms: anomaly-only training is insufficient here.

Future directions:

Deep learning models (Autoencoders, LSTMs) for sequential traffic patterns.

Semi-supervised learning to handle unseen attacks.

Online/streaming IDS deployment for real-time detection.
