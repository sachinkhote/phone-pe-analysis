# PhonePe Transaction Data Analysis

## Project Overview
This project performs an end-to-end data analysis of PhonePe transaction data across Indian states and districts from Q1 2018 to Q2 2021. The analysis is done using Python and Pandas in a Jupyter Notebook environment. It covers data loading, exploratory data analysis, data quality checks, merging datasets, visualizations and final insights.

---

## Dataset
**File:** `phonepe-pulse_raw-data_q12018-to-q22021-v0-1-5-1720351752.xlsx`

The Excel file contains 5 sheets:

### 1. State_Txn_Users
Contains transaction and user data at the state level.
| Column | Description |
|--------|-------------|
| State | Name of the state |
| Year | Year of the data |
| Quarter | Quarter of the year |
| Transactions | Number of transactions |
| Amount (INR) | Total transaction amount in INR |
| ATV (INR) | Average transaction value in INR |
| Registered Users | Number of registered users |
| App Opens | Number of times app was opened |

### 2. State_TxnSplit
Contains breakdown of transaction types at the state level.
| Column | Description |
|--------|-------------|
| State | Name of the state |
| Year | Year of the data |
| Quarter | Quarter of the year |
| Transaction Type | Type of transaction (Peer-to-peer, Merchant, Recharge, etc.) |
| Transactions | Number of transactions |
| Amount (INR) | Total transaction amount in INR |
| ATV (INR) | Average transaction value in INR |

### 3. State_DeviceData
Contains device brand information of registered users at the state level.
| Column | Description |
|--------|-------------|
| State | Name of the state |
| Year | Year of the data |
| Quarter | Quarter of the year |
| Brand | Device brand name |
| Registered Users | Number of users using that brand |
| Percentage | Percentage of users using that brand |

### 4. District_Txn_Users
Contains transaction and user data at the district level.
| Column | Description |
|--------|-------------|
| State | Name of the state |
| Year | Year of the data |
| Quarter | Quarter of the year |
| District | Name of the district |
| Code | District code |
| Transactions | Number of transactions |
| Amount (INR) | Total transaction amount in INR |
| ATV (INR) | Average transaction value in INR |
| Registered Users | Number of registered users |
| App Opens | Number of times app was opened |

### 5. District_Demographics
Contains demographic details for each district.
| Column | Description |
|--------|-------------|
| State | Name of the state |
| District | Name of the district |
| Headquarters | District headquarters |
| Population | Population of the district |
| Area (sq km) | Area in square kilometers |
| Density | Population density |
| Code | District code |
| Alternate Name | Alternate name of the district |

---

## Tasks Completed

### Task 1 - Data Loading and Understanding
- Loaded all 5 datasets from the Excel file using `pd.read_excel()` with `sheet_name` parameter
- Displayed first, last and middle rows of each dataset
- Calculated summary statistics (mean, median, std, min, max) for all numerical columns
- Identified data types of each column
- Checked for missing values and calculated their percentage
- Found that `Amount (INR)` in State data has 0.19% missing values and `Code` column in District data has 0.27% missing values
- Calculated total unique states (36) and districts (732)
- Identified Uttar Pradesh as the state with most districts (75)

### Task 2 - Exploratory Data Analysis
- Calculated total transactions and amount per state across all years
- Identified top 5 states (Karnataka, Maharashtra, Telangana, Andhra Pradesh, Rajasthan) and bottom 5 states (Meghalaya, Mizoram, Ladakh, Andaman & Nicobar, Lakshadweep) by transaction volume
- Found that Peer-to-peer payments is the most common transaction type across almost all states and quarters
- Identified Xiaomi and Samsung as the dominant device brands across most states
- Found Mumbai Suburban as the most populated district in Maharashtra
- Calculated average ATV per state — Ladakh has highest ATV, West Bengal has lowest
- Analyzed app opens trend over time — strong growth from 2019, dip in 2020 Q2 due to COVID, strong recovery after
- Created bar chart of transaction types for latest quarter (2021 Q2) — Peer-to-peer leads followed by Merchant payments
- Exported 732 unique district to district code mappings as a CSV file

### Task 3 - Data Quality Checks
- Summed district level transactions, amount and registered users by state, year and quarter
- Compared with state level data
- Found zero real discrepancies — district level data perfectly matches state level data
- Note: Some rows showed -0 due to floating point precision, handled using `.abs() > 1` filter

### Task 4 - Data Merging and Advanced Analysis
- Merged state user data with district demographics to calculate users to population ratio
- Delhi has the highest ratio (0.66) — 2 out of 3 people are registered on PhonePe
- Meghalaya and Mizoram have the lowest ratio (0.06-0.08) — huge untapped market
- Calculated correlation between population density and transaction volume — 0.42 (moderate positive)
- Found Telangana has highest average transaction amount per user (₹56,151) and Lakshadweep has lowest (₹5,593)
- Analyzed device brand usage ratio — Xiaomi leads in Maharashtra at 26%, followed by Samsung at 22%

### Task 5 - Data Visualization
- Created dual axis line plot showing transactions and amount over time for Maharashtra — both follow same growth pattern
- Created pie chart of transaction types for Maharashtra 2021 Q2 — Merchant payments (43.1%) slightly leads over Peer-to-peer (39.8%)
- Created bar chart of population density across Maharashtra districts — Mumbai Suburban and Mumbai City are far ahead with 20,000+ density

### Task 6 - Insights and Conclusions
- Analyzed yearly transaction trends — 8x growth from 2018 to 2020
- Summarized correlation findings between demographics and transaction data
- Listed key findings and actionable recommendations

---

## Key Trends and Observations

### Transaction Growth
- PhonePe transactions grew 8x from 2018 to 2020
- 2018 was the starting phase with very low adoption
- 2019 saw rapid growth as UPI gained popularity across India
- 2020 saw the highest transactions — COVID-19 lockdown forced people to adopt digital payments
- 2021 data is only till Q2 but the trajectory shows continued strong growth

### Transaction Types
- Peer-to-peer payments dominate nationally — people primarily use PhonePe to send money to friends and family
- Maharashtra is an exception — Merchant payments (43.1%) slightly leads over Peer-to-peer (39.8%), showing a more mature digital payment ecosystem
- Financial Services and Others are nearly negligible — still a very niche category

### Geographic Patterns
- Southern states (Karnataka, Telangana, Andhra Pradesh) lead in both volume and amount
- Karnataka leads in transaction count but Telangana leads in total amount — Telangana users make fewer but higher value transactions
- North-eastern states are significantly under-penetrated

### User Penetration
- Delhi has highest penetration at 66% — most digitally advanced state
- Telangana, Chandigarh and Karnataka also show strong penetration above 40%
- Mizoram, Meghalaya and Lakshadweep are below 10% — massive growth opportunity

### Device Ecosystem
- Xiaomi and Samsung dominate across most states — reflecting India's mid-range Android market
- Vivo and Oppo together hold significant share in many states
- Apple (iPhone) users are a very small minority on PhonePe despite being a premium brand

### App Engagement
- App opens grew consistently but dipped slightly in 2020 Q2 during COVID lockdown
- App opens are growing faster than transactions — users browse and check balances more than they transact
- Maharashtra crossed 1.2 billion app opens in 2021 Q2

### Population and Transactions
- Moderate positive correlation (0.42) between population density and transaction volume
- Denser districts tend to transact more but not always — Mumbai and Bengaluru are clear outliers
- Some low density districts also show decent transaction volumes due to tourist and pilgrim activity

---

## Key Findings

1. PhonePe saw exponential growth from 2018 to 2021 driven by UPI adoption and COVID
2. Peer-to-peer payments is the #1 use case nationally
3. Southern and western states are the most digitally active on PhonePe
4. Delhi has the highest user to population ratio in India at 66%
5. High ATV states (Ladakh, Andaman, Mizoram) do fewer but bigger transactions
6. Low ATV states (Karnataka, Maharashtra, West Bengal) do millions of small daily transactions
7. Xiaomi is the #1 device brand for PhonePe users across most states
8. District level data perfectly matches state level data — clean and reliable dataset
9. COVID-19 was the biggest accelerator of digital payment adoption in India
10. North-eastern states remain the biggest untapped opportunity for PhonePe

---

Add this section after **Key Findings** and before **Conclusions**:

---

## Problems Faced and How They Were Solved

### 1. Overcounting Districts with value_counts()
**Problem:** When counting districts per state using `value_counts()`, Uttar Pradesh showed 1050 districts which is impossible. The real number is 75.
**Cause:** The dataset has data for multiple quarters, so each district appears 14 times (once per quarter). `value_counts()` was counting rows not unique districts.
**Solution:** Used `groupby("State")["District"].nunique()` which counts only unique district names per state.

### 2. Amount Column Showing in Scientific Notation
**Problem:** Amount values were displaying as `3.18e+12` which is hard to read and understand.
**Solution:** Used `pd.options.display.float_format = '{:,.0f}'.format` to display full numbers with commas.

### 3. Ratio Values Showing as 0
**Problem:** User to population ratio was showing as 0 for almost all states even though the values were correct.
**Cause:** Python was rounding very small decimal values like 0.3530 to 0 during display.
**Solution:** Used `pd.options.display.float_format = '{:.4f}'.format` to show 4 decimal places.

### 4. False Discrepancies in Data Quality Check
**Problem:** Data quality check showed 491 discrepancies between district and state level data. But all differences were showing as 0 or -0.
**Cause:** Floating point precision issue in Python where tiny decimal differences like -0.000001 were being stored as -0.
**Solution:** Used `.abs() > 1` filter to ignore differences smaller than 1, which revealed zero real discrepancies.

### 5. Self Overwrite Bug in Task 5.1
**Problem:** Got a KeyError when trying to plot because the Period column was missing and state_ts had lost all its columns.
**Cause:** Wrote `state_ts = state_ts["Year"].astype(str) + "-Q" + ...` which replaced the entire dataframe with just a single column series.
**Solution:** Used `state_ts["Period"] = ...` to add Period as a new column instead of overwriting the whole dataframe.

### 6. X-axis Labels Not Rotating in Twin Axis Chart
**Problem:** `plt.xticks(rotation=45)` did not rotate the x-axis labels in the dual axis line chart (Task 5.1).
**Cause:** When using `twinx()`, there are two axes objects and `plt.xticks()` does not always apply correctly to both.
**Solution:** Used `ax1.set_xticks()` and `ax1.set_xticklabels()` directly on the axis object instead of using `plt.xticks()`.

### 7. Case Sensitivity Error
**Problem:** Column name `"transactions"` was throwing a KeyError.
**Cause:** Python column names are case sensitive. The actual column name was `"Transactions"` with a capital T.
**Solution:** Always match column names exactly as they appear in `df.columns`.

---

## Conclusions
PhonePe has established itself as a dominant UPI payment platform across India. The data clearly shows that urban, densely populated and economically active states have much higher adoption. However the growth trajectory from 2018 to 2021 shows that digital payment adoption is spreading to smaller states and districts as well. COVID-19 acted as a major inflection point that permanently shifted consumer behavior towards digital payments. The platform has strong fundamentals with clean consistent data across state and district levels.

---

## Future Scope
1. Extend analysis beyond 2021 to see post-COVID trends
2. Add district level visualization using maps (choropleth maps using folium or geopandas)
3. Build a forecasting model to predict future transaction volumes using time series analysis
4. Analyze merchant category wise spending patterns if data becomes available
5. Compare PhonePe market share with other UPI apps like Google Pay and Paytm
6. Perform cluster analysis to group similar states based on transaction behavior
7. Analyze seasonal patterns more deeply — monthly instead of quarterly breakdown

---

## Tools and Libraries Used
- Python 3
- Pandas — data loading, cleaning, grouping and analysis
- Matplotlib — data visualization and charts
- Jupyter Notebook — interactive coding environment

---

## Output Files
- `district_code_mapping.csv` — Unique mapping of 732 districts to their district codes
- `phonepe.ipynb` — Complete Jupyter Notebook with all analysis and charts