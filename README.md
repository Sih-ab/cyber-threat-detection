# 🛡️ AI-Powered Cyber Threat Detection System

An intelligent machine learning system for detecting network attacks and classifying different types of cyber threats using the UNSW-NB15 dataset.

## 📌 Project Overview

Cyber attacks are becoming increasingly sophisticated, making automated network threat detection an important part of modern cybersecurity.

This project develops a machine learning-based intrusion detection system that works in two stages:

1. **Binary Classification** — Detect whether network traffic is Normal or an Attack.
2. **Multiclass Classification** — Identify the specific type of attack when malicious traffic is detected.

The system uses the **UNSW-NB15** network intrusion dataset and Random Forest-based machine learning models.

## 📊 Dataset

This project uses the **UNSW-NB15** network intrusion detection dataset.

The dataset contains network traffic records with multiple network-related features and attack categories.

### Dataset Files

- `UNSW_NB15_training-set.csv` — Training data
- `UNSW_NB15_testing-set.csv` — Testing data

### Dataset Statistics

| Dataset | Records | Features |
|---|---:|---:|
| Training Set | 175,341 | 45 |
| Testing Set | 82,332 | 45 |

### Target Variables

- `label` — Binary target: Normal (0) or Attack (1)
- `attack_cat` — Specific category of the detected attack

## 📁 Project Structure

```text
cyber-threat-detection/
│
├── data/
│   ├── UNSW_NB15_training-set.csv
│   └── UNSW_NB15_testing-set.csv
│
├── notebooks/
│   └── 01_data_understanding.ipynb
│
├── models/
│
├── reports/
│
└── README.md

## 🧠 Methodology

The system follows a two-stage machine learning approach.

### Stage 1: Binary Attack Detection

The first model determines whether a network connection is:

- 🟢 **Normal**
- 🔴 **Attack**

Categorical network features such as `proto`, `service`, and `state` were converted using **One-Hot Encoding**.

A **Random Forest Classifier** was then trained to detect malicious network traffic.

### Stage 2: Attack Type Classification

If the traffic is identified as an attack, the second model determines the specific attack category.

The model classifies attacks into:

- Generic
- Exploits
- Fuzzers
- DoS
- Reconnaissance
- Analysis
- Backdoor
- Shellcode
- Worms

Because the attack categories are highly imbalanced, **class-weighted Random Forest** was used to improve performance on minority attack classes.


## 📈 Results

### Stage 1: Binary Classification

The binary Random Forest model achieved strong performance in distinguishing normal traffic from attack traffic.

| Metric | Result |
|---|---:|
| Accuracy | **87.12%** |
| Attack Recall | **99%** |
| True Positives | **44,663** |
| False Negatives | **669** |

The high attack recall indicates that the model was able to detect the majority of malicious network traffic.

### Stage 2: Multiclass Attack Classification

Several Random Forest configurations were evaluated.

| Model | Accuracy | Macro F1 |
|---|---:|---:|
| Baseline Random Forest | 77.43% | 0.48 |
| Balanced Random Forest | 75.36% | **0.53** |
| Mild-weight Random Forest | 76.31% | 0.50 |

The **Balanced Random Forest** was selected as the final multiclass model because it achieved the highest Macro F1 score.

### Attack-wise Performance

The final model performed particularly well on:

- **Generic:** 96% recall
- **Shellcode:** 83% recall
- **Reconnaissance:** 84% recall
- **Fuzzers:** 77% recall

Performance was lower for some minority or difficult-to-distinguish categories such as:

- **Analysis:** 4% recall
- **DoS:** 17% recall
- **Backdoor:** 54% recall
- **Worms:** 48% recall

## ⚠️ Limitations

Although the system achieved strong binary attack detection performance, some limitations remain.

- The dataset contains significant class imbalance among attack categories.
- Some minority attack types, especially **Analysis** and **Worms**, have relatively few training samples.
- The multiclass model does not perform equally well across all attack categories.
- Some attack types have similar network characteristics, making them difficult to distinguish.
- The current system is trained and evaluated on the UNSW-NB15 dataset and may require further validation on real-world network traffic.

## 🚀 Future Improvements

Future versions of this project could include:

- Advanced class balancing techniques such as **SMOTE** or targeted oversampling.
- Hyperparameter tuning for Random Forest and other machine learning models.
- Comparison with **XGBoost, LightGBM, and neural networks**.
- Feature selection and dimensionality reduction.
- Explainable AI techniques such as **SHAP** to understand model predictions.
- Real-time network traffic monitoring.
- A web-based dashboard for visualizing detected threats.
- Deployment as a practical intrusion detection system.

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Random Forest
- Jupyter Notebook
- VS Code
- Git & GitHub

## 📌 Project Status

**Completed — Machine Learning Prototype**

The current version successfully performs:

- Normal vs Attack detection
- Attack type classification
- Model evaluation and comparison
- Class imbalance analysis

Further improvements and real-time deployment are planned for future versions.