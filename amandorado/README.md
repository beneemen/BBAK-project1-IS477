# Amanda Dorado

Contribution for IS 477 Project 1.

# BJ Mensah

Contribustion for IS 477 Project 1.
# Census Median Household Income Data (2015–2024)

## Overview
This portion of our IS477 project focuses on collecting, assessing, and cleaning median household income data from the U.S. Census Bureau's American Community Survey (ACS).

The cleaned data will be integrated with housing prices, unemployment rates, and mortgage interest rates to examine the relationship between economic conditions and housing prices across U.S. states.

## Data Source

- **Source:** U.S. Census Bureau
- **Dataset:** American Community Survey (ACS) 1-Year Estimates
- **Variable:** B19013_001E (Median Household Income)
- **Geographic Level:** State-level data, including Washington, D.C. and Puerto Rico
- **Years:** 2015–2019 and 2021–2024

The standard 2020 ACS 1-Year Estimates were not released due to COVID-19-related data collection disruptions.

## Data Collection
Data was collected using the U.S. Census Bureau API with Python's `requests` library and combined using `pandas`.

The raw dataset contains 468 records representing 52 geographic areas across 9 years.

## Data Quality Assessment
Initial data quality checks identified the following:

- **Completeness:** No missing values were detected in the collected records. However, 2020 data is unavailable.
- **Consistency:** No duplicate state-year combinations were found. Income values were initially stored as strings.
- **Accuracy:** Income values were converted to numeric values and checked for invalid or nonpositive values.
- **Timeliness:** Data covers 2015–2024, excluding 2020.

## Data Cleaning
The following cleaning operations were performed using Python and pandas:

1. Renamed columns for readability and consistency.
2. Converted median household income values to numeric format.
3. Treated nonpositive income values as missing.
4. Standardized state names by removing extra whitespace.
5. Formatted state FIPS codes as two-character strings.

After cleaning, the dataset contains 468 records and 4 columns, with no missing income values or duplicate state-year combinations.

## Files
- `census_income_collection.ipynb` — Python notebook containing data collection, quality assessment, and cleaning.
- `census_income_raw.csv` — Original collected Census data.
- `census_income_cleaned.csv` — Cleaned household income data prepared for integration.

## Limitations and Next Steps
The primary limitation is the absence of standard 2020 ACS 1-Year data. This gap will need to be considered when integrating the income dataset with the other economic datasets.

Future work includes ensuring consistent geographic identifiers across datasets, integrating household income data with the group's other sources, and conducting post-integration data quality assessments.

## References
U.S. Census Bureau. American Community Survey (ACS) 1-Year Estimates, Table B19013:
