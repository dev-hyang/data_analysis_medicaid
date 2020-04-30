# Project Outline for Demographic Data Analysis of Physician Fee Schedule on Insurance
## Objective
Our vision is to set up anchor prices for physicians or patients’ reference on different medical procedure services around the demographic area in the United States. First, we have collected all data sources to compute the state level anchor procedure service prices for 51 states in the United States. Later on, we have discussed two special cases on state Indiana and Connecticut on the county level anchor prices.
In order to compute the anchor prices, we will need below data files: 
All Population data from United States Census Bureau
As the latest demographic data is only released for year 2018. This sets timeline for our main targeting data files collected from Medicaid, Medicare, as well as other demographic files.
Data is downloaded here.

## Input Data
- 2018 Census Data
- 2018 state level Medicaid Enrollment data
- 2018 state-county level Medicare Enrollment data
- 2018 Indiana/New York Medicaid Enrollment data
- 2018 Connecticut Township Medicaid Enrollment data & Town-County mapping dictionary
- 2018 Connecticut/Indiana/New York Physician Fee Schedule data

## EDA Techniques and Data Cleansing
### EDA techniques (Take the census data as an example)
Data Structure: <Tabular> CSV file, make “STNAME”, “CTNAME”, “YEAR”, “AGRP” as primary/foreign keys, “STNAME” and “CTNAME” are nominal data type, while others are quantitative data type.
Granularity: Each row stands for a population statistics record in a county from a state within year 2007-2018. We can use Groupby + sum to get the total population of each state.
Scope: all states and counties statistics within year 2007-2018 in U.S.
Temporality: Time dependes on “YEAR” column which represents as 0-11 integers, where 0 represents 2007, 11 represents 2018. It’s too huge. We just select data for year 2018 in the end.
Faithfulness: credited from United States Census Bureau

### Data Cleansing 
The Data we populated could be incomplete, noisy, dirty and invalid. Based on different data files and situations, we would use different data cleansing methods to correct the data frame.
- Noise data
Invalid data: focus on the time span till 2018. For example, we will count price data which takes effect after Jan-1-2019 as invalid.
Non statistics data: such as text messages/comments in the data file. Some of the files download has lots of comments and notes in the tail. We just ignore those rows.

- Missing data
Blanks: usually we will ignore/filter out rows with blank value, such as “UNKNOWN” rows in Medicare enrollment data.
“*”, “nan”, “N/A”: if it’s population or enrollment data, usually we replace this data as 0. We will also check the context, such as in the Medicare enrollment data file, the totals are constructed by “FFS Beneficiaries” – Fee For Service Program and “MA Beneficiaries” – Medicare Advantage Program. Then we fill the “*” in the total Medicare enrollment with “FFS Beneficiaries”.

- Merge data
As our goal is to compute the demographic anchor PFS prices, we need to combine all population data file, Medicaid enrollment data file, Medicare enrollment data file, Medicaid PFS file, and Medicare PFS export report. 

## Output
To compute the anchor procedure service price, we will take use the rates of Medicaid, Medicare, Private insurance enrollment rate in per state/county, and their physician fee schedule based on the HCPCT code/Procedure code.
The Process is below:
First, compute % of "STATE_MEDICAID_PRCENT" = Medicaid enrollment / state-level population, % of "STATE_MEDICARE_PRCENT" = # of Medicare beneficiaries / state-level population. 
Suppose % of private provider customers = 1 - % of "STATE_MEDICAID_PRCENT" - % of "STATE_MEDICARE_PRCENT
Second, compute $ Anchored Physician Fee Amount for per procedure code = % Medicaid Rate * Medicaid_fee + % Medicare Rate * Medicare_fee + %Private Insurance Rate* Private_Insurance_fee

In the /output folder, you could find the resulted fee tables.


## Conlusion
Through this project, we can get that different counties could have their own customized physician fee schedule based on demographic factor, poverty rate (Medicaid enrollment), aging factor (Medicare enrollment),  etc. The county-level fee shcedule could even vary from dollars to thousands of dollars. We conclude that the state-level weighted fee schedule could also be used to guide some newly Medicaid/Medicare expanded states as they have little or no information about Medicaid/Medicare information.


## Challenge and future
- 1, How to find valid, correct and uniformed formatted data is the key? But how could you get such data as each state has its own database or API? 
- 2, How to combine these data together with other statistics data, like form CMS, Census bureau. Both data format and content is different, we need to figure out the relationship (primary+foreign key) in each data file.
- 3, How to collect the actual expenditure of the Medicaid, Medicare, and Private insurance in the real patient-visit cases? As our data is based on the CMS or each state’s release fee schedule, what is the real cost is unknown during the visit? These could be more valuable if possible.
