# Road Casualties Analysis

<img width="900" height="500" alt="Screenshot 2026-08-11 at 18 32 39" src="https://github.com/user-attachments/assets/656ed85a-4efa-4076-aac1-87a233c1c311" />

## Overview
An analysis of UK traffic accident data 2022 to identify the key predictors of road casualties, surfacing insights that can support road safety improvements.

## Dataset
UK road accident data spanning 2021–2022, sourced from [Kaggle](https://www.kaggle.com/datasets/atharvasoundankar/road-accidents-dataset/code).

## Tools

- Power Query for data cleaning.
- DAX for custom measures and KPI calculations.
- Data modelling and interactive dashboard design in Power BI.

## Key Questions
1. How do casualty trends in 2022 compare to 2021?
2. Which vehicle types are most associated with fatal or serious casualties?
3. How do road conditions affect casualty outcomes?
4. How do light conditions affect casualty severity?
5. Which road type shows the highest concentration of casualties?

## Process
### Data Cleaning
The process of data cleaning and transformation in Power Query involved:
- Checking data consistency, e.g. converting the `Accident_Date` column to the correct Date format (UK locale).
- Removing redundant columns, such as `Accident_Index`.
- Grouping columns with low-frequency values, e.g. combining `Van / Goods 3.5 tonnes mgw or under` into a broader `Van` category within `Vehicle_Type`

### Data Modelling
- Created a Calendar table using `CALENDAR(MIN('Road Accident Data'[Accident Date]), MAX('Road Accident Data'[Accident Date]))` to cover the full date range.
- Marked the Calendar table as a Date Table to enable accurate time intelligence functions.
- Built a star schema, connecting the fact table (`Road Accident Data`) to the `Calendar` date table via a one-to-many relationship.

### DAX Measures
Key measures developed include:
- **Time intelligence**: year-to-date and year-over-year comparisons using `TOTALYTD` and `SAMEPERIODLASTYEAR`.
- **Filtering**: used `KEEPFILTERS` within `CALCULATE` to preserve existing month-level filters when applying year-based logic. This measure was used to create the 2021-2022 monthly trend chart.
- **Custom KPIs**: casualty count for the current year (2022) and prior year (2021), as well as casualty count broken down by severity (`Fatal`, `Serious`, `Slight`), and casualty change (current vs. prior year).

### Visualisation
Designed an interactive dashboard including:
- KPI cards showing current year (2022) vs. prior year (2021) casualty figures, with year-on-year percentage change, broken down by severity.
- A clustered bar chart comparing monthly casualties between 2021 and 2022.
- A table displaying casualties by vehicle type.
- An interactive map plotting accident locations.
- Slicers for road surface conditions and weather conditions, using dropdown style.

## Key Findings
1. **How do casualty trends in 2022 compare to 2021?** </br>
 Total casualties declined by 11.9% year-on-year to 196K, alongside an 11.7% drop in accidents to 144K. Fatal casualties decreased the most, down 33.3% to 3K, while serious casualties fell 16.2% and slight casualties fell 10.6%. This suggests an improvement in severity outcomes as well as accident frequency.

2. **Which vehicle types are most associated with fatal or serious casualties?** </br>
   Cars accounted for the majority of casualties (155,804) and fatal casualties (2,000), far ahead of vans (15,905) and motorcycles (15,579). However, as cars are the most common vehicle on UK roads, this is less likely to reflect a higher inherent risk and more their volume of usage. Furthermore, despite being much less common than vans, motorcycles recorded a similar casualty count, suggesting a disproportionately higher risk per rider.

3. **How do road conditions affect casualty outcomes?**
   Dry conditions accounted for the majority of casualties (132,000) and fatal casualties (2,000), with wet or damp conditions the second largest contributor (50,000 casualties and 754 fatal casualties). This may be explained by behavioural and exposure factors; for instance, drivers often slow down in wet conditions, and there are likely to be more people on UK roads in drier conditions. However, the proportion of fatal casualties was almost identical across both conditions (1.5%), suggesting that although wet weather results in fewer accidents overall, it does not increase the likelihood of a casualty being fatal. Road surface conditions also show a seasonal pattern, with snow and ice contributing to more casualties during winter months, and dry-condition casualties peaking mid-year.

4. **How do light conditions affect casualty severity?**
   The majority of casualties occur in daylight (73.8%), compared to 26.2% in darkness. As with road surface conditions, this may be explained by exposure
