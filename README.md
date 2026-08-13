# Healthcare-Patient-Insights-Dashboard-Power-BI-
An interactive Business Intelligence dashboard built in Power BI Desktop, analyzing a 40K+ record healthcare dataset covering patient demographics, medical conditions, billing, and hospital operations.

# Overview
This project explores patient-level healthcare data to surface demographic patterns, condition prevalence by age group, billing trends, and length-of-stay dynamics — packaged into a single-page interactive report with drill-down and cross-filtering.

# Data source
- Dataset: Healthcare Dataset (Kaggle) — synthetic patient records including Name, Age, Gender, Blood Type, Medical Condition, Date of Admission, Doctor, Hospital, Insurance Provider, Billing Amount, Room Number, Admission Type, Discharge Date, Medication, and Test Results.
- Note: this is a synthetic/randomly generated dataset, used here for dashboard-building and analytics practice — findings are illustrative, not real clinical conclusions.

# Features
- KPI cards — Total Patients, Total Billing, with custom icon styling
- Decomposition tree — drill from Total Patients → Medical Condition → Age Range with AI-assisted splits
- Patient Details table — expandable hierarchy (Name → Gender → Medical Condition → Doctor → Billing Amount)
- Total Patients by Quarter — trend line showing seasonal admission patterns
-  Total Patients by Age Range — donut chart segmenting patients into 0–18 / 19–35 / 36–55 / 56+ bands
- Total Billing & Average Length of Stay by Medical Condition — dual-axis combo chart comparing cost and stay duration across conditions
- Global slicers for Doctor, Hospital, and Insurance Provider
  
# Tools & techniques
- Power BI Desktop — report design, data modeling, DAX
- Power Query — data cleaning, type correction, calculated columns
- DAX measures, including:
   - Total Patients = DISTINCTCOUNT('Patients'[Name])
   - Avg Billing = AVERAGE('Patients'[Billing Amount])
   - Total Billing = SUM('Patients'[Billing Amount])
   - Avg Length of Stay = AVERAGE('Patients'[Length of Stay])
- Calculated columns, including:
   - Length of Stay = DATEDIFF('Patients'[Date of Admission], 'Patients'[Discharge Date], DAY)
   - Age Band = 
                SWITCH(
                  TRUE(),
                  'Patients'[Age] <= 18, "0–18",
                  'Patients'[Age] <= 35, "19–35",
                  'Patients'[Age] <= 55, "36–55",
                  "56+"
                )
   - Decomposition tree with AI splits, report page tooltips, conditional formatting, and display folders for measure organization
     
# Key findings
- Patients aged 36–55 make up the largest share (43%) of the dataset, followed by 19–35 (~30%)
- Arthritis and Diabetes are the most prevalent conditions by volume, with Hypertension and Cancer close behind
- Cancer cases show a notably longer average length of stay relative to other conditions
- Patient volume rises through Q1–Q3, peaking before a slight Q4 dip — a pattern worth planning capacity around (beds, equipment, medication stock) ahead of the peak rather than reacting   to it

# How to use
1. Clone this repo
2. Open dashboard.pbix in Power BI Desktop
3. Refresh the data source if pointing to a local CSV copy
  
# Author
- Built by Daniel as a hands-on Power BI / DAX / data storytelling project.
