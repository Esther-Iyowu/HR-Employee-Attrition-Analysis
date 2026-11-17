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
| SQL | Data analysis and querying |
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



## 8. Next Steps

The next stages of this project will involve:

1. Exploratory Data Analysis (EDA).
2. SQL queries to investigate employee attrition patterns.
3. Power BI data modelling and dashboard development.
4. Interpretation of findings and business recommendations.

**Note:** The analysis will focus on identifying associations and patterns within the dataset. These relationships will not automatically be interpreted as proof of causation.
