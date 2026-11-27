# HR Analytics - Employee Attrition Analysis
An HR analytics project analysing employee attrition patterns, workforce characteristics and performance indicators using Power query, SQL, Power BI to uncover insights that support employee retention and data-driven HR decisions.


## 1. Project Overview

Employee attrition is an important workforce management challenge for organisations. Understanding the patterns associated with employees leaving can help organisations identify areas that may require attention and develop strategies to improve employee retention.

This project explores employee data to identify patterns and factors associated with employee attrition. The analysis focuses on employee demographics, job roles, compensation, job satisfaction, work experience and other work place-related factors.

### Business Question

What factors are associated with employee attrition, and what can the organisation do to improve employee retention?

## 2. Project Objectives

The objectives of this analysis are to:

- Calculate the overall employee attrition rate.
- Identify departments with higher employee attrition.
- Determine which job roles experience higher turnover.
- Examine the relationship between overtime and employee attrition.
- Investigate the relationship between monthly income and attrition.
- Explore how job satisfaction and work-life balance relate to attrition.
- Examine attrition patterns across different age groups.
- Investigate the relationship between employee experience, length of service and retention.
- Provide data-driven recommendations to support employee retention.

## 3. Tools 

| Tool | Purpose |
|---|---|
| Power Query | Data exploration, cleaning and preparation |
| Power BI | visualisation and dashboard development |
| GitHub | Project documentation |

## 4. Dataset Overview

The project uses the IBM HR Analytics Employee Attrition dataset.

The dataset contains employee information covering demographics, job characteristics, compensation, satisfaction, work experience and attrition status.

### Dataset Information

| Attribute | Details |
|---|---|
| Dataset | IBM HR Analytics Employee Attrition |
| Initial Records | 1,470 |
| Initial Columns | 35 |
| Records Represent | Individual employees |
| Target Variable | Attrition |

## 5. Data Exploration

Before performing data cleaning, I explored the dataset to understand its structure, identify the available variables and assess its quality.

The initial exploration involved:

- Reviewing the number of rows and columns.
- Examining column names and data types.
- Understanding the variables and their relevance to the analysis.
- Checking for missing values.
- Identifying duplicate records.
- Checking the uniqueness of employee identifiers.
- Reviewing categorical columns for inconsistent entries.
- Examining numerical columns for unusual or invalid values.
- Investigating zero values in numerical columns.

This initial assessment provided an understanding of the dataset and helped determine the necessary data preparation steps.

## 6. Data Cleaning and Preparation

Data cleaning and preparation were performed using Power Query to improve consistency, validate the data and prepare it for analysis.

### 6.1 Column Header Standardisation

Reviewed and standardised column headers to improve readability and maintain consistency throughout the dataset.

### 6.2 Missing Values Assessment

Checked the dataset for missing and null values.

**Result:** No missing values were identified.

### 6.3 Duplicate Records Assessment

Checked for duplicate rows and reviewed the `EmployeeNumber` column to ensure that employee identifiers were unique.

**Result:** No duplicate records or duplicate employee identifiers were identified.

### 6.4 Text Standardisation

Reviewed categorical columns for inconsistent text formatting.

The `BusinessTravel` column contained values with underscores. These were standardised using the Replace Values transformation in Power Query.

| Original Value | Standardised Value |
|---|---|
| `Travel_Rarely` | `Travel Rarely` |
| `Travel_Frequently` | `Travel Frequently` |

The `Non-Travel` category was retained.

### 6.5 Data Type Validation

Reviewed the data types of the columns to ensure that numerical fields were stored as numeric values and categorical fields were appropriately assigned as text.

Special attention was given to numerical fields such as `MonthlyIncome` and `PercentSalaryHike` to ensure they were interpreted correctly.

### 6.6 Investigation of Zero Values

During data exploration, zero values were identified in several numerical columns.

Rather than treating all zero values as missing or invalid data, I examined the meaning of each column to determine whether zero represented a valid observation.

| Column | Number of Zero Values |
|---|---:|
| `NumCompaniesWorked` | 197 |
| `StockOptionLevel` | 631 |
| `TotalWorkingYears` | 11 |
| `TrainingTimesLastYear` | 54 |
| `YearsAtCompany` | 44 |
| `YearsInCurrentRole` | 244 |
| `YearsSinceLastPromotion` | 581 |
| `YearsWithCurrManager` | 263 |

**Decision:** The zero values were retained because they can represent valid employee information, such as no previous companies recorded, no training sessions during the previous year, or no completed years since a promotion.

These values were not replaced with blanks, averages or arbitrary numbers.

### 6.7 Identification and Removal of Constant Columns

During the data quality assessment, three columns were found to contain the same value across all 1,470 employee records.

| Column | Constant Value | Action |
|---|---|---|
| `EmployeeCount` | 1 | Removed |
| `Over18` | Y | Removed |
| `StandardHours` | 80 | Removed |

These columns were excluded from the analytical dataset because they contained no variation and would not contribute meaningful information to the analysis.

The `EmployeeNumber` column was retained as a unique employee identifier and will not be treated as a numerical measure.

### 6.8 Data Validation

Additional checks were performed on employment-related columns to identify potentially inconsistent records.

The following relationships were examined:

- `YearsAtCompany` against `TotalWorkingYears`.
- `YearsInCurrentRole` against `YearsAtCompany`.
- `YearsWithCurrManager` against `YearsAtCompany`.
- `YearsSinceLastPromotion` against `YearsAtCompany`.
- `TotalWorkingYears` against employee age.

**Result:** No violations were identified in the relationships checked.

### 6.8 Categorical Value Standardization

Replaced numeric codes with their corresponding descriptive labels in the following columns using the dataset's source documentation:

- `Education`
- `EnvironmentSatisfaction`
- `JobInvolvement`
- `JobSatisfaction`
- `PerformanceRating`
- `RelationshipSatisfaction`
- `WorkLifeBalance`

### 6.9 Text Data Cleaning

Applied the Trim and Clean transformations to relevant text columns as a preventive measure to remove potential leading or trailing spaces and non-printable characters, ensuring consistency across text fields.

## 7. Data Cleaning Summary

The data preparation process resulted in the following:

| Metric | Initial Dataset | Prepared Dataset |
|---|---:|---:|
| Rows | 1,470 | 1,470 |
| Columns | 35 | 32 |
| Missing Values | 0 | 0 |
| Duplicate Rows | 0 | 0 |
| Duplicate Employee Numbers | 0 | 0 |

The three constant columns were excluded, while valid zero values and all employee records were retained.

The prepared dataset is now ready for further exploratory data analysis and subsequent SQL analysis.

### Dataset Before Cleaning
![Before Cleaning](HR%20Attrition%20-%20Before%20Cleaning.png)

### Dataset After Cleaning
![After Cleaning](HR%20Attrition%20-%20After%20Cleaning.png)



## 8. Exploratory Data Analysis (EDA)

Exploratory Data Analysis was performed using Power BI to investigate employee attrition patterns and identify workforce characteristics associated with employees leaving the organisation.

The analysis focused on overall attrition, department, job role, overtime, compensation, job satisfaction, work-life balance, age groups, employee experience, distance from home, marital status, performance rating and business travel.

### 8.1 Overall Employee Attrition

The dataset contains 1,470 employee records. An initial assessment of employee attrition produced the following results:

| Metric | Value |
|---|---:|
| Total Employees | 1,470 |
| Employees Who Left | 237 |
| Active Employees | 1,233 |
| Overall Attrition Rate | 16.12% |

The organisation recorded an overall attrition rate of 16.12%, meaning approximately 16 out of every 100 employees in the dataset left the organisation.

### 8.2 Departmental Attrition Analysis

Employee attrition was examined across the three departments to identify where turnover was more pronounced.

| Department | Attrition Count | Attrition Rate |
|---|---:|---:|
| Research & Development | 133 | 13.84% |
| Sales | 92 | 20.63% |
| Human Resources | 12 | 19.05% |

**Key Findings:**

- Research & Development recorded the highest attrition count, with 133 employees leaving.
- Sales recorded the highest attrition rate at 20.63%, despite having fewer departures than Research & Development.
- Human Resources recorded an attrition rate of 19.05%.

Research & Development had the highest number of departures, while Sales had the highest attrition rate. This distinction is important because departmental employee populations differ in size.

### 8.3 Attrition by Job Role

Attrition rates were compared across job roles to identify positions experiencing higher employee turnover.

| Job Role | Attrition Rate |
|---|---:|
| Sales Representative | 39.76% |
| Laboratory Technician | 23.94% |
| Human Resources | 23.08% |
| Sales Executive | 17.48% |
| Research Scientist | 16.10% |
| Manufacturing Director | 6.90% |
| Healthcare Representative | 6.87% |
| Manager | 4.90% |
| Research Director | 2.50% |

**Key Findings:**

- Sales Representatives recorded the highest attrition rate at 39.76%.
- Laboratory Technicians followed with 23.94%.
- Human Resources employees recorded an attrition rate of 23.08%.
- Research Directors recorded the lowest attrition rate at 2.50%.

The findings indicate that attrition varies considerably across job roles, with Sales Representatives experiencing particularly high turnover.

### 8.4 Overtime and Employee Attrition

The relationship between overtime and employee attrition was examined by comparing the attrition rates of employees who work overtime with those who do not.

| Overtime Status | Attrition Count | Attrition Rate |
|---|---:|---:|
| Yes | 127 | 30.53% |
| No | 110 | 10.44% |

**Key Findings:**

- Employees who work overtime recorded an attrition rate of 30.53%.
- Employees who do not work overtime recorded an attrition rate of 10.44%.
- The overtime group had an attrition rate approximately 2.92 times that of the non-overtime group.

This indicates a strong association between overtime and employee attrition. Employees working overtime were considerably more likely to leave than those who did not.

### 8.5 Monthly Income and Employee Attrition

Average monthly income was compared between employees who left the organisation and those who remained.

| Attrition Status | Average Monthly Income |
|---|---:|
| Yes (Left) | 4,787.09 |
| No (Stayed) | 6,832.74 |

**Key Findings:**

- Employees who left earned an average monthly income of 4,787.09.
- Employees who remained earned an average monthly income of 6,832.74.
- The difference between the two groups was 2,045.65.
- Employees who left earned approximately 29.9% less on average than employees who stayed.

The results suggest an association between lower average monthly income and employee attrition.

#### Average Monthly Income by Job Level

To examine this relationship further, average monthly income was compared across job levels and attrition status.

| Job Level | Employees Who Left (Yes) | Employees Who Stayed (No) |
|---|---:|---:|
| Level 1 | 2,598.13 | 2,854.41 |
| Level 2 | 5,759.79 | 5,474.50 |
| Level 3 | 9,388.41 | 9,891.03 |
| Level 4 | 13,150.40 | 15,620.29 |
| Level 5 | 19,463.80 | 19,170.58 |

**Key Findings:**

- Employees who left earned less on average at Job Levels 1, 3 and 4.
- At Job Levels 2 and 5, employees who left earned slightly more on average than those who stayed.
- The most noticeable difference occurred at Job Level 4, where employees who left earned an average of 13,150.40 compared with 15,620.29 among employees who stayed.

The relationship between monthly income and attrition was not consistent across all job levels. This suggests that compensation and attrition may be influenced by other employee and job-related factors.

*Note: The dataset does not specify a currency for the monthly income values. Therefore, no currency symbol has been assigned.*

### 8.6 Job Satisfaction and Employee Attrition

Employee attrition rates were examined across the four job satisfaction categories.

| Job Satisfaction | Attrition Rate |
|---|---:|
| Low | 22.84% |
| Medium | 16.43% |
| High | 16.52% |
| Very High | 11.33% |

**Key Findings:**

- Employees with low job satisfaction recorded the highest attrition rate at 22.84%.
- Employees with very high job satisfaction recorded the lowest attrition rate at 11.33%.
- Attrition was generally higher among employees reporting lower job satisfaction, although the Medium and High categories had very similar rates.

The results suggest that lower job satisfaction is associated with higher employee attrition.

### 8.7 Work-Life Balance and Employee Attrition

The relationship between employees' reported work-life balance and attrition was investigated.

| Work-Life Balance | Attrition Rate |
|---|---:|
| Bad | 31.25% |
| Good | 16.86% |
| Better | 14.22% |
| Best | 17.65% |

**Key Findings:**

- Employees reporting bad work-life balance recorded the highest attrition rate at 31.25%.
- Employees reporting better work-life balance recorded the lowest rate at 14.22%.
- The Best category recorded an attrition rate of 17.65%, slightly higher than the Good and Better categories.

The findings indicate that poor work-life balance is associated with higher employee attrition. However, the pattern is not strictly linear across all categories.

### 8.8 Age Groups and Employee Attrition

Employee ages were grouped into five categories to examine differences in attrition across age ranges.

| Age Group | Attrition Rate |
|---|---:|
| 18–25 | 36% |
| 26–35 | 19% |
| 36–45 | 9% |
| 46–55 | 12% |
| 56+ | 17% |

**Key Findings:**

- Employees aged 18–25 recorded the highest attrition rate at 36%.
- Employees aged 36–45 recorded the lowest attrition rate at 9%.
- Attrition generally declined across the younger age groups before increasing among employees aged 56 and above.

The results suggest that age is associated with employee attrition, with younger employees experiencing higher turnover in this dataset.

### 8.9 Employee Experience and Length of Service

Employee experience and length of service were investigated using years at the company, years in the current role and years since the last promotion.

#### A. Years at Company

Employees were grouped according to their length of service in the organisation.

| Years at Company | Attrition Rate |
|---|---:|
| 0–2 Years | 29.80% |
| 3–5 Years | 13.80% |
| 6–10 Years | 12.30% |
| 11–20 Years | 6.70% |
| 21+ Years | 12.10% |

**Key Findings:**

- Employees with 0–2 years of service recorded the highest attrition rate at 29.80%.
- Employees with 11–20 years of service recorded the lowest rate at 6.70%.
- Attrition generally declined as length of service increased, although a slight increase was observed among employees with over 20 years of service.

This suggests that employees in their early years with the organisation may be more vulnerable to attrition.

#### B. Years in Current Role

Attrition was also examined based on how long employees had occupied their current positions.

| Years in Current Role | Attrition Rate |
|---|---:|
| 0–2 Years | 22.59% |
| 3–5 Years | 11.64% |
| 6–10 Years | 10.81% |
| 11–15 Years | 7.69% |


**Key Findings:**

- Employees with 0–2 years in their current roles recorded the highest reported attrition rate at 22.59%.
- Attrition declined across the first four tenure categories.
- Employees with 11–15 years in their current roles recorded the lowest reported rate at 7.69%.

The findings suggest that employees who have spent fewer years in their current roles experience higher attrition in the reported categories.

#### C. Years Since Last Promotion

Employees were grouped according to the number of years since their last promotion to investigate the relationship between career progression and attrition.

| Years Since Last Promotion | Attrition Rate |
|---|---:|
| 0–2 Years | 16.96% |
| 3–5 Years | 10.13% |
| 6–10 Years | 18.12% |
| 11–15 Years | 12.12% |


**Key Findings:**

- Employees in the 6–10 years since last promotion category recorded the highest reported attrition rate at 18.12%.
- The 3–5 years category recorded the lowest rate at 10.13%.
- Attrition did not increase consistently with the number of years since the last promotion.

This suggests that promotion history may be associated with employee attrition, although the relationship is not linear.

### 8.10 Distance from Home and Employee Attrition

Distance from home was grouped into categories to investigate whether employees' distance from home was associated with differences in attrition rates.

| Distance Group | Attrition Rate |
|---|---:|
| 1–5 | 13.77% |
| 6–10 | 14.47% |
| 11–15 | 21.74% |
| 16–20 | 18.40% |
| 21+ | 22.06% |

**Key Findings:**

- Employees in the 21+ distance category recorded the highest attrition rate at 22.06%.
- Employees in the 11–15 category also recorded a relatively high rate of 21.74%.
- Employees in the 1–5 category recorded the lowest attrition rate at 13.77%.
- The higher distance categories generally recorded higher attrition rates, although the pattern was not strictly linear.

The findings suggest an association between distance from home and employee attrition. This may be an area worth investigating further when considering employees' commuting and workplace arrangements.

*Note: The dataset does not specify the unit of measurement for DistanceFromHome. Therefore, the categories are presented without describing the values as miles, kilometres or travel time.*

### 8.11 Marital Status and Employee Attrition

Employee attrition rates were compared across marital status categories to identify differences in turnover.

| Marital Status | Attrition Rate |
|---|---:|
| Single | 25% |
| Married | 12% |
| Divorced | 10% |

**Key Findings:**

- Single employees recorded the highest attrition rate at 25%.
- Married employees recorded an attrition rate of 12%.
- Divorced employees recorded the lowest attrition rate at 10%.

The results indicate that attrition rates differ across marital status categories, with single employees recording a notably higher rate than married and divorced employees.

However, marital status alone does not explain why employees leave. Other factors, such as age, career stage and personal circumstances, may also be relevant.

### 8.12 Performance Rating and Employee Attrition

Attrition rates were examined across the two performance rating categories to determine whether employee performance ratings were associated with turnover.

| Performance Rating | Attrition Rate |
|---|---:|
| Outstanding | 16% |
| Excellent | 16% |

**Key Findings:**

- Employees rated Outstanding recorded an attrition rate of 16%.
- Employees rated Excellent also recorded an attrition rate of 16%.
- There was no noticeable difference in attrition rates between the two performance rating categories.

The findings suggest that performance rating did not show a noticeable association with employee attrition in this analysis.

### 8.13 Business Travel and Employee Attrition

Business travel was examined to investigate whether employees who travel for work experience different attrition rates from those who travel rarely or do not travel.

| Business Travel Category | Attrition Rate |
|---|---:|
| Travel Frequently | 24.91% |
| Travel Rarely | 14.96% |
| Non-Travel | 8% |

**Key Findings:**

- Employees who travel frequently recorded the highest attrition rate at 24.91%.
- Employees who travel rarely recorded an attrition rate of 14.96%.
- Employees who do not travel recorded the lowest attrition rate at 8%.
- Attrition was higher among employees who travel frequently compared with those who travel rarely or do not travel.

The findings suggest an association between frequent business travel and employee attrition. Frequent travel may be worth considering when reviewing employee workload and work-life balance. However, the dataset does not establish the reasons behind this relationship.

### 8.14 Summary of Key EDA Findings

The exploratory analysis identified several workforce characteristics associated with employee attrition.

The most notable findings include:

1. The overall employee attrition rate was 16.12%.
2. Sales had the highest departmental attrition rate at 20.63%.
3. Sales Representatives recorded the highest job-role attrition rate at 39.76%.
4. Employees who work overtime had a substantially higher attrition rate (30.53%) than those who do not (10.44%).
5. Employees who left earned approximately 29.9% less on average than employees who stayed.
6. Employees with low job satisfaction recorded a higher attrition rate than those with very high job satisfaction.
7. Employees reporting bad work-life balance recorded the highest rate at 31.25%.
8. Employees aged 18–25 recorded the highest age-group attrition rate at 36%.
9. Employees with 0–2 years of service recorded the highest attrition rate across the years-at-company categories at 29.80%.
10. Employees with 0–2 years in their current roles also recorded the highest reported attrition rate at 22.59%.
11. Employees in the 6–10 years since last promotion category recorded the highest reported attrition rate at 18.12%.
12. Employees in the 21+ distance category recorded the highest distance-group attrition rate at 22.06%.
13. Single employees recorded the highest marital-status attrition rate at 25%.
14. Performance rating showed no noticeable difference in attrition, with both Outstanding and Excellent categories recording 16%.
15. Employees who travel frequently recorded the highest business-travel attrition rate at 24.91%, while employees who do not travel recorded the lowest rate at 8%.

Overall, the findings highlight overtime, work-life balance, job role, age, job satisfaction, employee tenure, distance from home, marital status and business travel as areas worth considering when developing employee retention strategies. Performance rating, on the other hand, showed no noticeable difference in attrition across its two categories.

*Analytical note: Attrition rates represent the proportion of employees who left within each respective category.*


## 9. Power BI Dashboard Development

The dashboard development phase brings together the key findings from the exploratory data analysis into an interactive Power BI report.

### Page 1 – HR Attrition Overview

The first dashboard page provides a high-level view of employee attrition and workforce composition.

It includes:

- Total Employees
- Attrition Count
- Attrition Rate
- Active Employees
- Attrition Rate by Department
- Attrition Rate by Job Role
- Attrition Rate by Overtime

The overview page allows users to quickly assess the organisation's workforce and identify departments and job roles with higher employee turnover.

### Dashboard Screenshot

![HR Attrition Overview Dashboard](screenshots/hr-attrition-overview.png)

*Figure 1: HR Attrition Overview dashboard built using Power BI.*




