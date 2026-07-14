## India CPI Inflation Analysis (2013–2023)

## 📌 Overview
This project analyzes 10 years of Consumer Price Index (CPI) data 
sourced from the Government of India (GOI) to uncover inflation 
trends, identify key price drivers, and investigate the impact of 
major economic events on India's inflation landscape.

The analysis covers Rural, Urban, and combined (Rural+Urban) sectors 
across 30+ CPI categories from 2013 to 2023.

---

## 🎯 Objective
To translate raw government CPI index data into actionable insights 
that help understand:
- Which categories drive India's inflation the most
- How inflation has trended year over year
- How major events like COVID-19 and the Russia-Ukraine war 
  impacted prices
- How global crude oil prices influence domestic inflation 
  across categories

---

## 📂 Dataset
- **Source:** Government of India — Ministry of Statistics and 
  Programme Implementation (MOSPI)
- **Base Year:** 2012 (Base value = 100)
- **Time Period:** January 2013 to May 2023
- **Sectors:** Rural, Urban, Rural+Urban
- **Format:** Excel (.xlsx)
- **Size:** 372 rows × 30 columns

### Key columns:
- Sector, Year, Month
- 27 CPI category columns (Cereals, Meat, Egg, Housing, 
  Health, Transport, Education, etc.)
- General Index (overall CPI for that month)

---

## 🧹 Data Cleaning
- Handled missing values using **Moving Average imputation**
- Rural Housing column set to **0** (structurally excluded 
  from CPI-Rural basket per GOI methodology — rural households 
  predominantly own homes and don't pay rent)
- Standardized month and year formatting
- Verified no duplicate rows across Sector + Year + Month

---

## ❓ Questions Analyzed

### Q1 — Category Contribution (Latest Month: May 2023)
- Grouped 27 sub-categories into 11 broader segments
  (Food, Housing, Healthcare, Transport, Education, etc.)
- Calculated equal-weighted average index per segment
- Computed contribution % for each segment
- **Finding:** Pan, Tobacco & Intoxicants is the highest 
  contributor (10.52%) under equal-weight assumption, driven 
  by consistent government excise duty hikes since 2012

### Q2 — Year-on-Year Inflation Trend (2017–2023)
- Used Rural+Urban General Index to calculate annual 
  average CPI per year
- Computed YoY inflation % for each year
- **Finding:** 2022 recorded the highest inflation (6.62%), 
  driven by the Russia-Ukraine war's impact on global crude 
  oil and food commodity prices

### Q3 — Food Inflation Analysis (12 months ending May 2023)
- Calculated month-on-month % change in food bucket index
- Identified highest (June 2022: +1.03%) and lowest 
  (February 2023: -0.59%) food inflation months
- Computed absolute change per food sub-category
- **Finding:** Spices recorded the highest absolute increase 
  (+30.90 index points) while Oils & Fats saw the sharpest 
  decline (-30.90), linked to easing global edible oil prices 
  post Russia-Ukraine war

### Q4 — COVID-19 Impact Analysis
- Compared Pre-COVID (Sep 2019 – Feb 2020) vs 
  Post-COVID (Mar 2020 – Aug 2020) average CPI per category
- Focused on Healthcare, Food, and Essential Services
- **Finding:** Meat & Fish (+9.42%) and Pulses (+8.52%) 
  spiked due to panic buying while Vegetables crashed 
  (-14.48%) due to supply chain breakdown; Health surprisingly 
  remained stable (+1.85%) as routine healthcare visits dropped

### Q5 — Crude Oil Price Correlation (2021–2023)
- Sourced monthly Brent crude oil prices (2021–2023)
- Calculated MoM% for both oil prices and all CPI categories
- Used CORREL function to find correlation per category 
  per year, then averaged across 3 years
- **Finding:** Pan, Tobacco & Intoxicants (0.41) shows 
  strongest correlation with oil prices due to petroleum-based 
  packaging and logistics costs; Fuel & Light (-0.08) shows 
  near-zero correlation despite being most directly oil-linked 
  — reflecting India's government fuel price regulation policy

---

## 💡 Key Insights
- Under equal weighting, Pan & Intoxicants dominates CPI 
  contribution — but in reality, Food holds ~46% official 
  weight and would dominate under GOI's actual methodology
- 2022 was India's highest inflation year in the 2017–2023 
  period, primarily driven by the Russia-Ukraine war
- COVID-19 created a sharp divergence in food prices — 
  essential staples spiked while perishables crashed
- India's government fuel price regulation policy 
  effectively insulates domestic consumers from global 
  crude oil price shocks — Fuel & Light shows near-zero 
  oil correlation despite being most directly linked
- Rural vs Urban inflation patterns differ significantly — 
  Food dominates Rural inflation while Education dominates 
  Urban, reflecting fundamentally different spending patterns

---

## 🛠️ Tools Used
- **OnlyOffice / Microsoft Excel**
  - Pivot Tables
  - AVERAGEIFS, CORREL, AVERAGE functions
  - Data filtering and manual unpivoting
  - Line charts, Pie charts, Bar charts
  - Conditional formatting

---
