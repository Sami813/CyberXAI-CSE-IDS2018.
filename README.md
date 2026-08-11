# CyberXAI-CSE-CIC-IDS2018

## Explainable Machine Learning and Big Data Analytics for Cybersecurity Threat Detection

This repository contains the implementation, experimental outputs, and supporting documentation for an MSc group project on explainable machine learning for network intrusion detection using the **CSE-CIC-IDS2018** benchmark dataset.

The project was designed as a traceable end-to-end workflow covering data quality checks, class-imbalance analysis, feature selection, machine-learning model comparison, final held-out evaluation, explainability, attack-level error analysis, and Power BI reporting.

\---

## Project Overview

The main aim of the project is to investigate how effectively an explainable machine-learning workflow can distinguish **benign** and **malicious** network traffic while keeping the modelling process transparent and reproducible.

The project examines:

* data quality and preprocessing;
* class imbalance and attack distribution;
* feature relevance and redundancy;
* malicious-class precision, recall, and F1-score;
* false positives and false negatives;
* attack-level detection weaknesses;
* SHAP and other feature-importance methods;
* reproducible transfer of model outputs into Power BI.

\---

## Dataset

The experiments use the **CSE-CIC-IDS2018** dataset.

|Item|Value|
|-|-:|
|Source files|10 parquet files|
|Total records|6,659,532|
|Benign records|5,329,008 (80.02%)|
|Malicious records|1,330,524 (19.98%)|
|Missing values in processed files|0|
|Infinite values in processed files|0|
|Within-file duplicates in processed files|0|

The full raw and processed datasets are **not stored in this repository** because of their size. The repository instead contains notebooks, configuration files, selected outputs, and documentation needed to understand and reproduce the workflow.

\---

## Research Workflow

1. Dataset inventory and quality audit
2. Preprocessing and binary target construction
3. Stratified 80:20 train-test split
4. Exploratory class and attack analysis
5. Training-only feature analysis
6. Top-10, Top-15, and Top-20 candidate feature evaluation
7. Model comparison and limited tuning
8. Final model selection
9. One-time evaluation on the untouched test set
10. Attack-level error analysis
11. Global and local explainability
12. Power BI reporting and interpretation

### Final split

* **Training records:** 5,327,625
* **Test records:** 1,331,907
* **Random seed:** 42

The final test set was kept separate from feature selection and model tuning.

\---

## Feature Selection

Feature analysis used:

* correlation analysis;
* mutual information;
* Random Forest feature importance;
* redundancy checks;
* validation of reduced candidate feature sets.

The final modelling representation contained **20 features**.

### Selected 20 features

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

\---

## Models Compared

Four supervised classifiers were evaluated:

* Logistic Regression
* Decision Tree
* Random Forest
* XGBoost

Random Forest and XGBoost produced the strongest validation results. After limited tuning, **XGBoost** was selected as the final classifier.

\---

## Final Model Configuration

* **Model:** XGBoost
* **n\_estimators:** 250
* **max\_depth:** 6
* **learning\_rate:** 0.05
* **min\_child\_weight:** 2
* **subsample:** 0.85
* **colsample\_bytree:** 0.85
* **random seed:** 42
* **classification threshold:** 0.50
* **number of selected features:** 20

\---

## Final Held-Out Test Results

The final XGBoost model was evaluated once on **1,331,907 untouched test records**.

|Metric|Result|
|-|-:|
|Accuracy|98.00%|
|Precision (malicious)|97.92%|
|Recall (malicious)|91.96%|
|F1-score (malicious)|94.85%|
|ROC-AUC|98.82%|
|Average Precision|97.46%|
|True Negatives|1,060,600|
|False Positives|5,202|
|False Negatives|21,386|
|True Positives|244,719|

Approximate timings:

* **Training:** 392.81 seconds
* **Final test prediction:** 19.75 seconds

\---

## Key Finding: Infilteration Detection

The overall test performance was strong, but attack-level error analysis revealed an important limitation.

Of the **21,386 false negatives**, **21,161 were Infilteration records**.

For Infilteration:

* **Test records:** 23,697
* **True positives:** 2,536
* **False negatives:** 21,161
* **Detection rate:** approximately 10.70%

This shows why the project does not rely on overall accuracy alone.

\---

## Explainability

The final model was interpreted using:

* XGBoost native feature importance;
* permutation importance;
* SHAP global explanations;
* SHAP local explanations for selected predictions.

Across these methods, **Fwd Seg Size Min** appeared as one of the most influential features.

Other important features included:

* Init Fwd Win Bytes
* RST Flag Count
* Bwd IAT Min
* Fwd IAT Std
* Init Bwd Win Bytes
* Flow Duration
* Fwd Packet Length Max

The explanation results describe how the fitted model behaves on this benchmark. They are **not treated as proof that these variables cause malicious activity**.

\---

## Power BI Dashboard

Power BI is used as a reporting and visualisation layer.

The dashboard presents:

* overall model metrics;
* confusion-matrix results;
* attack-level detection performance;
* false-negative distribution;
* model-error analysis;
* feature-importance results.

Power BI does not independently recalculate the machine-learning results. It uses exported CSV/JSON outputs from the Python workflow.

\---

## Repository Structure

```text
CyberXAI-CSE-CIC-IDS2018/
│
├── README.md
├── .gitignore
│
├── notebooks/
│   └── Jupyter notebooks for data audit, preprocessing,
│       feature selection, modelling, testing, and XAI
│
├── documentation/
│   └── Experiment configuration, audit files, and supporting records
│
├── outputs/
│   └── Final metrics, confusion matrices, attack-level results,
│       and explainability exports
│
├── models/
│   └── Model-related configuration and retained artefacts
│
├── powerbi/
│   └── Power BI reporting resources
│
└── data/
    └── Large raw/intermediate datasets are excluded from Git
```

\---

## Reproducibility

Important reproducibility records include:

* data-quality audit outputs;
* train-test split configuration;
* random seed;
* selected feature list;
* candidate feature-set results;
* baseline model results;
* tuned model results;
* final model configuration;
* final held-out evaluation;
* confusion-matrix values;
* attack-level error outputs;
* SHAP and feature-importance results;
* Power BI input tables.

\---

## Software and Tools

* Python
* Jupyter Notebook
* pandas
* NumPy
* scikit-learn
* XGBoost
* SHAP
* Matplotlib
* PyArrow / parquet files
* Power BI

\---

## Running the Project

```bash
git clone <repository-url>
cd CyberXAI-CSE-CIC-IDS2018
pip install -r requirements.txt
jupyter notebook
```

Then run the notebooks in their documented workflow order.

Because the complete CSE-CIC-IDS2018 dataset is not stored in GitHub, the dataset must be obtained separately and placed in the expected local data directory before running the full preprocessing pipeline.

\---

## Project Team

**University of the West of Scotland**  
School of Computing, Engineering and Physical Sciences  
MSc Masters Project — 2025/26

|Student|Workstream|
|-|-|
|Sami Ullah|Cyber Threat Pattern and Class Imbalance Analytics|
|Asad Waseem|Feature Selection and Network Flow Feature Analysis|
|Student 3 — name to insert|Comparative Machine-Learning-Based Threat Classification|
|Student 4 — name to insert|Explainability and Dashboard-Based Cybersecurity Threat Interpretation|

\---

## Academic Scope

This repository represents an **offline academic benchmark study**.

The project does not claim:

* live production deployment;
* automatic blocking of network traffic;
* operation inside a security operations centre;
* cross-network generalisation from a single benchmark;
* that SHAP or feature importance establishes cyberattack causation.

Future work should consider chronological evaluation, cross-dataset testing, probability calibration, cost-sensitive modelling, and deeper analysis of the Infilteration failure mode.

\---

## Citation

Suggested citation:

```text
CyberXAI Project Team (2026).
An Explainable Machine Learning and Big Data Analytics Framework
for Cybersecurity Threat Detection Using CSE-CIC-IDS2018.
MSc Masters Project, University of the West of Scotland.
```

\---

## License

This repository is currently provided for academic and research purposes.

Before adding an open-source license, confirm the intended licensing terms with the project team and university requirements.

\---

## Acknowledgement

This project uses the **CSE-CIC-IDS2018** intrusion-detection benchmark developed by the Canadian Institute for Cybersecurity.

