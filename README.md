# Olist E-Commerce – Sales Performance, Customer Experience & Retention Analysis

## Project Overview

This project uses the Brazilian Olist E-Commerce Public Dataset to explore e-commerce sales performance, customer experience, delivery reliability, and repeat-purchase behaviour.

The interactive Power BI report brings operational and commercial metrics together to help stakeholders understand how revenue is distributed, which product categories and customer states contribute to sales, and how delivery performance is associated with customer review scores.

The analysis is organized into two report pages:

1. **Executive Overview** – sales, orders, average order value, customer reviews, repeat-purchase rate, late-delivery rate, revenue trends, product categories, and geographic performance.
2. **Delivery Performance & Customer Satisfaction** – review scores by delivery status and delay bucket, alongside late-delivery rates by customer state.

> **Analytical note:** The dashboard examines relationships between delivery performance and customer satisfaction. It does not establish that delivery delays cause customers to stop purchasing. Repeat-purchase behaviour should be interpreted using its defined metric and the available order history.

## Business Objectives

- Monitor overall e-commerce sales and order performance.
- Track revenue trends over time.
- Identify product categories that contribute most to revenue.
- Compare revenue contribution across customer states.
- Understand repeat-purchase behaviour.
- Evaluate delivery timeliness and late-delivery patterns.
- Examine how review scores vary across delivery outcomes and delay buckets.
- Present findings in an interactive dashboard that supports business discussion.

## Dashboard Pages

### 1. Executive Overview

The first page provides a high-level view of business performance.

**KPI cards**
- Revenue
- Orders
- Average Order Value (AOV)
- Average Review
- Late Delivery Rate
- Repeat Purchase Rate

**Visuals**
- Monthly Revenue – revenue trend over time.
- Top 10 Categories by Revenue – highest-revenue product categories.
- Revenue by State – geographic revenue contribution.
- Year and Customer State slicers – interactive filtering.

### 2. Delivery Performance & Customer Satisfaction

The second page focuses on delivery outcomes and customer feedback.

**Visuals**
- Late Deliveries Get Much Lower Reviews – compares average review scores for delivery-status groups.
- Review Score Falls as Delays Grow – compares average review scores across delivery-delay buckets.
- Late Delivery Rate by State – compares the proportion of late deliveries across customer states.

The page also includes an explanatory insight that distinguishes observed customer-satisfaction differences from an unproven causal claim about retention.

## Key Performance Indicators

| KPI | Purpose |
|---|---|
| Revenue | Measures the sales value represented by the report's revenue measure. |
| Orders | Tracks the number of orders represented by the report's order measure. |
| Average Order Value (AOV) | Indicates the average revenue per order. |
| Average Review | Summarizes customer review scores. |
| Late Delivery Rate | Measures the share of eligible orders classified as late under the report's delivery logic. |
| Repeat Purchase Rate | Tracks the proportion of customers meeting the report's repeat-purchase definition. |

The exact calculation logic is maintained in the Power BI semantic model. Review the DAX measures and their filter context before reusing KPI values in another report or presentation.

## Tools & Technologies

- **Microsoft Power BI Desktop** – data modelling, DAX measures, report design, and interactive visualizations.
- **Power Query** – data preparation and transformation, where applicable in the PBIX.
- **DAX** – KPI and analytical measure calculations.
- **Olist Brazilian E-Commerce Public Dataset** – source data for the analysis.

## Dataset

The project is based on the Olist Brazilian E-Commerce Public Dataset, a public dataset commonly distributed through Kaggle. It contains e-commerce order, customer, product, seller, payment, review, and logistics-related information.

The report uses fields and measures including:
- Order revenue and order counts
- Order date / year-month
- Product category
- Customer state
- Delivery status and delay bucket
- Customer review score
- Repeat-purchase and late-delivery measures

Refer to the original dataset source and its usage terms when redistributing source data. The PBIX report and this documentation do not imply ownership of the original dataset.

## Business Questions

1. How does revenue change over time?
2. Which product categories generate the highest revenue?
3. Which customer states contribute most to revenue?
4. What proportion of customers place repeat orders?
5. What is the overall late-delivery rate?
6. Do average review scores differ between on-time and late deliveries?
7. How do review scores vary across delivery-delay buckets?
8. Are late-delivery rates concentrated in particular customer states?

## Key Observations

The current report contains the following stated observations, which should be revalidated against the live report after applying filters or changing the model:

- Average review score is shown as approximately **4.3** for on-time deliveries and **2.3** for late deliveries.
- Orders in the **8+ day delay** bucket are shown with an average review score of approximately **1.7**.
- The overall late-delivery rate is shown as approximately **6.8%**.
- The report's explanatory text highlights higher late-delivery rates in selected states, including AL, MA, and SE.

These figures are report-level observations, not universal rates. They may change with slicer selections, data refreshes, or measure definitions.

## How to Use the Dashboard

1. Open `Olist_Retention_Dashboard.pbix` in Power BI Desktop.
2. Select **Executive Overview** to review sales and customer KPIs.
3. Use the Year and Customer State slicers to explore different segments.
4. Review monthly revenue, category contribution, and state-level revenue.
5. Navigate to **Delivery Performance & Customer Satisfaction**.
6. Compare review scores across delivery statuses and delay buckets.
7. Examine state-level late-delivery rates.
8. Clear slicers when you want to return to the unfiltered view.

## Repository Structure

A suggested repository structure is:

```text
olist-ecommerce-analysis/
│
├── Olist_Retention_Dashboard.pbix
├── README.md
├── PROJECT_DOCUMENTATION.md
│
├── dataset/
│   └── README.md
│
└── screenshots/
    ├── executive_overview.png
    └── delivery_customer_satisfaction.png
```

Add the dataset files only if redistribution is permitted. Otherwise, use the `dataset/README.md` file to explain where the data can be obtained.

## Limitations & Considerations

- The dashboard is based on historical dataset records and does not represent live Olist business operations.
- Review scores are customer feedback indicators; they do not capture every dimension of customer experience.
- An association between delivery delays and lower review scores does not, by itself, prove causation.
- Repeat-purchase rate depends on the customer identification, order-history window, and measure definition used in the model.
- Revenue, order, and late-delivery calculations should be checked for the intended grain and treatment of cancellations, missing dates, and incomplete records.
- Geographic comparisons may be affected by differences in order volume across states.
- KPI values may change when report slicers or filters are applied.

## Potential Future Enhancements

- Add month-over-month and year-over-year revenue growth.
- Add customer cohort and repeat-purchase trend analysis.
- Add delivery lead-time distributions and on-time delivery percentage.
- Add a customer segmentation view based on purchase frequency and value.
- Add product-level profitability if cost data becomes available.
- Add drill-through pages for category, state, and customer analysis.
- Add a documented data dictionary and explicit DAX definitions for every KPI.

## Author

**Nisarg Kamble**

This project is part of a portfolio demonstrating practical skills in business intelligence, data analysis, KPI reporting, and translating data into business-focused insights.
