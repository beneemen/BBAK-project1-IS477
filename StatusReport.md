### Benjamin Liang — Update for Milestone 3

I did the initial exploratory analysis of the 30-year fixed-rate mortgage dataset ([`MORTGAGE30US.csv`](MORTGAGE30US.csv)), sourced from Federal Reserve Economic Data (FRED). This dataset tracks the weekly national average commitment rate for a 30-year fixed-rate mortgage across the United States and serves as our core macroeconomic financing indicator.

To document and reproduce this workflow, I created and uploaded [`Course Project - Mortgage.ipynb`](Course%20Project%20-%20Mortgage.ipynb), along with the ORIGINAL dataset to the repository. The original dataset, which was downloaded from and already filtered by 2015-2024 through FRED, didn't require me to manually portion the data to obtain what we wanted.

In the notebook, I manipulated the dataset to now include the average mortgage rate for each month, formatted into "Mon" + "Year". I'm hoping that by doing this, and still having the individual timestamped mortgage rate records, we can find some interesting patterns or clues as to why the rates shifted over time.

Because FRED provides standardized time-series exports, the dataset was clean and straightforward to manipulate—audits confirmed zero missing values, duplicate timestamps, or malformed entries across our target window, eliminating the need for any additional cleaning. I encountered no technical blockers during data collection or initial processing. 

I think moving forward, our next steps would be to find common features among our separate datasets and to link and join them so that we can perform further financial analysis on the entire thing. I'll most likely make sure the datasets are integrated properly so that the combined data is usable and accessible. I might have to do additional formatting on my mortgage dataset to make sure the variables are consistent.
