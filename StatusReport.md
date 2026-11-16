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

**Role:** I am responsible for collecting, assessing, and cleaning the state unemployment rate dataset from Federal Reserve Economic Data (FRED), which redistributes the Bureau of Labor Statistics' Local Area Unemployment Statistics. I also co-lead dataset integration with Ben.

#### Task updates

**Data collection: done.** My first download was the national series `UNRATE` ([`UNRATE.csv`](Unemployment2015-2024/UNRATE.csv), cleaned in [`Unemployemnt_cleaning.ipynb`](Unemployment2015-2024/Unemployemnt_cleaning.ipynb)). Two problems ruled it out as our main unemployment dataset. First, it is a single national rate, but Research Question 3 asks how unemployment relates to home values *across states*. Second, the file stopped at January 2024. I replaced it with FRED's monthly, seasonally adjusted state series, which are named by postal code plus `UR` (for example `ILUR` and `CAUR`). I wrote a Python/pandas acquisition step in [`State_cleaning_unemplyment.ipynb`](Unemployment2015-2024/State_cleaning_unemplyment.ipynb) that builds each series ID and downloads it from FRED's CSV endpoint (`https://fred.stlouisfed.org/graph/fredgraph.csv?id={series_id}`) for January 2015 – December 2024. `UNRATE` will stay in the repository as a national benchmark only.

**Data cleaning: done.** I parsed dates into datetime objects, pulled out a `year` column, and converted the rates to numbers with `pd.to_numeric(..., errors="coerce")`. I then mapped every series to three standard identifiers: a 2-character zero-padded FIPS code stored as text (`state_fips`, e.g. `"06"`), the postal abbreviation (`state_abbr`), and the full name (`state_name`). Finally, I averaged the monthly rates by state and year, rounded to 2 decimals, so they match the annual Census income data. The outputs are:

- [`state_unemployment_monthly_2015_2024.csv`](Unemployment2015-2024/Unemployment2015-2024/state_unemployment_monthly_2015_2024.csv): 6,120 rows (51 geographies × 120 months)
- [`state_unemployment_annual_2015_2024.csv`](Unemployment2015-2024/Unemployment2015-2024/state_unemployment_annual_2015_2024.csv): 510 rows (51 geographies × 10 years)

**Pre-integration quality assessment: done.**

| Dimension | Result |
|---|---|
| Completeness | All 50 states + D.C. have all 120 months; there are no missing values after converting to numbers and no duplicate state-month or state-year keys. |
| Timeliness | Every observation falls inside the 2015–2024 study window, including all of 2024, which the old `UNRATE` file lacked. |
| Consistency | `state_fips` is always 2 characters (`"01"`–`"56"`), and state names match the spellings in the Zillow and Census files. |
| Accuracy | Values come straight from BLS through FRED. Rates range from 1.7% to 30.5%. The maximum is Nevada in April 2020, a real COVID-19 shock, so I kept it and will flag it in the analysis instead of removing it. |

**Integration prep: in progress (with Ben).** I tested the join keys against my teammates' cleaned files. Joining to Zillow on name + year matches all 500 Zillow rows. Joining to Census on FIPS + year matches 459 of 468 Census rows. The 9 unmatched Census rows are Puerto Rico, which has no state unemployment series in our data. There are also two coverage gaps. Zillow has no D.C. rows, and Census has no 2020 data (the ACS 1-year estimates were not released). That means the three-way join will produce about 450 state-year rows (50 states × 9 years). We need to decide as a team whether to accept that or fill 2020 another way.

#### Changes to the project plan

The plan listed the unemployment join key as "State + year after annual aggregation," while Census used "State FIPS code + year." I changed the unemployment schema to carry `state_fips`, `state_abbr`, and `state_name`, and I included D.C. (FIPS `"11"`) to match the Census output. This lets every state-level dataset join on a code instead of on name spellings. I also changed the unemployment source from the national series to the state series, as described above.

#### Challenges and how I resolved them

1. **Too many series to download by hand.** Searching FRED for state unemployment returned 9,400+ mixed series: metro areas, U-1 to U-6 measures, and non-seasonally adjusted annual series. Rather than download 51 CSVs by hand, I generated the series IDs from the `{STATE}UR` naming pattern and fetched them in code. This also gives us a reproducible acquisition step for the final workflow.
2. **FIPS codes losing their leading zero.** When `pandas.read_csv()` reloads `"06"`, it reads it as the integer `6`, and joins on text keys break. I format the codes with `.zfill(2)` when saving and will load them with `dtype={"state_fips": str}` in the integration script.
3. **Upcoming:** the 2020 Census gap and the missing D.C. and Puerto Rico rows described above.

#### Next steps

| Task | Status | Target date |
|---|---|---|
| Collect state unemployment data | Done | Nov 16 |
| Clean the data and aggregate to annual averages | Done | Nov 16 |
| Add SHA-256 checksums to the acquisition step | Not started | Nov 20 |
| Split the notebook into separate `acquire` and `clean` scripts for the workflow | Not started | Nov 22 |
| Join Zillow, Census, unemployment, and mortgage data, then run post-integration quality checks | Not started | Nov 25 (with Ben) |
