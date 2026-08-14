# CyberXAI-CSE-IDS2018

## Explainable Machine Learning and Big Data Analytics for Cybersecurity Threat Detection

This repository contains the implementation, notebooks, explainability outputs, and Power BI artefacts for the MSc group project:

**“An Explainable Machine Learning and Big Data Analytics Framework for Cybersecurity Threat Detection Using CSE-CIC-IDS2018.”**

## Project Overview

The experimental dataset contains:

* **6,659,532 labelled network-flow records**
* **5,329,008 benign records (80.02%)**
* **1,330,524 malicious records (19.98%)**
* **10 Parquet files**
* **0 missing values**
* **0 infinite values**
* **0 within-file duplicates identified during the audit**

A stratified **80:20 train/test split** with random seed **42** was used.

The final model is a tuned **XGBoost classifier** using **20 selected features**.

### Final Test Performance

|Metric|Result|
|-|-:|
|Accuracy|98.00%|
|Malicious Precision|97.92%|
|Malicious Recall|91.96%|
|Malicious F1-score|94.85%|
|ROC-AUC|98.82%|
|Average Precision|97.46%|
|True Negatives|1,060,600|
|False Positives|5,202|
|False Negatives|21,386|
|True Positives|244,719|

## Repository Structure

```text
CyberXAI-CSE-IDS2018/
├── data/
│   ├── raw/
│   ├── processed/
│   ├── interim/
│   └── splits/
├── notebooks/
│   ├── 01\_dataset\_inventory.ipynb
│   ├── 02\_data\_quality\_audit.ipynb
│   ├── 03\_processed\_data\_creation.ipynb
│   ├── 04\_exploratory\_data\_analysis.ipynb
│   ├── 05\_train\_test\_split.ipynb
│   ├── 06\_training\_feature\_selection.ipynb
│   ├── 07\_candidate\_feature\_set\_validation.ipynb
│   ├── 08\_model\_development\_validation.ipynb
│   ├── 09\_random\_forest\_xgboost\_tuning.ipynb
│   ├── 10\_final\_model\_training\_test\_evaluation.ipynb
│   └── 11\_explainability\_error\_analysis\_and\_powerbi.ipynb
├── documentation/
├── models/
├── outputs/
├── powerbi/
├── requirements.txt
└── README.md
```

The notebooks use **portable project-relative paths**, so the repository can be extracted to any normal local folder.

## 1\. Download the Repository

```bash
git clone https://github.com/Sami813/CyberXAI-CSE-IDS2018.git
cd CyberXAI-CSE-IDS2018
```

Alternatively, use **Code → Download ZIP** on GitHub and extract it anywhere.

## 2\. Download the Dataset

Download the 10 Parquet assets from:

https://github.com/Sami813/CyberXAI-CSE-IDS2018/releases/tag/dataset-v1

Place all 10 `.parquet` files inside:

```text
data/raw/
```

Required assets:

1. `Botnet-Friday-02-03-2018\_TrafficForML\_CICFlowMeter.parquet`
2. `Bruteforce-Wednesday-14-02-2018\_TrafficForML\_CICFlowMeter.parquet`
3. `DDoS1-Tuesday-20-02-2018\_TrafficForML\_CICFlowMeter.parquet`
4. `DDoS2-Wednesday-21-02-2018\_TrafficForML\_CICFlowMeter.parquet`
5. `DoS1-Thursday-15-02-2018\_TrafficForML\_CICFlowMeter.parquet`
6. `DoS2-Friday-16-02-2018\_TrafficForML\_CICFlowMeter.parquet`
7. `Infil1-Wednesday-28-02-2018\_TrafficForML\_CICFlowMeter.parquet`
8. `Infil2-Thursday-01-03-2018\_TrafficForML\_CICFlowMeter.parquet`
9. `Web1-Thursday-22-02-2018\_TrafficForML\_CICFlowMeter.parquet`
10. `Web2-Friday-23-02-2018\_TrafficForML\_CICFlowMeter.parquet`

## 3\. Python Environment

Tested environment:

```text
Python 3.14.7
```

### Windows PowerShell

```powershell
py -m venv .venv
.\\.venv\\Scripts\\python.exe -m pip install --upgrade pip
.\\.venv\\Scripts\\python.exe -m pip install -r requirements.txt
```

Verify the main packages:

```powershell
.\\.venv\\Scripts\\python.exe -c "import pandas,numpy,sklearn,xgboost,shap,matplotlib,pyarrow,joblib; print('ALL PACKAGES OK')"
```

## 4\. Verify the Dataset

```powershell
(Get-ChildItem ".\\data\\raw\\\*.parquet").Count
```

Expected output:

```text
10
```

## 5\. Start JupyterLab

```powershell
.\\.venv\\Scripts\\python.exe -m jupyter lab
```

Open the `notebooks` folder.

## 6\. Notebook Execution Order

For a complete reproduction, run:

```text
01 → 02 → 03 → 04 → 05 → 06 → 07 → 08 → 09 → 10 → 11
```

|Notebook|Purpose|
|-|-|
|`01\_dataset\_inventory.ipynb`|Dataset inventory and file verification|
|`02\_data\_quality\_audit.ipynb`|Missing, infinite, duplicate and label audit|
|`03\_processed\_data\_creation.ipynb`|Processed dataset creation|
|`04\_exploratory\_data\_analysis.ipynb`|Exploratory data analysis|
|`05\_train\_test\_split.ipynb`|Stratified training/test split|
|`06\_training\_feature\_selection.ipynb`|Training-only feature selection|
|`07\_candidate\_feature\_set\_validation.ipynb`|Candidate feature-set validation|
|`08\_model\_development\_validation.ipynb`|Comparative model development and validation|
|`09\_random\_forest\_xgboost\_tuning.ipynb`|Random Forest and XGBoost tuning|
|`10\_final\_model\_training\_test\_evaluation.ipynb`|Final XGBoost training and untouched test evaluation|
|`11\_explainability\_error\_analysis\_and\_powerbi.ipynb`|Explainability, error analysis and Power BI exports|

The notebooks already contain saved outputs from the completed experiment. Users who only want to inspect the reported results do not need to retrain the complete workflow.

## 7\. Reproducibility Checkpoints

### Notebook 01

```text
Parquet files found: 10
Total files: 10
Total rows: 6,659,532
```

### Notebook 05

```text
Training records: 5,327,625
Test records: 1,331,907
```

### Notebook 10

```text
Accuracy:            98.00%
Malicious Precision: 97.92%
Malicious Recall:    91.96%
Malicious F1-score:  94.85%
ROC-AUC:             98.82%
Average Precision:   97.46%
```

## 8\. Final Selected Features

1. Fwd Packet Length Max
2. Init Bwd Win Bytes
3. Fwd Packet Length Std
4. Avg Fwd Segment Size
5. Init Fwd Win Bytes
6. Fwd Seg Size Min
7. Flow Duration
8. Flow IAT Max
9. Packet Length Variance
10. Subflow Fwd Bytes
11. Flow IAT Mean
12. Packet Length Mean
13. Packet Length Max
14. Avg Bwd Segment Size
15. Fwd IAT Std
16. Bwd Packet Length Std
17. Bwd Packet Length Max
18. Bwd Packets Length Total
19. Bwd IAT Min
20. RST Flag Count

## 9\. Final XGBoost Configuration

```text
n\_estimators     = 250
max\_depth        = 6
learning\_rate    = 0.05
min\_child\_weight = 2
subsample        = 0.85
colsample\_bytree = 0.85
random\_state     = 42
decision threshold = 0.50
```

## 10\. Explainability and Error Analysis

The final workflow includes:

* feature-importance analysis
* SHAP-based explainability
* attack-label performance analysis
* false-positive and false-negative analysis
* confidence-band analysis
* performance-by-test-file analysis
* Power BI export tables

## 11\. Power BI Dashboard

Main Power BI project:

```text
powerbi/CyberXAI\_FINAL\_STABLE\_V9/CyberXAI\_FINAL\_STABLE\_V9.pbip
```

If opened on another computer, Power BI data-source paths may need to be updated.

## Important Reproducibility Notes

* Start JupyterLab from the repository root where possible.
* Keep the repository structure unchanged.
* Place all 10 raw Parquet files in `data/raw/`.
* Use `requirements.txt` to recreate the tested environment.
* Later notebooks depend on artefacts generated by earlier notebooks.
* Full tuning and SHAP analysis can require substantial processing time.
* Saved notebook outputs are retained as reference results.

## Group Project Contributors

* **Sami Ullah** — Cyber Threat Pattern and Class Imbalance Analytics
* **Asad Waseem** — Feature Selection and Network Flow Feature Analysis
* **Hamad Ullah** — Comparative Machine-Learning-Based Threat Classification
* **Monu** — Explainability and Dashboard-Based Cybersecurity Threat Interpretation

## Repository

https://github.com/Sami813/CyberXAI-CSE-IDS2018

