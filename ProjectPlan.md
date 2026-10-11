# Project Plan: Housing Prices and Economic Conditions in the United States

## Overview
Our project aims to investigate how economic conditions relate to housing prices across the United States from 2015 to 2024. We chose this topic because housing affordability is an important concern for many households, and changes in income, unemployment, and mortgage interest rates may be associated with changes in home values. Our goal is to find patterns across states and over time, rather than assume that one factor directly causes housing prices to change.

We plan to collect data from Zillow Research, the U.S. Census Bureau, and Federal Reserve Economic Data (FRED). First, we will examine the structure, documentation, and quality of each dataset. We will then clean the data by addressing missing values, inconsistent state names or codes, different date formats, and possible duplicates. Since our datasets may report information at different time intervals, we will organize the data by state and year. We will then combine the datasets using matching states and years to analyze relationships between housing prices and economic conditions. Finally, we will use summary statistics and visualizations to compare trends and explore relationships between housing prices and economic indicators. We will document our process, maintain code and files in GitHub, and create a reproducible workflow.

## Team
Our four-person team will share responsibility for research, decisions, documentation, and reviewing the final submission.

-  Krissy Ho — Collect and clean housing price data from Zillow. Standardize state names and dates.
-  Amanda Dorado — Collect and clean household income data from the U.S. Census Bureau. Handle missing values and inconsistent formatting.
- BJ Mensah — Collect and clean unemployment and mortgage interest rate data from FRED. Standardize time periods.
- Ben Liang - Lead the integration of all datasets, check data quality, and help develop the final analysis.

All four members will collaborate on research questions, documentation, GitHub updates, and reviewing the final results.

## Research Questions
1. How have typical home values changed across U.S. states from 2015 to 2024?
2. What relationship exists between median household income and typical home values across states and years?
3. How are state unemployment rates associated with typical home values?
4. Which states experienced the largest changes in the ratio of typical home value to median household income?

## Datasets

| Dataset | Source | Key information | Frequency / geography | Integration key |
|---|---|---|---|---|
| Zillow Home Value Index (ZHVI) | [Zillow Research](https://www.zillow.com/research/data/) | Typical home values | Monthly, state | State + year after annual aggregation |
| American Community Survey (ACS), Table B19013 | [U.S. Census Bureau](https://data.census.gov/) | Median household income | Annual, state | State FIPS code + year |
| State unemployment rate series | [FRED](https://fred.stlouisfed.org/) (underlying labor statistics from BLS) | State unemployment rates | Monthly, state | State + year after annual aggregation |
| 30-Year Fixed Rate Mortgage Average (MORTGAGE30US) | [FRED](https://fred.stlouisfed.org/series/MORTGAGE30US) (underlying source: Freddie Mac) | National mortgage interest rates | Weekly, United States | Year after annual aggregation |

**Planned integration:** We will clean and standardize state names, dates, and other variables across the datasets. Since some datasets contain monthly data, we will calculate yearly averages to make them consistent. Next, we will combine the housing price, income, and unemployment datasets using state and year, then add national mortgage rates using year. Finally, we will check for missing or duplicate records and document the variables used in our analysis.

## Timeline

| Task | Description | Deadline | Responsible Members |
|---|---|---|---|
| Data Collection | Download housing price, income, unemployment, and mortgage rate datasets from their sources. | October 23, 2026 | Krissy, BJ Amanda |
| Data Cleaning | Handle missing values, standardize state names and dates, and organize datasets for integration. | November 2, 2026 | Krissy, Amanda, BJ |
| Data Integration | Combine datasets using state and year, and check for duplicate or missing records. | November 12, 2026 | Ben, with support from all members |
| Interim Status Report | Document completed work, challenges, and remaining tasks. Submit the status report. | November 19, 2026 | All members |
| Data Analysis | Analyze relationships between housing prices and economic conditions using summary statistics and visualizations. | November 27, 2026 | All Members |
| Final Documentation & Submission | Complete the final report, review code, and organize the GitHub repository for submission | December 4-7, 2026| All members |

## Constraints
- **Different reporting frequencies:** Our datasets report information at different time intervals. For example, Zillow reports monthly data, while Census income data is annual. Converting the data into yearly averages may cause us to lose some details about short-term changes.
- **Geographic differences:** Some datasets may use different state names, abbreviations, or codes. We will need to standardize these to combine the datasets correctly. Additionally, national mortgage rates may not reflect differences between states.
- **Missing Data:** Some datasets may have missing information for certain states or years. We will check for missing values and determine how to handle them before combining the datasets.
- **Measurement differences:** Zillow reports estimated home values rather than actual home sale prices. Income data may also need to be adjusted for inflation when comparing different years.
- **Limitations of Analysis:** Our analysis may identify relationships between housing prices and economic conditions, but it cannot prove that one factor directly causes another. Other factors, such as housing supply and population changes, may also affect housing prices.
- **Data access:** We will review the sources and usage restrictions for each dataset to make sure we can properly access, use, and share the data.

## Gaps
- **Dataset Availability:** We still need to confirm that all datasets contain information for the states and years we plan to analyze (2015–2024).
- **Data Consistency:** We need to determine how to handle differences in data formatting, reporting periods, and inflation adjustments across the datasets.
- **Data Integration:** We need to confirm that the datasets have matching state and year information so they can be combined correctly.
- **Analysis Methods:** We still need to decide which statistical methods and visualizations will be most useful for answering our research questions.
- **Team Responsibilities:** We need to finalize specific responsibilities for each team member and determine which tools we will use for data cleaning and integration.

