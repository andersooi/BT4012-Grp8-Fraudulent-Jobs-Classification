# Real Job? Or Just a Rob | Detecting Fake Job Listings

## 👨🏻‍💻 Project Overview

Job scams are one of the fastest-growing forms of fraud, with estimated losses soaring from **$90 million (2020) to over $501 million (2024)**.

Leveraging unsuspecting job seekers, scammers use fraudulent job posts for various malicious reasons, including Identity Theft, Credential Harvesting, setting up Pyramid Schemes/MLMs, extracting Training 'Fees', and Malware Installation, among many others.

Our project developed a sophisticated Machine Learning pipeline to automatically predict and flag fraudulent job posts, protecting job seekers from identity theft and financial harm. 

## 🎯 Definition of Success
Success for this project was defined as creating a reliable fraud detection framework exhibiting a high ROC AUC score, while maximumising recall by ensuring the fewest possible scams slip through the cracks, minimising False Negatives.

## 📁 Data Overview

We leveraged the **Fraudulent Job Posting Dataset** from the University of Aegean, which contains 17,880 job descriptions suffering from a severe class imbalance, with a ratio of approximately 20 non-fraudulent posts for every fraudulent one.

## 🔎 Methodology

Through extensive Exploratory Data Analysis (EDA) and feature engineering, we identified strong characteristics inherent to fake job posts. These ranged from structural omission of certain attributes, textual brevity, to even the presence of specific identified scam indicators.
We used this comprehensive sk-learn pipeline framework to rigorously test the performance and characteristics of six different models: 

| Model | Selection Justification |
| :--- | :--- |
| **Logistic Regression (LR)** | Crucial interpretable baseline for feature impact analysis. |
| **Gaussian Naive Bayes (GNB)** | Lightweight generative baseline for sanity checks (best suited for continuous features). |
| **Random Forest (RF)** | Non-linear ensemble model to capture complex feature interactions and robust against noise. |
| **XGBoost (Extreme Gradient Boosting)** | Core non-linear model known for strong performance on imbalanced/mixed datasets. |
| **Bi-directional LSTM (BiLSTM)** | Deep learning model for learning sequential, context-dependent textual patterns (high Recall focus). |
| **DistilBERT** | Advanced transformer benchmark for transfer learning and deep semantic understanding. |

---

## 📊 Experiments and Results Summary
The model evaluation utilised two separate cross-validation processes: Stratified 5-Fold CV for traditional machine learning (ML) models and Stratified 3-Fold CV for deep learning (DL) models (due to computational limits), with the Receiver Operating Characteristic - Area Under Curve (ROC AUC) as the primary stability metric.

| Model | Precision | Recall | F1-Score | ROC AUC | Selection Rationale |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BiLSTM** | 0.34874 | **0.95954** | 0.51156 | 0.98771 | **Primary Detector:** Chosen for highest Recall, prioritizing user safety (min. False Negatives). |
| **DistilBERT** | 0.93711 | 0.86127 | 0.89759 | **0.99364** | **High-Confidence Ranker:** Best F1-Score and ROC AUC; ideal for triaging high-risk posts. |
| **RF** | **0.97183** | 0.67788 | 0.79833 | 0.98603 | High Precision baseline; good non-linear performance. |
| **XGBoost** | 0.90190 | 0.71132 | 0.79535 | 0.98121 | Best balance in traditional ML; robust for mixed data types. |
| **LR** | 0.58379 | 0.85686 | 0.69443 | 0.97844 | Strong, interpretable baseline performance. |
| **GNB** | 0.39374 | 0.69746 | 0.50333 | 0.82152 | Underperformed due to sparse TF-IDF and violated assumptions. |

## 💡 Key Learnings 

* **Traditional Models Validate Structural Signals:** Models like **XGBoost** and **Random Forest** performed exceptionally well (high ROC AUC) on the engineered features. This confirms that **interpretable structural cues** we identified are highly predictive and provide a strong, efficient baseline.
* **Deep Learning (BiLSTM) Guarantees Safety:** Although DistillBERT has the highest ROC AUC Score, the **BiLSTM** was chosen as the primary detector because its superior **Recall (0.95954)** directly addresses the goal of minimizing **False Negatives** (missed scams). In fraud detection, high Recall is prioritised because the cost of an FN (identity theft/user harm) outweighs the inconvenience of a False Positive.

---

## 🚀 Future Considerations 

* **Optimise Performance and Comparability:** We must implement **Systematic Hyperparameter Tuning** across all six models to achieve the optimal **Precision–Recall trade-off** and make performance comparisons fairer.
* **Develop Hybrid Systems:** Future work should focus on **Ensemble Methods** to combine the high-recall **BiLSTM** (for detection) with the high-precision **DistilBERT/XGBoost** (for filtering high-risk posts) for robust real-world deployment.
