# Global-Inflation-Food-Prices-Project

Interactive Power BI dashboard analyzing real global inflation trends and food price changes from 2010–2024.  
Includes key metrics, country risk classifications, and year-over-year comparisons to identify high-risk regions and economic patterns.  
All datasets are real, not fictional.

---

## 📂 Project Files
- 📊 [Dashboard (.pbix)](Inflation%20Project%20BI.pbix)  
- 📜 [DAX Measures](DAX_Measures_Inflation_Project.md)  
- 📂 **Data Files:**
  - [countries.csv](data/countries_202507270014%20-%20Copy.csv)  
  - [datacode_reference_dictionary.csv](data/datacode_reference_dictionary%20-%20Copy.csv)  
  - [food_price_index.csv](data/food_price_index_202507270103%20-%20Copy.csv)  
  - [inflation.csv](data/inflation_202507270014%20-%20Copy.csv)  

---
**************************************************************************************************************
## ERD & Data Modeling
----------------------
Data Model Structure
--------------------------

<img width="547" height="547" alt="image" src="https://github.com/user-attachments/assets/fb98974d-e841-4157-a14a-f2530abd06dd" />


- countries

Core reference table for all country-level analysis

Columns: CountryID, CountryName, DevelopmentGroup (Western/Developing)

- inflation

Contains yearly inflation rates by country

Key columns: CountryName, Country_Yea (year), InflationRate, DevelopmentGroup

- food_price_index

Contains food-specific inflation rates (YoY) by country and year

Columns: CountryName, Country_Year, Year, YoY_Food_Inflation, plus aggregate fields

- food_price_index_merged

Joined/aggregated table for complex visuals (average, dot plots)

Columns: mirrors food_price_index with additional grouping and labeling fields

Table Relationships
---------------------
food_price_index (Country_Year) — * to 1 — inflation (Country_Yea)

food_price_index (CountryName) — * to 1 — countries (CountryName)

food_price_index_merged (Country_Year) — * to 1 — inflation (Country_Yea)

food_price_index_merged (CountryName) — * to 1 — countries (CountryName)

inflation (CountryName) — * to 1 — countries (CountryName)

Additional: aggregate/join on AvgFoodIndex

Relationship Notes

Star schema: All analytics run through countries as a hub for grouping by DevelopmentGroup

1-to-many: Time-series tables (inflation, food_price_index, food_price_index_merged) connect on both country and year, enabling seamless YoY and cross-country comparisons

No circular or ambiguous joins: All relationships are single-directional and clean—supporting transparent, reliable metrics

**************************************************************************************************************

## 📌 Key Insights

- Food inflation and CPI move together—except the impact is amplified in poorer countries.
  When overall inflation rises, food prices surge even faster in developing economies.

- 2022–2024 broke the pattern.
  Food prices exploded in a handful of developing countries. Example: Ethiopia’s food inflation hit 181% in 2024.

- Most countries stayed stable. Four did not.
  Out of 23 countries, just 4 hit the “High Risk” threshold. Their food inflation rates weren’t just higher—they were off the charts, with some over 100% for more   than one year.

- It’s not random.
  Every “High Risk” country is a developing nation. The data points to structural vulnerabilities, not isolated crises.

**************************************************************************************************************
Visual Overview
-----------------
Geographic Risk Map
--------------------

Shows global distribution of food inflation risk (Western nations generally low risk, developing nations dominate high risk).
<img width="1307" height="732" alt="image" src="https://github.com/user-attachments/assets/4c76a5ae-5ce6-4f27-9ccb-7e29830d1c20" />

Scatter Plot: Food Inflation vs. CPI
-------------------------------------

Strong positive correlation, but steeper slope for developing nations.
<img width="1308" height="732" alt="image" src="https://github.com/user-attachments/assets/0c0d6ead-00a8-46dc-adff-a48def742132" />

Year-on-Year Trends
---------------------

Food inflation remained modest until 2022, then spiked in select countries.

Ethiopia, Ghana, Nigeria, Pakistan stand out for multi-year, double/triple-digit food inflation.

<img width="1307" height="732" alt="image" src="https://github.com/user-attachments/assets/b589fa2b-3809-4ef1-b98a-9e12c44ed8cc" />

<img width="1307" height="735" alt="image" src="https://github.com/user-attachments/assets/53023750-b74a-42bc-8cee-4367f32d1e4b" />

High-Risk Table
------------------

Ethiopia: Highest observed food inflation (181% in 2024).

All high-risk countries are developing economies.

Western countries’ average food inflation remains below 3% even during global crises.

<img width="1303" height="731" alt="image" src="https://github.com/user-attachments/assets/eadd5ef1-4b8d-4547-ad18-ab0edff52599" />

Insights Panel
-----------------

Only 4 countries flagged “High Risk”.

Average total inflation (all countries, all years): 5.93%.

Visual breakdown of risk level count and leading high-risk nations.

<img width="1301" height="726" alt="image" src="https://github.com/user-attachments/assets/165a59aa-1b8a-4bea-b3b4-9dbda41f3d1b" />

<img width="1296" height="732" alt="image" src="https://github.com/user-attachments/assets/3e8f006f-c406-4099-97b6-254d2ac92b09" />

**************************************************************************************************************

Data Caveats
---------------

- All data sources are real. No synthetic or fabricated data has been used.

- Coverage: Data spans 2010–2024, but not all countries or years are represented. The analysis emphasizes year-on-year and cross-country patterns where data is      available.

- Risk definition: “High Risk” countries are flagged strictly based on observed food inflation rates—no subjective or qualitative classification.

- Dashboard interactivity: The screenshots shown here represent a static view of the report. The actual Power BI dashboard is fully interactive, allowing users to   explore the data dynamically using slicers and filters.

  **************************************************************************************************************



