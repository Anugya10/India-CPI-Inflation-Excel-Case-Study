# India CPI Inflation Analysis (2013 - May 2023)

An end-to-end Excel data analytics case study on India's Consumer Price Index (CPI). Acting as an analyst at the National Statistical Office (NSO), I cleaned monthly CPI data, built a formula-driven calculation layer, and answered five questions on category contribution, inflation trends, food prices, the COVID-19 impact, and the influence of crude oil prices.

## Project overview

**Objective:** Use CPI data to find key inflation trends and explain what drove them.

**Background:** CPI measures the average change in prices of a fixed basket of goods and services against a base year (2012 = 100). A CPI of 110 means prices are 10% higher than in the base year. Because CPI is an index, index values are compared using percentage changes and are never summed across months.

**Questions answered:**

| # | Question |
|---|---|
| Q1 | Which broader category contributes most to the CPI basket (latest month)? |
| Q2 | What is the year-on-year inflation trend from 2017, and which year was highest? |
| Q3 | How did food inflation behave in the 12 months ending May 2023, and which food category contributed most? |
| Q4 | How did the COVID-19 lockdown (March 2020) affect inflation? |
| Q5 | How strongly did imported crude oil price changes influence category inflation (2021 to 2023)? |

## Dataset

- **Source:** CPI index data published by the Government of India 
- **Period:** January 2013 to May 2023 (monthly)
- **Sectors:** Rural (CPI-R), Urban (CPI-U) and Rural+Urban (combined)
- **Columns:** Sector, Year, Month and about 27 category indices, including the food sub-categories (cereals, meat and fish, egg, milk, oils and fats, fruits, vegetables, pulses, sugar, spices, beverages, prepared meals), the broader divisions (Food and beverages, Pan/tobacco, Clothing and footwear, Housing, Fuel and light, Household goods, Health, Transport and communication, Recreation, Education, Personal care, Miscellaneous) and the **General Index** (overall inflation for all categories combined)
- **Oil data (Q5):** Brent crude monthly average prices for 2021 to 2023

## Excel analysis file (Google Drive)

[India CPI Inflation Case Study - Excel File]([PASTE-YOUR-GOOGLE-DRIVE-LINK-HERE](https://docs.google.com/spreadsheets/d/1C6jBW9gnhz7IieU8gSdJdBZSiMCeflX3/edit?gid=100897086#gid=100897086))

## Workbook structure

| Sheet | Purpose |
|---|---|
| `Overview` | Objective, CPI basics, formulas, assumptions and colour code |
| `Raw_Data` | Untouched source data |
| `Cleaned_data` | Cleaned data with imputed values, corrected labels and two helper columns (`Month_No`, `Key_YYYYMM`) |
| `Calc_RU` | Calculation sheet: index, YoY % and MoM % for every category (Rural+Urban), all formulas |
| `Q1_Contribution` | Category contribution tables for Rural+Urban, Rural and Urban, with chart |
| `Q2_YoY_Trend` | Yearly inflation tables, highest-year lookup, bar and line charts |
| `Q3_Food_Analysis` | Food MoM table (combined, Rural, Urban), sub-category changes, charts |
| `Q4_COVID_Impact` | Before vs after March 2020 comparison and chart |
| `Q5_Oil_Correlation` | Oil price series, correlation of every category with oil, chart |


## Data cleaning

| Issue | Treatment |
|---|---|
| "NA" values across categories | Imputed with the average of the previous and next month: `=AVERAGE(previous, next)` |
| Rural Housing blank | Left blank and excluded, because Housing is not part of the Rural CPI basket (a 0 would be read as a real price) |
| April 2019 missing entirely | Added three rows (Rural, Urban, Rural+Urban) interpolated from March and May 2019, so every year has 12 months |
| Month-label typos (`"Marcrh"`, `"November "`) | Corrected so month-based lookups work |
| Row order independence | Added a `Key_YYYYMM` column (Year x 100 + Month number, e.g. May 2023 = 202305) so formulas look up values by key instead of by row position |

## Key formulas

| Calculation | Formula |
|---|---|
| Value lookup by sector and month | `=SUMIFS(category column, Sector, "Rural+Urban", Key, YYYYMM)` |
| Year-on-year inflation % | `=(CPI this month / CPI same month last year - 1) * 100` |
| Month-on-month inflation % | `=(CPI this month / CPI last month - 1) * 100` |
| Yearly average index | `=AVERAGEIFS(General Index, Year, year)` |
| Category contribution % | `=category index / SUM(all category indices)` |
| Correlation with oil | `=CORREL(category MoM % range, oil MoM % range)` |
| Highest / lowest lookup | `=INDEX(labels, MATCH(MAX(values), values, 0))` |

## Questions, approach and insights

### Q1. Category contribution to the CPI basket (May 2023)

**Question:** Based on the latest month's data, identify the contribution of broader categories towards the CPI basket and find the highest contributor. Contributions must add up to 100%.

**Approach:**
- The latest month is found with `MAX(Key)`, which gives 202305 (May 2023)
- The 12 broader CPI divisions are used as buckets. The data already contains their combined indices (for example, Food and beverages), so the sub-items are not added again
- With equal weights across categories, contribution = category index/sum of all 12 indices, so the total is 100%
- Done separately for Rural+Urban, Rural and Urban

**Insights:**
- **Pan, tobacco and intoxicants have the highest contribution: 9.31%** (Rural 10.0%, Urban 9.5%)
- Its index is about 201, the highest of all 12 categories
- Other categories range from 7.6% (Transport and communication, lowest) to 8.6% (Clothing and footwear)
- Rural has no Housing in its basket, so Rural shares are calculated over 11 categories

### Q2. Year-on-year inflation trend (2017 - 2023)

**Question:** Show the YoY CPI inflation trend (Rural+Urban) from 2017 for the entire basket, graph it, and identify the year with the highest inflation and the reason behind it.

**Approach:**
- Uses the Rural+Urban **General Index**, which represents the entire basket combined
- Yearly average index is calculated with `AVERAGEIFS`, then YoY % between consecutive years
- The same result is cross-checked as the average of the monthly YoY rates
- Charts: yearly YoY bar chart and monthly YoY line chart

**Insights:**
- **2022 had the highest inflation: 6.62%**, with monthly YoY peaking at 7.79% in April 2022
- Inflation was moderate in 2017 to 2019 (3.3% to 4.0%) and elevated in 2020 to 2022 (5.8% to 6.6%)
- January to May 2023 inflation is still about 5.6% compared with the same months of 2022
- **Reason for 2022:** the Russia-Ukraine war from February 2022 raised crude oil, edible oil, wheat and fertiliser prices, on top of supply chains that had not fully recovered from COVID

### Q3. Food inflation (June 2022 - May 2023)

**Question:** Analyse the broader food category's month-on-month changes for the 12 months ending May 2023, highlight the highest and lowest months, and identify the biggest individual food category contributor to inflation.

**Approach:**
- Month-on-month % change of the Food and beverages index for Rural+Urban, Rural, and Urban (May 2022 is the base for the first change)
- Highest and lowest months found with `MAX`/`MIN` and `INDEX/MATCH`
- Absolute change in index points for each of the 12 food sub-categories between May 2022 and May 2023, ranked
- Charts: MoM line chart and sub-category change bar chart

**Insights:**
- **Highest MoM food inflation: October 2022 (+1.01%). Lowest: December 2022 (-1.35%)**, consistent with a winter vegetable price correction
- Prices rose every month from June to October 2022, fell in November and December, were flat in March 2023, and rose again in April (+0.51%) and May (+0.68%)
- **Spices** contributed the most to food inflation (+33.1 index points, +17.9%), followed by Cereals (+19.6) and Milk and products (+14.6)
- **Oils and fats** fell the most (-32.4), in line with easing global edible oil prices, then Vegetables (-13.9)

### Q4. Impact of COVID-19 (onset March 2020)

**Question:** Investigate how the onset and progression of COVID-19 affected inflation, focusing on healthcare, food and essential services, by comparing the trend before and after March 2020.

**Approach:**
- Two 12-month windows: before (March 2019 to February 2020) and after (March 2020 to February 2021)
- Average YoY % calculated for each window for food, cereals, meat and fish, pulses, vegetables, oils and fats, health, fuel and light, transport and communication, and the General Index
- Change in percentage points, plus YoY in February 2020, June 2020 and the peak in the post window
- Chart: before vs after clustered bar chart

**Insights:**
- Average inflation rose from **4.51% to 5.67%** after the lockdown (+1.16 pp)
- Biggest rises: Oils and fats (+10.6 pp), Pulses (+7.3 pp), Transport and communication (+5.9 pp), Meat and fish (+5.2 pp), Cereals (+2.0 pp)
- Vegetables fell (-12.4 pp), mainly because the period before included the late-2019 vegetable price spike (31.6% YoY in February 2020)
- Health inflation did not spike (-2.1 pp); CPI measures price changes, not healthcare usage

### Q5. Imported oil prices and inflation (2021 - 2023)

**Question:** Investigate how imported crude oil price fluctuations (2021 to 2023, month-on-month) influenced inflation, and identify the category whose inflation changes most strongly with oil prices.

**Approach:**
- Brent crude monthly prices and their month-on-month % change
- MoM % change of every category from `Calc_RU.`
- `CORREL` between each category's MoM % and the oil MoM %, over 28 monthly points (February 2021 to May 2023, the period CPI data covers)
- Categories ranked by correlation, with a 5% significance check (|r| of about 0.374)
- Chart: correlation bar chart for all categories

**Insights:**
- **Meat and fish (r = 0.40) and Oils and fats (r = 0.38)** show the strongest correlation with oil price changes; they are the only two that are statistically significant
- Fuel and light (0.13), Transport and communication (0.08) and the General Index (0.08) barely move with oil month to month, plausibly because retail fuel prices are administered and pass through with a lag
- Several staples are negatively correlated (Cereals -0.28, Milk -0.28, Pulses -0.25), showing monthly food prices are driven mainly by seasonality and domestic supply

## Skills and tools

- **Excel:** SUMIFS, AVERAGEIFS, COUNTIFS, INDEX/MATCH, RANK, CORREL, MAX/MIN, charts
- **Data cleaning:** imputation, handling missing months and values, fixing inconsistent labels
- **Analysis:** year-on-year and month-on-month growth, contribution analysis, before/after comparison, correlation analysis
- **Reporting:** insight writing and chart-based communication

## Author

**Anugya Singhal**
[LinkedIn](https://www.linkedin.com/in/your-profile)
