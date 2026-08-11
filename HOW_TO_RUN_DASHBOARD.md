# How to Run the CyberXAI Power BI Dashboard

This file explains how to open and refresh the Power BI dashboard included in the **CyberXAI-CSE-CIC-IDS2018** repository.

## Dashboard Version

Use the final stable dashboard version:

```text
powerbi/
└── CyberXAI\_FINAL\_STABLE\_V9/
    └── CyberXAI\_FINAL\_STABLE\_V9.pbip
```

Open:

```text
CyberXAI\_FINAL\_STABLE\_V9.pbip
```

Do not use older dashboard versions if the final V9 project is available.

\---

## Requirements

Install **Microsoft Power BI Desktop** on Windows.

The dashboard is stored as a **Power BI Project (`.pbip`)** rather than a single `.pbix` file.

If Power BI Desktop does not open the project correctly, check:

```text
File
→ Options and settings
→ Options
→ Preview features
```

and enable the Power BI Project / PBIP option if required by your installed version.

The report also uses the Power BI enhanced report definition format (PBIR). If your Power BI version asks to enable the enhanced report format, enable it under the same Preview Features section.

Restart Power BI Desktop after changing preview-feature settings.

\---

## Step 1 — Download or Clone the Repository

Repository:

```text
https://github.com/Sami813/CyberXAI-CSE-IDS2018
```

You can either clone it with GitHub Desktop or download the repository as a ZIP file.

After downloading, keep the complete Power BI folder structure together.

\---

## Step 2 — Locate the Dashboard

Navigate to:

```text
CyberXAI-CSE-IDS2018
└── powerbi
    └── CyberXAI\_FINAL\_STABLE\_V9
```

Inside this folder, locate:

```text
CyberXAI\_FINAL\_STABLE\_V9.pbip
```

Double-click this file to open the dashboard in Power BI Desktop.

\---

## Step 3 — Required CSV Files

The dashboard uses the following analytical result files:

```text
confusion\_matrix.csv
errors\_by\_attack\_label.csv
errors\_by\_confidence\_band.csv
feature\_importance.csv
model\_metrics.csv
model\_summary.csv
performance\_by\_attack\_label.csv
performance\_by\_test\_file.csv
```

These files are included with the final Power BI project.

They contain the final analytical outputs used by the dashboard.

\---

## Step 4 — Important: Data Source Path

The current semantic model was originally developed using the local source folder:

```text
D:\\Sami Data Set\\powerbi\\
```

Because this is an absolute Windows path, another computer may display a data-source error after opening the project.

### If the dashboard opens normally

No change is required. Click:

```text
Home → Refresh
```

and verify that the visuals load correctly.

### If Power BI reports that a CSV file cannot be found

Update the file locations to the folder on your own computer.

In Power BI Desktop:

```text
Home
→ Transform data
→ Data source settings
```

Select the relevant CSV source and choose:

```text
Change Source
```

Then browse to the final dashboard folder in your cloned repository, for example:

```text
C:\\Users\\<YOUR-USERNAME>\\Desktop\\CyberXAI-CSE-IDS2018\\
powerbi\\CyberXAI\_FINAL\_STABLE\_V9\\
```

Repeat this for the required CSV files if Power BI asks for each source individually.

After updating the paths, select:

```text
Close \& Apply
```

and then:

```text
Home → Refresh
```

\---

## Step 5 — Verify the Dashboard

The final stable V9 project contains presentation/report pages and a live analytics page.

Check that the report opens without missing-data errors and that the model outputs agree with the final experiment files.

Key final-test values include:

|Metric|Value|
|-|-:|
|Accuracy|98.00%|
|Precision (malicious)|97.92%|
|Recall (malicious)|91.96%|
|F1-score (malicious)|94.85%|
|ROC-AUC|98.82%|
|False Positives|5,202|
|False Negatives|21,386|
|True Positives|244,719|
|True Negatives|1,060,600|

A major attack-level finding is that **21,161 of the 21,386 false negatives are Infilteration records**.

If a dashboard screenshot or old static resource disagrees with the final CSV/JSON outputs, treat the final analytical CSV/JSON files as the authoritative result source.

\---

## Step 6 — Main Dashboard Evidence Files

The Power BI semantic model uses the following files for its main analytical views:

### Model performance

```text
model\_metrics.csv
model\_summary.csv
confusion\_matrix.csv
```

### Attack-level analysis

```text
errors\_by\_attack\_label.csv
performance\_by\_attack\_label.csv
performance\_by\_test\_file.csv
```

### Error confidence analysis

```text
errors\_by\_confidence\_band.csv
```

### Explainability

```text
feature\_importance.csv
```

\---

## Troubleshooting

### The `.pbip` file does not open

Update Power BI Desktop to a current version and check the Power BI Project/PBIP preview setting under:

```text
File → Options and settings → Options → Preview features
```

\---

### Power BI says a CSV file cannot be found

The project currently contains absolute source paths from the development machine.

Update them through:

```text
Transform data → Data source settings → Change Source
```

and point them to the CSV files inside:

```text
powerbi/CyberXAI\_FINAL\_STABLE\_V9/
```

\---

### The dashboard opens but contains blank visuals

Run:

```text
Home → Refresh
```

If the refresh fails, check the CSV source paths.

\---

### A screenshot shows different values from the CSV files

Use the **final CSV/JSON analytical outputs** as the source of record.

The project archive contains material from more than one dashboard iteration, so old static screenshots should not override the frozen experiment outputs.

\---

## Recommended Repository Structure

```text
CyberXAI-CSE-CIC-IDS2018/
│
├── README.md
├── HOW\_TO\_RUN\_DASHBOARD.md
│
├── notebooks/
├── documentation/
├── outputs/
├── models/
│
└── powerbi/
    └── CyberXAI\_FINAL\_STABLE\_V9/
        ├── CyberXAI\_FINAL\_STABLE\_V9.pbip
        ├── CyberXAI\_FINAL\_STABLE\_V9.Report/
        ├── CyberXAI\_FINAL\_STABLE\_V9.SemanticModel/
        ├── confusion\_matrix.csv
        ├── errors\_by\_attack\_label.csv
        ├── errors\_by\_confidence\_band.csv
        ├── feature\_importance.csv
        ├── model\_metrics.csv
        ├── model\_summary.csv
        ├── performance\_by\_attack\_label.csv
        └── performance\_by\_test\_file.csv
```

\---

## Notes

* The dashboard is intended as a reporting and interpretation layer.
* The machine-learning metrics are generated in Python first.
* Power BI imports the saved analytical results rather than independently recalculating the final machine-learning experiment.
* Keep the `.pbip`, `.Report`, and `.SemanticModel` components together because they form one Power BI project.
* Large raw CSE-CIC-IDS2018 dataset files are not required simply to view the final dashboard if the final analytical CSV files are available.

\---

## Project Repository

**CyberXAI-CSE-CIC-IDS2018**

```text
https://github.com/Sami813/CyberXAI-CSE-IDS2018
```

