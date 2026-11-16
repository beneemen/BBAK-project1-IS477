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

### BJ Mensah — Update for Milestone 3

For this milestone, I was responsible for collecting and cleaning the state unemployment rate data from Federal Reserve Economic Data (FRED), which comes from the Bureau of Labor Statistics. I am also working with Ben on integrating our datasets.

I first downloaded the national unemployment rate ([`UNRATE.csv`](Unemployment2015-2024/UNRATE.csv)). I then realized that a single national rate couldn't answer our research question about differences between states. Searching FRED for state unemployment returned over 9,400 mixed series, so instead of downloading 51 files by hand, I wrote Python code in [`State_cleaning_unemplyment.ipynb`](Unemployment2015-2024/State_cleaning_unemplyment.ipynb). The code automatically pulls the monthly, seasonally adjusted unemployment rate for all 50 states plus Washington, D.C. from 2015 to 2024.

In the notebook, I converted the dates to a proper date format, made sure all unemployment rates were numeric, and added each state's name, abbreviation, and FIPS code so the data matches Amanda's Census dataset. I then averaged the monthly rates into yearly rates so they line up with the annual income data. I saved both versions: [`state_unemployment_monthly_2015_2024.csv`](Unemployment2015-2024/Unemployment2015-2024/state_unemployment_monthly_2015_2024.csv) (6,120 rows) and [`state_unemployment_annual_2015_2024.csv`](Unemployment2015-2024/Unemployment2015-2024/state_unemployment_annual_2015_2024.csv) (510 rows). After cleaning, the data had no missing values or duplicate records. The highest rate was Nevada in April 2020 (30.5%), which reflects COVID-19, so I kept it.

One challenge I ran into was that FIPS codes like "06" for California lose their leading zero when loaded with pandas, which breaks the join with the Census data. I fixed this by saving FIPS codes as two-character text and loading them as strings.

Moving forward, I will work with Ben to combine the housing, income, unemployment, and mortgage datasets by state and year. We also need to decide as a team how to handle 2020, which is missing from the Census data. I will also add SHA-256 checksums and split my notebook into separate scripts for our final workflow.

### Krissy Ho — Update for Milestone 3

For this milestone, I was responsible for collecting and cleaning the Zillow Home Value Index (ZHVI) dataset. This dataset provides housing values across different states in the U.S. and will help us look at how housing prices relate to factors like household income, unemployment rates, and mortgage interest rates from 2015 to 2024.

I started by downloading the Zillow Home Value Index (ZHVI) dataset from Zillow Research, which included monthly home values dating back to 2000 and several columns that weren't needed for our project. Since we're planning to combine our datasets by state and year, I needed to narrow the data down to 2015–2024 and calculate the annual average home values for each state.

I used Python and pandas in a Jupyter notebook (zillow_cleaning.ipynb) to clean and organize the Zillow dataset. I removed unnecessary columns, filtered the data to 2015–2024, and calculated the annual average home values for each state. I also checked for missing values and duplicate records to make sure the data was accurate. The final cleaned dataset (zillow_home_values_cleaned.csv) contains 500 records across all 50 states from 2015 to 2024, with no missing values or duplicate state-year records.

One challenge I ran into was that the original Zillow dataset had a separate column for every month, which made it harder to work with and combine with our other datasets. To fix this, I reorganized the data so that each row represented one state and year instead. I also had to double-check that I was averaging the correct months for each year and that all the states were accounted for.

Moving forward, I'll work with my teammates to make sure the Zillow data can be properly combined with the income, unemployment, and mortgage datasets. We may need to make a few more formatting adjustments so that everything matches up correctly. Once the datasets are integrated, I also plan to help analyze housing price trends and see how they relate to changes in economic conditions over time.
