# Road Casualties Analysis

<img width="900" height="500" alt="Screenshot 2026-08-14 at 14 24 20" src="https://github.com/user-attachments/assets/80b73c1b-66f4-4a9f-9262-5711b591cad5" />

## Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Key Questions](#key-questions)
- [Tools](#tools)
- [Process](#process)
  - [Data Cleaning](#data-cleaning)
  - [Data Modelling](#data-modelling)
  - [DAX Measures](#dax-measures)
  - [Visualisation](#visualisation)
- [Key Findings and Recommendations](#key-findings-and-recommendations)
- [Future Improvements](#future-improvements)

## Overview
An analysis of 20222 UK traffic accident data to identify the key predictors of road casualties, surfacing insights that can support road safety improvements.

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

## Key Findings and Recommendations 
### 1. **How do casualty trends in 2022 compare to 2021?** </br>
 Total casualties declined by 11.9% year-on-year to 196K, alongside an 11.7% drop in accidents to 144K. Fatal casualties decreased the most, down 33.3% to 3K, while serious casualties fell 16.2% and slight casualties fell 10.6%. This suggests an improvement in severity outcomes as well as accident frequency.

   Further investigation into whether an external factor resulted in this improvement could help identify strategies worth enforcing in future years.

### 2. **Which vehicle types are most associated with fatal or serious casualties?** </br>
   Cars accounted for the majority of casualties (155,804) and fatal casualties (2,000), far ahead of vans (15,905) and motorcycles (15,579). However, as cars are the most common vehicle on UK roads, this is less likely to reflect a higher inherent risk and more their volume of usage. Furthermore, despite being much less common than vans, motorcycles recorded a similar casualty count, suggesting a disproportionately higher risk per rider.

   Motorcyclist safety initiatives, such as improved rider training and dedicated motorcycle lanes on high-risk junctions and roads, could help reduce this risk.

### 3. **How do road conditions affect casualty outcomes?** </br>
   Dry conditions accounted for the majority of casualties (132,000) and fatal casualties (2,000), with wet or damp conditions the second largest contributor (50,000 casualties and 754 fatal casualties). This may be explained by behavioural and exposure factors; for instance, drivers often slow down in wet conditions, and there are likely to be more people on UK roads in drier conditions. However, the proportion of fatal casualties was almost identical across both conditions (1.5%), suggesting that although wet weather results in fewer accidents overall, it does not increase the likelihood of a casualty being fatal. Road surface conditions also show a seasonal pattern, with snow and ice contributing to more casualties during winter months, and dry-condition casualties peaking mid-year.

### 4. **How do light conditions affect casualty severity?** </br>
   The majority of casualties occur in daylight (73.8%), compared to 26.2% in darkness. As with road surface conditions, this may be explained by exposure: more people travel during daylight hours. However, the fatality rate of casualties is higher in darkness (1.96%) compared to in daylight (1.34%), which may be influenced by reduced visibility and higher speeds due to roads being quieter.

   Improved street lighting on high-risk rural roads and increased use of reflective signage could help reduce the severity of road accidents during darkness.
   
### 5. **Which road type shows the highest concentration of casualties?** </br>
   Single carriageways had the highest number of casualties in 2022 (145,000), far exceeding dual carriageways, the second highest at 32,000. This pattern is also reflected in severity, with single carriageways responsible for 67% of fatal casualties and 78% of serious casualties. This may be as a result of factors such as overtaking manoeuvres, shared use with other road users like cyclists, and blind spots such as bends or hidden dips.

   Road infrastructure improvements, such as crash barriers or additional signage, could help reduce the concentration of risk on single carriageways. 

## Future Improvements
- Incorporate traffic volume data.
- Expand the dataset to include additional years for longer-term trend analysis.
- Explore demographic factors (age, road user type, vehicle make) to identify correlations with casualty rates.
- Add predictive modelling to identify high-risk locations in advance.

