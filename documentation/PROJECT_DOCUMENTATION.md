# Project Documentation
## Olist E-Commerce – Sales Performance, Customer Experience & Retention Analysis

## 1. Project Summary

### 1.1 Background

E-commerce businesses need to monitor more than sales volume. Revenue trends, product mix, geographic performance, delivery reliability, customer feedback, and repeat purchasing all contribute to a broader understanding of business performance.

This project uses the Olist Brazilian E-Commerce Public Dataset to build an interactive Power BI dashboard. The report is designed to help a business user review commercial performance and investigate the relationship between delivery outcomes and customer satisfaction.

### 1.2 Project Purpose

The purpose of the project is to:
- Consolidate important sales and customer-experience indicators into an interactive report.
- Make revenue and order patterns easier to explore.
- Identify leading product categories and customer states by revenue.
- Monitor late-delivery performance.
- Compare customer review scores across delivery outcomes.
- Examine repeat-purchase behaviour without overstating what the available data proves.

### 1.3 Intended Audience

- Business analysts
- E-commerce operations teams
- Sales and category managers
- Customer-experience teams
- Logistics and delivery stakeholders
- Management reviewing business performance

## 2. Dataset Overview

### 2.1 Source

**Dataset:** Olist Brazilian E-Commerce Public Dataset  
**Publisher:** Olist  
**Public distribution:** Kaggle (search for the exact dataset title)

The dataset contains historical records from a Brazilian e-commerce marketplace. Depending on the files used in the model, the source data can include orders, order items, customers, products, sellers, payments, reviews, and geolocation information.

### 2.2 Relevant Analytical Fields

The current report's visual definitions reference the following fields and measures:

| Analytical area | Fields / measures used in the report |
|---|---|
| Sales | `Revenue` |
| Order volume | `Orders` |
| Average order value | `AOV` |
| Customer feedback | `Avg Review` |
| Repeat purchasing | `Repeat Rate` |
| Delivery performance | `Late %`, `Delivery Status`, `Delay Bucket` |
| Time analysis | `Year Month`, `Year` |
| Product analysis | `product_category_name_english` |
| Geographic analysis | `customer_state` |

The semantic model contains the table/entity `olist_orders_dataset`, and the report also references `olist_customers_dataset` for customer-state analysis. Confirm the complete model table list in Power BI Model view before publishing a formal data dictionary.

### 2.3 Data Grain and Relationships

The report combines order-level measures with customer, product-category, time, and geographic attributes. Before changing relationships or adding new measures, confirm the grain of each source table.

Recommended modelling checks:
- Identify the unique key for each table.
- Confirm whether order items create multiple rows per order.
- Avoid summing order-level revenue after joining it to item-level rows unless the measure accounts for the grain.
- Check relationship cardinality and filter direction.
- Confirm that customer and order identifiers are unique where expected.
- Validate date relationships used by monthly and yearly analysis.

Do not assume every table is at order level. An order can contain multiple items and may have multiple payment or review-related records.

## 3. Business Requirements & Questions

The report is intended to answer the following questions.

### Sales and commercial performance
1. What revenue is represented in the selected reporting period?
2. How many orders are represented?
3. What is the average order value?
4. How does revenue change month by month?
5. Which product categories contribute the most revenue?
6. Which customer states contribute the most revenue?

### Customer and delivery performance
7. What is the average customer review score?
8. What proportion of customers are repeat purchasers under the model's definition?
9. What is the late-delivery rate?
10. How do review scores differ between on-time and late deliveries?
11. How do review scores vary by delivery-delay bucket?
12. Which customer states have comparatively high late-delivery rates?

## 4. Power BI Report Design

The report uses a 1920 × 1080 (16:9) page canvas and contains two pages.

### Page 1 – Executive Overview

**Purpose:** Provide a high-level view of commercial performance and customer indicators.

#### KPI cards

| KPI | Business interpretation |
|---|---|
| Revenue | Overall sales value represented by the Revenue measure. |
| Orders | Number of orders represented by the Orders measure. |
| AOV | Average Order Value; an indicator of average order size by value. |
| Average Review | Average customer review score under the model's calculation. |
| Late % | Share of eligible orders classified as late under the model's logic. |
| Repeat Rate | Share of customers classified as repeat purchasers under the model's definition. |

#### Visual 1 – Monthly Revenue

- **Visual type:** Line chart
- **Axis:** `Year Month`
- **Value:** `Revenue`
- **Purpose:** Show how revenue changes over time and identify broad trends or fluctuations.
- **Business use:** Helps stakeholders investigate periods of stronger or weaker sales.

#### Visual 2 – Top 10 Categories by Revenue

- **Visual type:** Clustered bar chart
- **Category:** `product_category_name_english`
- **Value:** `Revenue`
- **Purpose:** Rank the ten product categories with the highest revenue.
- **Business use:** Helps identify major revenue-contributing categories.

#### Visual 3 – Revenue by State

- **Visual type:** Clustered column chart
- **Axis:** `customer_state`
- **Value:** `Revenue`
- **Purpose:** Compare revenue across customer states.
- **Business use:** Supports geographic performance comparisons.

#### Slicers

- `Year`
- `customer_state`

**Interaction:** Slicers allow users to filter the report and examine a selected year or customer state. Verify visual interactions in Power BI if any chart is intentionally excluded from filtering.

### Page 2 – Delivery Performance & Customer Satisfaction

**Purpose:** Explore the relationship between delivery outcomes and customer review scores, and identify geographic differences in late deliveries.

#### Visual 1 – Late Deliveries Get Much Lower Reviews

- **Visual type:** Clustered column chart
- **Axis:** `Delivery Status`
- **Value:** `Avg Review`
- **Purpose:** Compare average review scores for delivery-status groups.
- **Business use:** Helps assess whether customer feedback differs between on-time and late deliveries.

#### Visual 2 – Review Score Falls as Delays Grow

- **Visual type:** Clustered column chart
- **Axis:** `Delay Bucket`
- **Value:** `Avg Review`
- **Purpose:** Compare review scores across delivery-delay categories.
- **Business use:** Helps identify whether longer delays coincide with lower average review scores.

#### Visual 3 – Late Delivery Rate by State

- **Visual type:** Clustered column chart
- **Axis:** `customer_state`
- **Value:** `Late %`
- **Purpose:** Compare late-delivery rates across customer states.
- **Business use:** Helps identify geographic areas that may warrant further logistics investigation.

#### Narrative insight

The current report contains the following stated observations:
- On-time deliveries: approximately 4.3 average review score.
- Late deliveries: approximately 2.3 average review score.
- Orders in the 8+ day delay bucket: approximately 1.7 average review score.
- Overall late-delivery rate: approximately 6.8%.
- The report highlights higher late-delivery rates in selected states, including AL, MA, and SE.

These values should be rechecked in the interactive report. They are not guaranteed to remain constant under slicers, filters, or model changes.

## 5. KPI Definitions and Validation

The PBIX contains measures named `Revenue`, `Orders`, `AOV`, `Avg Review`, `Late %`, and `Repeat Rate`. The report file's visual metadata confirms these measure names, but a visual's field reference does not expose the complete DAX formula.

Use the following as business definitions to validate against the actual DAX expressions in the model.

| KPI | Suggested business definition | Validation point |
|---|---|---|
| Revenue | Sum of the intended sales/revenue amount. | Confirm the amount column, order status rules, and table grain. |
| Orders | Count of distinct qualifying order IDs. | Confirm whether cancelled or unavailable orders are excluded. |
| AOV | Revenue divided by qualifying orders. | Ensure numerator and denominator use consistent filters. |
| Avg Review | Average of valid review scores. | Check duplicate reviews, missing values, and review grain. |
| Late % | Late qualifying orders divided by eligible orders. | Confirm the delivery-date comparison and treatment of missing dates. |
| Repeat Rate | Customers meeting the repeat-purchase definition divided by eligible customers. | Document the repeat threshold and observation window. |

### Recommended DAX validation checks

- Use `DISTINCTCOUNT` where the intended metric is unique orders or customers.
- Protect ratios from division by zero, for example with `DIVIDE`.
- Confirm that numerator and denominator share the same filter context.
- Decide explicitly how cancelled, unavailable, and undelivered orders are treated.
- Validate whether repeat purchasing means two or more orders per customer within the available history.
- Confirm whether late delivery compares actual delivery date with estimated delivery date.
- Test each measure with a small manually checked subset of records.

These are validation recommendations, not a claim that the current measures use these exact formulas.

## 6. Analytical Methodology

A recommended workflow for reproducing and maintaining the analysis is:

1. **Source review:** Identify the source files and inspect their columns, data types, keys, and missing values.
2. **Data preparation:** Standardize data types, review nulls, and prepare the fields needed for time, product, customer, and delivery analysis.
3. **Data modelling:** Establish appropriate relationships and confirm table grain to prevent double counting.
4. **Measure development:** Create and validate business KPIs using DAX.
5. **Visual development:** Build the two report pages around the business questions.
6. **Interaction testing:** Verify slicers, cross-filtering, sorting, and tooltip behaviour.
7. **Result validation:** Reconcile important totals and percentages against source data or independent calculations.
8. **Documentation:** Record KPI definitions, assumptions, and known limitations.

## 7. Business Insights and Interpretation

### 7.1 Delivery performance and customer satisfaction

The current report shows a lower average review score for late deliveries than for on-time deliveries. It also shows lower average reviews in longer-delay buckets.

**Interpretation:** Delivery experience and customer feedback appear to be associated in this dataset. This is a useful operational signal for further investigation.

**Do not conclude:** The dashboard alone does not prove that delivery delays cause customers to stop purchasing. Other factors, such as product quality, seller performance, order value, location, and customer expectations, may also influence reviews and repeat purchases.

### 7.2 Geographic delivery performance

The state-level late-delivery chart allows comparison of delivery reliability across customer locations.

**Interpretation:** States with higher late-delivery rates may warrant further investigation into logistics coverage, carrier performance, distance, and order mix.

**Validation:** Compare both the late-delivery percentage and the underlying number of eligible orders. A high percentage based on a small number of orders should be interpreted carefully.

### 7.3 Revenue and category performance

The monthly trend, category ranking, and state comparison provide a commercial overview.

**Interpretation:** These views can help identify revenue concentration, seasonality, and geographic differences. Further analysis is required before making pricing, inventory, or expansion decisions.

### 7.4 Repeat-purchase behaviour

The Repeat Rate KPI provides a summary of repeat purchasing under the model's definition.

**Interpretation:** Repeat purchasing is relevant to retention analysis, but a single overall percentage does not explain when customers return, how frequently they purchase, or which groups are most likely to return.

**Recommended extension:** Add cohort retention, time-to-second-purchase, and repeat-rate trends by acquisition month.

## 8. Design and Usability Guidelines

Recommended presentation standards for the final report:

- Use a 16:9 canvas.
- Use a light neutral background and consistent white visual containers.
- Use a restrained navy, blue, and teal palette.
- Keep KPI cards aligned and equal in size.
- Use consistent chart-title and label formatting.
- Sort ranking visuals in descending order.
- Use clear units and percentage formats.
- Keep slicers in a consistent, easy-to-find location.
- Avoid unnecessary borders, shadows, and decorative elements.
- Use contrasting colours consistently for on-time and late delivery.
- Ensure the report remains readable at Fit to Page and in presentation mode.

Suggested palette:
- Navy: `#173B5E`
- Blue: `#2476A8`
- Teal: `#16A6A1`
- Light background: `#F5F7FA`
- White: `#FFFFFF`
- On-time indicator: `#16A36A`
- Late-delivery indicator: `#E5A13A`

## 9. Quality Assurance Checklist

### Data and model
- [ ] Confirm source file names and refresh status.
- [ ] Check primary and foreign keys.
- [ ] Validate table relationships and cardinality.
- [ ] Confirm the grain of orders, order items, payments, and reviews.
- [ ] Check for nulls and invalid dates in delivery fields.
- [ ] Validate revenue and order totals independently.

### Measures
- [ ] Document the DAX definition of every KPI.
- [ ] Confirm AOV uses consistent revenue and order filters.
- [ ] Confirm Late % uses the intended eligible-order denominator.
- [ ] Confirm Repeat Rate uses a documented customer-level definition.
- [ ] Test measures under slicers and cross-filters.

### Report
- [ ] Check both pages at 100% and Fit to Page.
- [ ] Confirm all slicers behave as intended.
- [ ] Confirm charts are sorted and labelled clearly.
- [ ] Check that percentages and currency formats are correct.
- [ ] Ensure narrative insights match the current report values.
- [ ] Check for clipped titles, labels, and overlapping visuals.

## 10. Limitations

- The dataset represents historical records and is not a live operational feed.
- The report's findings depend on the available records and the model's definitions.
- Delivery and review-score associations do not demonstrate causation.
- Repeat-purchase calculations depend on the observation period and customer/order definitions.
- State-level percentages can be affected by differing order volumes.
- Revenue calculations may be sensitive to table grain, order status, and treatment of cancellations.
- The current report does not, by itself, establish profitability because cost and margin data may not be available.
- The current report does not include a full cohort-retention or customer-lifetime-value analysis.

## 11. Future Enhancements

Potential next steps include:

1. Add month-over-month and year-over-year revenue growth.
2. Add customer cohort retention analysis.
3. Add repeat-purchase frequency and time-to-next-order.
4. Add on-time delivery rate and delivery lead-time distributions.
5. Add customer segmentation using purchase frequency and monetary value.
6. Add seller and carrier performance analysis if suitable fields are available.
7. Add drill-through pages for products, states, and customer segments.
8. Add a KPI glossary with exact DAX expressions and filter assumptions.
9. Add a refresh and data-quality monitoring page.
10. Add cost and margin data for profitability analysis, if available.

## 12. Project Deliverables

Recommended repository deliverables:

- `Olist_Retention_Dashboard.pbix` – interactive Power BI report.
- `README.md` – concise project overview for GitHub.
- `PROJECT_DOCUMENTATION.md` – detailed project and analytical documentation.
- `screenshots/` – report-page screenshots for portfolio presentation.
- `dataset/README.md` – dataset acquisition instructions and source attribution.

## 13. Conclusion

The Olist E-Commerce dashboard demonstrates how business intelligence tools can be used to organize sales, customer, and delivery metrics into an interactive analytical report.

The Executive Overview supports commercial performance monitoring, while the Delivery Performance & Customer Satisfaction page investigates differences in review scores and late-delivery rates. Together, the pages provide a starting point for data-informed discussions across sales, customer experience, and logistics.

The most important analytical discipline is to distinguish what the dashboard directly measures from what it only suggests. Clear KPI definitions, sound data modelling, validation, and careful interpretation make the report more useful and credible.

## Author

**Nisarg Kamble**
