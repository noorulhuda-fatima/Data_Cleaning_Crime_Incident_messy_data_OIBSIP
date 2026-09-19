# Crime Incident Data Cleaning: A Systematic Approach to Analysis-Ready Data
# Oasis Infobyte Internship Project

## Project Overview

This project demonstrates a complete, professional-grade data cleaning workflow applied to a deliberately messy, real-world-style crime incident dataset. Rather than simply removing errors, every cleaning decision was made deliberately and documented — including which missing values were imputed, which were removed, and which were intentionally preserved as meaningful gaps rather than fabricated. The outcome is a fully validated, analysis-ready dataset with a transparent audit trail from raw data to final output.

## Dataset Overview

| Detail | Value |
|---|---|
| Source file | crime_incidents_messy.csv(https://www.kaggle.com/datasets/sananshaikh/messy-crime-dataset-for-data-cleaning-practice/data?select=crime_incidents_messy.csv)|
| Rows (raw) | 5,250 |
| Rows (cleaned) | 4,721 |
| Total columns | 33 |
| File format | CSV |

Column names (33 total):
incident_id, crime_type, district, city, state, address, latitude, longitude, incident_datetime, officer_id, officer_first_name, officer_last_name, badge_number, suspect_id, suspect_first_name, suspect_last_name, suspect_age, suspect_gender, suspect_race, victim_id, victim_first_name, victim_last_name, victim_age, victim_gender, victim_phone, weapon_used, severity, case_status, resolution, num_arrests, property_loss_usd, reported_online, notes

## Methodology

The cleaning process followed a structured eight-stage pipeline, with each stage building directly on the previous one:

1. Data Quality Audit — profiled null counts, data type mismatches, and value-range anomalies before any modification was made
2. Duplicate Removal — deduplicated records using the natural key (incident_id) rather than exact full-row matching
3. Standardisation — consolidated 182 raw spelling and case variants of crime_type into 18 clean categories, and applied the same approach to district, gender, status, and severity fields; unified three inconsistent date formats into a single datetime column
4. Outlier Detection — applied the IQR method to statistically-bound numeric fields (age, monetary loss) and domain-based validation rules to physically-bound fields (coordinates, counts)
5. Missing Data Handling — selected an imputation strategy (median, mode, constant label, or row deletion) individually for each column, based on the nature of that specific field, rather than applying one blanket rule
6. Data Type Correction — enforced correct data types across all 33 columns, including nullable integers, floats, datetime, and boolean types
7. Before-and-After Validation — quantified every improvement through a structured comparison table
8. Export — saved the final cleaned dataset for downstream analysis

## Key Highlights

- Reduced 182 inconsistent crime_type spellings and case variants down to 18 standardized categories
- Identified and removed 200 exact duplicate incident records
- Detected and corrected 741 biologically impossible age values, including negative ages and values as high as 298
- Identified 176 geographically impossible coordinate values (latitude readings exceeding valid Earth ranges)
- Brought 32 of 33 columns to their correct data type, up from only 6 in the raw file
- Every missing-value decision is explicitly justified rather than applied by default, including the rationale for values deliberately left unfilled

## Results: Before vs. After Cleaning

| Metric | Before Cleaning | After Cleaning |
|---|---|---|
| Row count | 5,250 | 4,721 |
| Column count | 33 | 33 |
| Total null cells | 16,478 | 4,098 (intentionally retained; see Limitations) |
| Duplicate rows | 200 | 0 |
| Correct-dtype columns (of 33) | 6 | 32 |
| crime_type categories | 182 | 18 |
| district categories | 131 | 10 |
| Invalid latitude/longitude values | 176 | 0 |
| Invalid age values | 741 | 0 |

## Limitations

- 4,098 null values remain by deliberate design, not oversight. These are concentrated in suspect_id, victim_id, badge_number, and victim_phone, where a blank value represents a genuine real-world fact — for example, a suspect who was never identified — rather than a data-entry gap. Filling these fields would have meant fabricating information.
- 329 rows were removed because their incident_datetime could not be reliably parsed or was missing entirely, since a crime's timestamp cannot be reasonably estimated or guessed.
- Date parsing assumes dash-separated dates follow a day-first format and slash-separated dates follow a month-first format, consistent with common US data conventions. This is a documented assumption rather than a verified fact.
- Certain crime_type category mappings required subjective judgment (for example, classifying "Battery" under "Assault"), which a subject-matter expert might categorize differently.

## Tools Used

Python 3
pandas — data manipulation and cleaning
numpy — numeric operations and missing-value handling
Jupyter Notebook — development environment

## How to Run

1. Clone or download this repository
2. Ensure crime_incidents_messy.csv is located in the same directory as the notebook
3. Install the required dependencies:
   pip install pandas numpy jupyter
4. Launch the notebook:
   jupyter notebook crime_data_cleaning.ipynb
5. Run all cells sequentially from top to bottom (Kernel then Restart and Run All), since later stages depend on transformations performed in earlier cells
6. The cleaned dataset will be saved as crime_incidents_cleaned.csv in the same directory

## Author
Noor Ul Huda Fatima-Data Analytics Intern at Oasis Infobyte

GitHub: [https://github.com/noorulhuda-fatima]

LinkedIn: [www.linkedin.com/in/noor-ul-huda-fatima-a01382387]
