# CICIDS2017 Intrusion Detection Capstone Project

## 📌 Project Overview
This capstone project focuses on building an **intrusion detection system (IDS)** using the [CICIDS2017 dataset](https://www.kaggle.com/datasets/chethuhn/network-intrusion-dataset) (mirrored on Kaggle).  
The goal is to classify network traffic as **benign or malicious** and provide actionable insights for cybersecurity defense.  

We applied multiple approaches — from classical ML to anomaly detection — and compared their strengths and weaknesses.  

---

## 📂 Dataset
- **Source:** CICIDS2017 (Canadian Institute for Cybersecurity)  
- **Size (after sampling):** ~300,000 records, 78 features  
- **Classes:**  
  - **BENIGN** (normal traffic)  
  - **ATTACKS** (DoS, PortScan, DDoS, Brute Force, Infiltration, etc.)  

**Sampling strategy:** Stratified random sampling to keep class balance and ensure computational feasibility.  

---

## 🛠️ Modelling Approach
We evaluated **supervised** and **unsupervised** models:

### 🔹 1. RandomForest (Baseline)
- Strong, interpretable supervised classifier.
- Tuned with class balancing (`class_weight="balanced_subsample"`).
- Served as our main benchmark.  

### 🔹 2. XGBoost
- Gradient boosting method optimized for structured/tabular data.  
- Achieved high accuracy and generalization.  

### 🔹 3. Logistic Regression
- Lightweight linear model for comparison.  
- Useful as a baseline sanity check.  

### 🔹 4. IsolationForest (Unsupervised)
- Trained only on **benign traffic** to flag anomalies.  
- Explored different contamination values (`0.001–0.1`).  
- Results showed very **low recall** → anomaly detection alone struggles in CICIDS2017.  

---

## 📊 Results & Metrics

| Model              | Precision | Recall | F1-score | ROC-AUC |
|--------------------|-----------|--------|----------|---------|
| **RandomForest**   | ~0.9985   | ~0.9985| ~0.9985  | High    |
| **XGBoost**        | ~0.997–0.998 | ~0.997–0.998 | ~0.998 | High    |
| **Logistic Reg.**  | Lower     | Lower  | Lower    | Moderate|
| **IsolationForest**| 0.0526    | 0.0002 | Very low | Poor    |

📌 **Interpretation:**
- **Supervised models (RF, XGBoost)** → excellent detection, near-perfect metrics.  
- **IsolationForest** → performed poorly, confirming that CICIDS2017 attacks are not strong statistical outliers.  

---

## 🔍 Explainability
We used **SHAP (SHapley Additive exPlanations)** to understand model behavior:  
- Top contributing features included **Flow Duration, Packet Length, Flow IAT Mean**, etc.  
- SHAP summary plots and feature importance rankings provided transparency for stakeholders.  

---

## 🤖 AI Support (IBM Granite)
Throughout the project, **IBM Granite LLM** was used for:  
- **Exploratory Data Analysis (EDA)** guidance  
- **Feature importance summarization**  
- **Executive-level reporting** → auto-generated summaries & recommendations for cybersecurity teams.  

---

## 📈 Key Insights
1. **RandomForest and XGBoost are highly reliable** for intrusion detection on CICIDS2017.  
2. **IsolationForest is insufficient** as a standalone IDS — recall was too low.  
3. **Feature explainability** (via SHAP) gives trust and transparency, critical for real-world adoption.  
4. **Balanced sampling** ensured fair training and evaluation.  

---

## ✅ Recommendations
- Use **RandomForest/XGBoost** as the production baseline IDS.  
- Deploy **explainability tools (SHAP)** alongside models for transparency.  
- Explore **deep learning (RNNs/CNNs)** for sequential traffic analysis.  
- Consider **real-time deployment** using streaming frameworks (Kafka, Flink).  

---

## 📦 Repository Structure
├── data/ # Raw and sampled dataset
├── notebooks/ # Jupyter/Colab notebooks
│ └── ClassificationData&SummarizationIBMCapstone.ipynb
├── reports/ # PPT / PDF presentation slides
├── README.md # Project documentation

yaml
Copy code

---

## 📤 Submission Details
- **Notebook:** Colab + GitHub repo with dataset + code  
- **Presentation:** PPT/PDF summarizing findings  
- **AI Support:** Documented use of IBM Granite  

---

## 🙌 Acknowledgements
- Dataset by **Canadian Institute for Cybersecurity (CIC)**  
- IBM Granite for LLM-based assistance  
- Project completed as part of **Capstone – Data Classification & Summarization**  

Deep learning models (Autoencoders, LSTMs) for sequential traffic patterns.

Semi-supervised learning to handle unseen attacks.

Online/streaming IDS deployment for real-time detection.
