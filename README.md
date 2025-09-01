# Car_Sales_-skillshowcase-
This Power BI report analyzes car sales using a star schema with car_data_fact as the fact table and dimensions for cars, customers, dealers, and calendar. It tracks KPIs, trends, and insights with surrogate keys ensuring efficiency. An experimental “12% Sales Rise” page models hypothetical growth impacts.

## 🧭 Report Pages
- Sales Overview YTD
 <img width="1292" height="733" alt="Page 1" src="https://github.com/user-attachments/assets/16a97372-8422-4d7a-9f66-249b741ae89b" />

- Customer Sheet
 <img width="1297" height="728" alt="Page 2" src="https://github.com/user-attachments/assets/0785bcd4-5058-4831-8e81-04c8dc3609b1" />

- Region
 <img width="1293" height="728" alt="Page 3" src="https://github.com/user-attachments/assets/06fbecee-4497-42a0-ba91-0d8cabf0f3bf" />

- 12% Sales Rise
 <img width="1292" height="736" alt="Page 4" src="https://github.com/user-attachments/assets/e32785bb-661e-4b93-945f-a96163ba49d3" />

- KPI

- tooltip
 <img width="405" height="315" alt="TP1" src="https://github.com/user-attachments/assets/761d36e2-95b4-470b-9af9-e5f24f18f7dc" />

- tooltip2
 <img width="403" height="303" alt="TP2" src="https://github.com/user-attachments/assets/5163d161-b784-478b-9ec4-3439f3a62767" />


## 📊 Visuals Summary
Top visual types used:
- **card**: 56
- **slicer**: 8
- **tableEx**: 6
- **actionButton**: 6
- **textbox**: 4
- **areaChart**: 2
- **multiRowCard**: 2
- **treemap**: 1
- **gauge**: 1
- **image**: 1
- **clusteredColumnChart**: 1
- **map**: 1
- **donutChart**: 1
- **lineClusteredColumnComboChart**: 1
- **lineChart**: 1


## 🧱 Data Model (Star Schema)
This report follows a classic **star schema** with one central **fact** table and multiple **dimension** tables.

- **Fact**: `car_data_fact`
- **Dimensions**: `car dim`, `Customer dim`, `Dealer dim`, `calendar Table`

**Surrogate Keys & Relationships**
- The star schema typically uses **integer surrogate keys** on dimensions (e.g., `CarKey`, `CustomerKey`, `DealerKey`, `DateKey`) and matching foreign keys on the fact table (e.g., `car_data_fact[CarKey] → car dim[CarKey]`).
- Based on the file metadata, the following tables are present in the model diagram: car dim, car_data_fact, Customer dim, Dealer dim, calendar Table.
- While the PBIX export exposes tables and visuals, it does not directly expose relationship metadata in a machine-readable way here. Given the usage of a Date/`calendar Table` and domain dimensions (`car dim`, `Customer dim`, `Dealer dim`), the model **strongly indicates** one-to-many relationships from each dimension into `car_data_fact`, with **single-directional** filter propagation from dimensions to fact (standard star best practice).


## 🧩 Tables Detected (from Model Diagram)
- car dim
- car_data_fact
- Customer dim
- Dealer dim
- calendar Table


## 🗂️ Columns observed in visuals
*(Likely physical attributes used as slicers/grouping fields)*
- **Customer dim** → `Customer Name`
- **Customer dim** → `target sasles`
- **Dealer dim** → `Dealer_Region`
- **calendar Table** → `Month`
- **car dim** → `Body Style`
- **car dim** → `Target Sales`
- **car dim** → `Color`
- **car dim** → `Company`
- **car dim** → `Engine`
- **car dim** → `Target Growth`
- **car dim** → `Transmission`
- **car dim** → `Max Point`
- **car dim** → `Model`
- **car dim** → `Sales Growth`
- **car dim** → `gap growth`
- **car dim** → `max point`
- **car dim** → `sales growth`


## 🧮 Measures / Calculated Fields (by naming & usage)
The following DAX measures (or calculated columns) were detected by name from visuals. Exact DAX expressions are not visible in the extracted metadata, but naming indicates **time intelligence** and **KPI** patterns:

- **car dim** → `YTD(sales)`
- **car dim** → `PY(sales)`
- **car dim** → `YTD(count)`
- **car dim** → `YTD(avg)`
- **car dim** → `YOY(sales)`
- **car dim** → `Total Avg`
- **car dim** → `YOY(count)`
- **car dim** → `YOY(avg)`
- **car dim** → `PY(count)`
- **car dim** → `Avg Difference`
- **car dim** → `MTD(avg)`
- **car dim** → `MTD(sales)`
- **car dim** → `PY %`
- **Customer dim** → `KPI (avg)`
- **Customer dim** → `KPI card(sales)`
- **Customer dim** → `KPI(count)`
- **Customer dim** → `YOY(avg)`
- **Customer dim** → `Avg Price`
- **Customer dim** → `Avg Difference`


### Time Intelligence Techniques Used
- **YTD/MTD/PY/YOY** patterns (e.g., `YTD(sales)`, `MTD(sales)`, `PY(sales)`, `YOY(sales)`) imply use of:
  - `TOTALYTD`, `DATESYTD`, `SAMEPERIODLASTYEAR`, `DATEADD`, `PARALLELPERIOD`
  - A dedicated **Calendar** table (`calendar Table`) marked as *Date Table* to enable correct time intelligence.
- **Count & Average** metrics: `YTD(count)`, `YTD(avg)`, `YOY(avg)` — suggesting separate measures for **volume** and **average price**.

### KPI & Targeting Patterns
- Presence of KPIs (e.g., `KPI (avg)`, `KPI card(sales)`, `KPI(count)`) and target attributes (`Target Sales`, `Target Growth`, `Max Point`) indicates:
  - Measures with **goal vs actual** comparisons.
  - **Conditional formatting** on cards/gauges, and possibly **KPI indicators** (up/down arrows, colors).

## 🧰 Report-Building Techniques
- **Star schema modeling** with a central fact (`car_data_fact`) and multiple conformed dimensions.
- **Surrogate keys** for relationship management (integer keys on dimensions; fact holds FKs).
- **Date table** (`calendar Table`) to support **time intelligence** (YTD/MTD/PY/YOY).
- **Slicers** for user interactivity: car dim.Engine, car dim.Body Style, car dim.Color, car dim.Transmission, car dim.Company, car dim.Model, Dealer dim.Dealer_Region, calendar Table.Month.
- **KPI Cards & Multi-row cards** for high-level metrics (56 card visuals identified).
- **Tables & Treemap** for detail and categorical composition; **Area/Line/Column/Combo** charts for trends; **Donut** for share; **Map** for geographic views (via `Dealer_Region`).
- **Tooltip pages** (`tooltip`, `tooltip2`) used for richer on-hover context.
- **Buttons/Navigation** (`actionButton`) present for guided exploration.
- **Field formatting** (cards/gauges) implied by KPI and “%” naming conventions.

## 🔧 Data Sources & Partitions
- Power BI stores source and partition details inside the model; however, in this export the `DataModel` binary is not directly readable without Power BI/Tabular Editor.
- Visual metadata and diagram nodes confirm the table names and their use across pages/visuals.

## 🧪 Validation Notes
- Total pages: **7**
- Total visuals: **92**
- Slicers detected: **8**
- Cards detected: **56**

## 🚀 How to Rebuild Locally
1. Open `https://github.com/HariVikas2119/Car_Sales_-skillshowcase-/blob/main/car_sales.pbix` in **Power BI Desktop**.
2. Verify **Model view** shows the star schema with:
   - `car_data_fact` 1*-* relationships from `car dim`, `Customer dim`, `Dealer dim`, and `calendar Table`.
3. Ensure `calendar Table` is marked as **Date table** (Model view → Table tools → Mark as date table).
4. Confirm surrogate keys:
   - Integer keys on each dimension; matching FKs in the fact.
5. Confirm time intelligence measures:
   - Use of `TOTALYTD`, `DATEADD`, `SAMEPERIODLASTYEAR`, etc., referencing `calendar Table[Date]` or `[DateKey]`.

## 📝 License
MIT (change as needed).

---

*This README was generated by inspecting the PBIX package (layout & diagram metadata). For full DAX definitions and relationship cardinalities, open the PBIX in Power BI Desktop or Tabular Editor and export the model schema.*

