### Benjamin Liang — Update for Milestone 3

I did the initial exploratory analysis of the 30-year fixed-rate mortgage dataset ([`MORTGAGE30US.csv`](MORTGAGE30US.csv)), sourced from Federal Reserve Economic Data (FRED). This dataset tracks the weekly national average commitment rate for a 30-year fixed-rate mortgage across the United States and serves as our core macroeconomic financing indicator.

To document and reproduce this workflow, I created and uploaded [`Course Project - Mortgage.ipynb`](Course%20Project%20-%20Mortgage.ipynb), along with the ORIGINAL dataset to the repository. The original dataset, which was downloaded from and already filtered by 2015-2024 through FRED, didn't require me to manually portion the data to obtain what we wanted.

In the notebook, I manipulated the dataset to now include the average mortgage rate for each month, formatted into "Mon" + "Year". I'm hoping that by doing this, and still having the individual timestamped mortgage rate records, we can find some interesting patterns or clues as to why the rates shifted over time.

Because FRED provides standardized time-series exports, the dataset was clean and straightforward to manipulate—audits confirmed zero missing values, duplicate timestamps, or malformed entries across our target window, eliminating the need for any additional cleaning. I encountered no technical blockers during data collection or initial processing. 

I think moving forward, our next steps would be to find common features among our separate datasets and to link and join them so that we can perform further financial analysis on the entire thing. I'll most likely make sure the datasets are integrated properly so that the combined data is usable and accessible. I might have to do additional formatting on my mortgage dataset to make sure the variables are consistent.

### Amanda Dorado — Update for Milestone 3

For this milestone, I was responsible for collecting and cleaning the median household income dataset from the U.S. Census Bureau's American Community Survey (ACS). This dataset provides state-level median household income estimates and will help us examine how household income relates to housing prices and other economic indicators across the United States.

To collect the data, I used Python and the Census API to retrieve household income estimates for 2015–2019 and 2021–2024. I combined the yearly datasets using pandas, resulting in 468 records across 52 geographic areas. I uploaded the original dataset ([`census_income_raw.csv`](amandorado/census_income_raw.csv)), cleaned dataset ([`census_income_cleaned.csv`](amandorado/census_income_cleaned.csv)), and Python notebook ([`census_income_collection.ipynb`](amandorado/census_income_collection.ipynb)) to our shared GitHub repository.

In my notebook, I conducted initial data quality assessments to identify missing values, duplicate state-year combinations, and inconsistent data types. The dataset initially contained no standard missing values or duplicate records, but the income values were stored as strings. To address this, I converted the income values to numeric format, standardized column names, removed unnecessary whitespace from state names, and formatted state FIPS codes consistently. After cleaning, the dataset contained no missing income values or duplicate state-year combinations.

One challenge I encountered was the unavailability of standard 2020 ACS 1-year estimates due to COVID-19-related disruptions. Moving forward, I plan to coordinate with my teammates to determine how to address this missing year and ensure that the household income dataset can be properly integrated with the other datasets. I may also need to make additional formatting adjustments to ensure consistency across our datasets.