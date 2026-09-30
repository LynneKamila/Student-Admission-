**DePaul University Graduate Admissions  
Exploratory Data Analysis Report**

**1\. Overview**

This report documents the exploratory stage of the DePaul University graduate admissions analytics project. The purpose of EDA is to understand the structure and quality of the data, describe applicant and admissions patterns, identify notable relationships and anomalies, and establish a reliable evidence base for the subsequent explanatory analysis.

# **2\. Project Objective**

The main objective of the project is to analyze graduate admissions applicant data to understand application volume, admission outcomes, applicant geography, program demand, recruitment channels, intake patterns, and documented outreach activity.

The exploratory analysis addresses the following objectives:

- Determine the number of applicants and admission outcomes across the available intake periods and years.
- Understanding the data to point out anomalies and check the data quality before cleaning.
- Identify the countries that contribute the highest number of applicants.
- Identify the graduate programs that attract the highest number of applications.
- Compare observed admission outcomes across countries, programs, colleges, application source, and Study Group status.
- Examine available outreach and contact information to understand how much applicant engagement is documented.
- Identify data-quality issues and limitations that may affect interpretation of admissions patterns.

# **3\. Dataset Overview**

The DePaul dataset is an international graduate student applicant tracking dataset used by a recruitment consultancy (Study Group) that manages admissions outreach on behalf of DePaul University. The dataset contains 7543 rows and 80 columns. The table below represents a snapshot of the dataset.

|     |     |
| --- | --- |
| Group | Columns |
| Applicant identity | Reference_ID, Given_Name, Last_Name, Date_of_Birth |
| Geography | Country, City, Region, Citizenship |
| Academic background | College, College_1st_Choice, Degree Type |
| Application details | Intake, Major, Application_Source, Recieved_At |
| Outcome | Admit_Date, Is_Admitted, Status, Most_Recent_Released_Decision |
| Process/outreach | Comments, Outcome_1, Caller_Name, Date_of_Contact |

**4\. Data Dictionary**

The table below contains an example of the data dictionary of the dataser in order to understand what the data is composed of.

|     |     |     |     |
| --- | --- | --- | --- |
| Column Name | Data Type | Example Value | Description |
| Reference_ID | integer | 45405320 | Unique identifier assigned to each applicant. |
| Given_Name | text | Deeksha \*\*ddy | Applicant first name. |
| Last_Name | text | Bhum\*\*\*\* | Applicant surname. |
| College | text | INDIA - Osmania University - Bachelor's Degree | Name of the applicant's prior educational institution and degree type |
| Major | text | NULL | Field of study at prior institution |
| Degree_Type | text | NULL | Type of degree pursued at DePaul |
| Country | text | India | Country of origin of applicant. |
| Recieved_At | integer | 1757494436974 | Timestamp when application was received. |
| Counselor | text | NULL | EMPTY COLUMN |
| University | text | DePaul University | Name of the institution (DePaul University). |
| Citizenship | text | NULL | Citizenship status of applicant. |
| Status | text | NULL | Application status |

**5\. Data Quality Report**

An initial data profiling and quality assessment of the dataset revealed several critical anomalies, missing values, and structural issues that require remediation before further analysis:

1.  **Completely Empty Fields:** A total of 22 columns contain zero data and are entirely blank. This includes critical fields such as status, citizenship, is_Admitted, Date_of_Birth, Major, and Degree_Type.
2.  **Inconsistent Placeholders:** The dataset lacks standardized null values. Instead of clean blanks, multiple fields utilize non-standard placeholders such as "?", "Unknown", and "Not Specified".
3.  **Data timestamps:** Recieved_At, Created_At, and Modified_At are stored as epoch-millisecond values. The raw snapshot shows the same timestamp value, 1757494436974, across all 7,543 records. Because there is no useful variation in these fields, they cannot support meaningful temporal analysis in their current form.
4.  **Duplicate Records:** Repeated applicant identifiers are present in the raw snapshot. For example, Reference_ID 291925 appears nine times. Across the 7,543-row snapshot, profiling identified 4,000 distinct applicant identifiers and 3,543 repeated/duplicate-looking records. This is treated as a data-quality observation rather than a final claim that all repeated records are erroneous or redundant.
5.  **Critical Missing Values:** Some record do not contain any data and are blank which may lead to incorrect data information during analysis.

The following table highlights key operational fields with significant missing data and their respective impact on downstream analysis:

| **Column** | **Missing Records (%)** | **Analytical Impact** |
| --- | --- | --- |
| Admit_Date | 1,754 (23.2%) | Over 23% of official admission timelines and outcomes cannot be verified. |
| Comments | 1,625 (21.5%) | Crucial qualitative outreach and counselling notes are missing for one-fifth of the records. |
| Date_of_Contact | 3,194 (42.4%) | Nearly half of the recruitment effort timeline is untraceable, preventing longitudinal tracking. |

**6\. Exploratory Data Analysis**

**Finding 1: Extreme Geographic Concentration from India**

India dominates the applicant pool at 4,617 applicants, representing 61.2% of all 7,543 records. The next largest market is the United States at 10%, followed by Ghana (5.6%), Nigeria (5.7%), and Pakistan (2.8%). No other country exceeds 2%.

<img width="750" height="453" alt="image" src="https://github.com/user-attachments/assets/4747d051-b9a1-4706-b02e-3522b4bb025e" />

**Finding 2: Duplicate records**

Out of the total 7,543 records in this snapshot, nearly half the dataset is redundant data. Only **53.0% (4,000 records)** represent unique applicants, while the remaining **47.0% (3,543 records)** consist of duplicate entries.

  <img width="823" height="392" alt="image" src="https://github.com/user-attachments/assets/4d9226ea-8baa-4b85-8687-7b437fc1c40e" />


**Finding 3: Study Group Channel Outperforms Standard Applications**

Applicants acquired through the Study Group channel are at 13%, compared to 87% for non-Study Group. Non Study Group applicants have a higher observed application rate than Study Group applicants in this dataset. This is an association in the observed data; the analysis does not establish that Study Group participation causes a higher probability of admission.

.<img width="691" height="354" alt="image" src="https://github.com/user-attachments/assets/d174bc33-d849-4269-befc-23a02a8b3a5f" />


**Finding 4: Outreach counsellors**

A critical segment of **3,194 applicants (42.4%)** contains no recorded Date_of_Contact or tracking history. This indicates that either these 3,194 students were completely missed during counsellor outreach efforts, or the individual counsellors responsible for the contact failed to log their names and interaction timelines into the tracking system.

<img width="752" height="452" alt="image" src="https://github.com/user-attachments/assets/8fe4cfca-10ac-4948-be4c-55a10292e84f" />

## **Finding 5: Application Patterns**

The application year field shows the highest application volumes in 2025 and 2024. There are 290 records with a missing application year, which limits complete year-over-year comparison.

|     |     |     |
| --- | --- | --- |
| **Intake Year** | **Applicants** | **Share** |
| 2022 | 1   | 0.0% |
| 2023 | 164 | 3.3% |
| 2024 | 2,200 | 44.0% |
| 2025 | 2,307 | 46.1% |
| 2026 | 38  | 0.8% |
| Missing | 290 | 5.8% |

At the application -period level, September 2024 has the largest recorded volume (1,383 applicants), followed by September 2025 (1,211) and January 2024 (658). Some application-period values remain missing or inconsistently formatted, so temporal comparisons should use the standardized fields and their quality flags.

## **Finding 6: Intake Patterns**

Business Analytics is the largest program by applicant volume, with 846 applicants (16.9%), followed by Computer Science (607) and Data Science (337).

<img width="940" height="556" alt="image" src="https://github.com/user-attachments/assets/c3951d09-edac-42ad-91b8-38d7eb9b4f4c" />

# **7\. Initial EDA Findings**

- The raw dataset contains 7,543 records across 80 columns and includes applicant, geographic, academic, application, outcome, and outreach information.
- Applicant records are strongly concentrated in India, which represents 61.2% of the raw snapshot.
- The raw dataset contains substantial missingness, including 42.4% missing Date_of_Contact and 23.2% missing Admit_Date.
- Repeated applicant identifiers and duplicate-looking records are present and must be reviewed before final applicant-level counts are reported.
- Twenty-two columns are entirely blank, while several other fields use inconsistent placeholders such as '?', 'Unknown', and 'Not Specified'.
- The system timestamp fields do not provide useful temporal variation in the supplied snapshot.
- Admission-related information is present in multiple fields but requires validation and a consistent definition before an admission-status KPI can be calculated.
- Program and intake fields require interpretation and standardization before reliable demand and temporal comparisons are made.

# **8\. Data Preparation Priorities for the Next Stage**

The EDA identifies the following requirements for the separate Data Cleaning Report. These are preparation priorities rather than cleaned-data findings:

- Review repeated Reference_IDs and determine the appropriate applicant-level record structure.
- Standardize missing-value representations and distinguish true categories from placeholders.
- Assess the 22 empty columns and document whether they should be excluded from the analytical model.
- Validate and standardize admission-related fields and document the rule used to derive a consistent admission status.
- Review the meaning and structure of the raw Intake field before using it for program or temporal analysis.
- Standardize country, source, date, and other categorical fields where inconsistent values exist.
- Exclude or appropriately handle constant system timestamps that cannot support meaningful analysis.
- Preserve missingness indicators where missing information has analytical significance rather than silently imputing uncertain values.

# **9\. Limitations and Assumptions**

- The dataset represents applicant/admissions activity and does not establish confirmed student enrollment or registration.
- The raw snapshot contains repeated applicant identifiers; therefore, raw record counts should not automatically be interpreted as unique applicants.
- Missing contact dates indicate that contact information is not recorded, not that outreach definitely did not occur.
- The raw EDA does not infer reasons for admission or non-admission.
- Observed geographic concentrations are descriptive and do not establish recruitment effectiveness or applicant quality.
- The supplied dataset cannot establish causes of observed patterns where relevant explanatory variables are absent.
- The constant system timestamps are not suitable for meaningful time-series analysis in their current form.

# **10\. Conclusion**

The exploratory analysis provides an initial evidence base for understanding the original DePaul graduate admissions dataset before cleaning. The raw snapshot contains 7,543 records and 80 columns, with information covering applicant geography, academic background, application details, admission-related fields, and outreach.

The EDA identifies several issues that affect direct interpretation, including repeated applicant identifiers, substantial missingness, non-standard placeholders, entirely blank columns, ambiguous field definitions, and constant system timestamps. It also shows a strong geographic concentration in India and highlights the need to validate program, intake, and admission-related fields before producing final analytical KPIs.

The next stage is the Data Cleaning Report. That stage should document the treatment of duplicates, missing values, inconsistent categories, timestamp fields, field definitions, and the derivation of a consistent admission-status variable. Only after those steps should the cleaned dataset be used for Explanatory Data Analysis and the Power BI dashboard.
