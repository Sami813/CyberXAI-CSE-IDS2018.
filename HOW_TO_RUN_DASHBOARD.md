# How to Run the CyberXAI Power BI Dashboard

## Dashboard File

Open the following Power BI project file from the downloaded repository:

```text
powerbi/CyberXAI\_FINAL\_STABLE\_V9/CyberXAI\_FINAL\_STABLE\_V9.pbip
```

The `CyberXAI\_FINAL\_STABLE\_V9` folder already contains the dashboard input CSV files required for the final report, including:

```text
confusion\_matrix.csv
errors\_by\_attack\_label.csv
errors\_by\_confidence\_band.csv
feature\_importance.csv
model\_metrics.csv
model\_summary.csv
performance\_by\_attack\_label.csv
performance\_by\_test\_file.csv
powerbi\_data\_dictionary.csv
```

You do **not** need to create or copy these CSV files separately.

\---

## Software Required

Install **Microsoft Power BI Desktop** on Windows.

Python and Jupyter are only required if you want to reproduce the machine-learning analysis. They are not required simply to open and inspect the final dashboard.

\---

## Step 1 — Download the Repository

Download or clone:

```text
https://github.com/Sami813/CyberXAI-CSE-IDS2018
```

If using GitHub ZIP:

1. Download the repository ZIP.
2. Extract it to any folder on the computer.
3. Keep the original folder structure unchanged.

\---

## Step 2 — Open the Dashboard

Navigate to:

```text
powerbi/CyberXAI\_FINAL\_STABLE\_V9/
```

Open:

```text
CyberXAI\_FINAL\_STABLE\_V9.pbip
```

Power BI Desktop should open the report and semantic model.

\---

## Step 3 — If the Dashboard Opens Normally

If all visuals load correctly:

1. Select **Home → Refresh**.
2. Confirm that the dashboard values appear normally.
3. No data-source changes are required.

\---

## Step 4 — If Power BI Shows a Data Source / File Path Error

The Power BI semantic model was originally developed on a different computer and may still contain an absolute source path such as:

```text
D:\\Sami Data Set\\powerbi\\
```

On another computer, this path may not exist.

If Power BI cannot locate the CSV files:

1. Open the `.pbip` project.
2. Go to **Home → Transform data**.
3. Open **Data source settings**.
4. Select the affected CSV/file source.
5. Choose **Change Source**.
6. Point Power BI to the local folder:

```text
<YOUR\_EXTRACTED\_REPOSITORY>\\powerbi\\CyberXAI\_FINAL\_STABLE\_V9\\
```

7. Select the corresponding CSV file if Power BI asks for an individual file.
8. Repeat only for sources that show an error.
9. Choose **Close \& Apply**.
10. Select **Home → Refresh**.

You are only correcting the local file path. Do not replace, edit, or recreate the analytical CSV files.

\---

## Step 5 — Verify the Main Results

The final dashboard should remain consistent with the authoritative Python outputs.

Expected final model values include:

```text
Test records:              1,331,907
Accuracy:                  98.00%
Malicious precision:       97.92%
Malicious recall:          91.96%
Malicious F1-score:        94.85%
ROC-AUC:                   98.82%
Average precision:         97.46%

True negatives:            1,060,600
False positives:           5,202
False negatives:           21,386
True positives:            244,719
```

The main attack-level limitation should also remain visible:

```text
Infilteration test records:      23,697
Infilteration false negatives:   21,161
Infilteration detection rate:    10.70%
```

\---

## Important Note About the Dashboard

Power BI is used as the **reporting and visual communication layer**.

The machine-learning analysis, predictions, SHAP calculations, evaluation metrics, and error-analysis outputs were produced in Python.

The CSV/JSON analytical outputs are therefore the authoritative evidence. Power BI presents those results visually and should be refreshed whenever the underlying analytical files change.

\---

## Raw Dataset Requirement

The ten raw CSE-CIC-IDS2018 parquet files are **not required simply to open and inspect the final Power BI dashboard** because the final dashboard CSV files are already included in the V9 Power BI folder.

The raw parquet files are required only if a user wants to reproduce the complete Python/Jupyter workflow from the beginning.

\---

## Recommended Folder Structure

Keep the project structure similar to:

```text
CyberXAI-CSE-IDS2018/
├── data/
│   └── raw/
├── notebooks/
├── powerbi/
│   └── CyberXAI\_FINAL\_STABLE\_V9/
│       ├── CyberXAI\_FINAL\_STABLE\_V9.pbip
│       ├── CyberXAI\_FINAL\_STABLE\_V9.Report/
│       ├── CyberXAI\_FINAL\_STABLE\_V9.SemanticModel/
│       ├── confusion\_matrix.csv
│       ├── errors\_by\_attack\_label.csv
│       ├── errors\_by\_confidence\_band.csv
│       ├── feature\_importance.csv
│       ├── model\_metrics.csv
│       ├── model\_summary.csv
│       ├── performance\_by\_attack\_label.csv
│       ├── performance\_by\_test\_file.csv
│       └── powerbi\_data\_dictionary.csv
├── requirements.txt
└── README.md
```

\---

## Quick Summary for a New User

```text
1. Download and extract the repository.
2. Install Power BI Desktop.
3. Open powerbi/CyberXAI\_FINAL\_STABLE\_V9/CyberXAI\_FINAL\_STABLE\_V9.pbip.
4. If it opens normally, click Refresh.
5. If a path error appears, change the source path to the local V9 folder.
6. Close \& Apply, then Refresh.
7. Verify the final metrics shown above.
```

