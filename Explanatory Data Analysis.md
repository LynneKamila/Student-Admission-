# **Exploratory Data Analysis**

**Overview**

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

**Data Dictionary**

The table below contains an example of the data dictionary of the data.

|     |     |     |     |
| --- | --- | --- | --- |
| **Column Name** | **Data Type** | **Example Value** | **Description** |
| Reference_ID | integer | 45405320 | Unique identifier assigned to each applicant. |
| Given_Name | text | Deeksha Reddy | Applicant first name. |
| Last_Name | text | Bhumireddy | Applicant surname. |
| College | text | INDIA - Osmania University - Bachelor's Degree | Name of the applicant's prior educational institution and degree type |
| Major | text | NULL | Field of study at prior institution |
| Degree_Type | text | NULL | Type of degree pursued at DePaul |
| Country | text | India | Country of origin of applicant. |
| Recieved_At | integer | 1757494436974 | Timestamp when application was received. |
| Counsler | text | NULL | EMPTY COLUMN |
| University | text | DePaul University | Name of the institution (DePaul University). |
| Citizenship | text | NULL | Citizenship status of applicant. |
| Status | text | NULL | Application status |

**Data Quality Report**

An initial data profiling and quality assessment of the dataset revealed several critical anomalies, missing values, and structural issues that require remediation before further analysis:

- **Completely Empty Fields:** A total of 22 columns contain zero data and are entirely blank. This includes critical fields such as status, citizenship, Is_Admitted, Date_of_Birth, Major, and Degree_Type.
- **Inconsistent Placeholders:** The dataset lacks standardized null values. Instead of clean blanks, multiple fields utilize non-standard placeholders such as "?", "Unknown", and "Not Specified".
- **Data Corruption (Timestamps):** The datetime fields Recieved_At, Created_At, and Modified_At are stored as epoch milliseconds. Alarmingly, all 7,543 records share the exact same timestamp ($1757494436974$), indicating a major data corruption or logging error during data extraction.
- **Duplicate Records:** High rates of applicant duplication were identified. For instance, Reference_ID **291925** erroneously appears 9 separate times across the dataset.
- **Critical Missing Values**

The following table highlights key operational fields with significant missing data and their respective impact on downstream analysis:

| **Column** | **Missing Records (%)** | **Analytical Impact** |
| --- | --- | --- |
| Admit_Date | 1,754 (23.2%) | Over 23% of official admission timelines and outcomes cannot be verified. |
| Comments | 1,625 (21.5%) | Crucial qualitative outreach and counseling notes are missing for one-fifth of the records. |
| Date_of_Contact | 3,194 (42.4%) | Nearly half of the recruitment effort timeline is untraceable, preventing longitudinal tracking. |

**Exploratory Data Analysis**

**Finding 1: Extreme Geographic Concentration from India**

India dominates the applicant pool at 4,617 applicants, representing 61.2% of all 7,543 records. The next largest market is the United States at 10%, followed by Ghana (5.6%), Nigeria (5.7%), and Pakistan (2.8%). No other country exceeds 2%.

**Impact:** The applicant pipeline is heavily dependent on a single geographic source. If recruitment from India faces any disruption visa policy changes, economic shifts, or competition the total application volume drops by more than half. This represents significant pipeline risk for DePaul's admissions strategy.

**Finding 2: Duplicate records**

Out of the total 7,543 records in this snapshot, nearly half the dataset is redundant data. Only **53.0% (4,000 records)** represent unique applicants, while the remaining **47.0% (3,543 records)** consist of duplicate entries.  

**Finding 3: Study Group Channel Outperforms Standard Applications**

Applicants acquired through the Study Group channel admit at 87%, compared to 13% for non-Study Group. This suggests Study Group either pre-screens more effectively or attracts higher-quality applicants.

**Impact:** If scalable, the Study Group channel could significantly improve overall conversion rates. With 13% of current applicants coming through this channel, there may be room to increase investment in this acquisition source.

**Finding 4: Outreach counsellors**

A critical segment of **3,194 applicants (42.4%)** contains no recorded Date_of_Contact or tracking history. This indicates that either these 3,194 students were completely missed during counsellor outreach efforts, or the individual counsellors responsible for the contact failed to log their names and interaction timelines into the tracking system. This lack of documentation creates a massive operational blind spot, making it impossible to audit recruitment timelines or accurately evaluate counsellor productivity.

**Recommendations**

- **Execute a Rigorous Data Cleaning and De-duplication Protocol:** Before performing any further modeling or reporting, a data-clearing pipeline must be established to remove the 3,543 redundant duplicate rows and isolate the true 4,000 unique records. This will eliminate analytical bias, fix the skewed application metrics, and provide stakeholders with an accurate, single-source-of-truth view of the actual student pipeline.
- **Investigate Channel Variables ("Study Group vs. Standard Funnels"):** Conduct a deep-dive comparative analysis to identify exactly why the Study Group channel achieves an 87.3% admission rate compared to the 75.1% rate of standard applications. Evaluate specific underlying factors affecting student applications across these channels—such as candidate qualification profiles, document completion rates, and the impact of dedicated counselor follow-ups—to replicate these high-conversion behaviors across the entire admissions funnel.
- **Perform a Granular Geographic Optimization Study:** Expand the geographic analysis beyond high-level country counts to examine regional concentrations (using fields like City and Region). Pinpoint exactly which specific states, provinces, or metropolitan hubs within dominant markets like India are driving the volume, and evaluate whether auxiliary markets like Nigeria and Ghana possess similar high-yield urban centers that can be targeted to diversify pipeline risk.