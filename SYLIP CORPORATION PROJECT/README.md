# Visualizing Value: Sylip Corporation’s Roadmap to Profitability

## Table of Contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Technology](#technology)
- [Skills](#skills)
- [Exploratory Data Analaysis](#exploratory-data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)

### Project Overview

Embark on a journey into the world of retail as this project uncovers valuable insights for Sylip Corporation, a versatile retail company offering household items, groceries, clothing, and more. Leveraging sales data, the project focuses on critical key performance indicators (KPIs) to provide actionable insights. Through meticulous data manipulation, analysis, and visualization, the project reveals region-wise profits, annual revenue, and yearly units sold, offering a comprehensive understanding of the company's performance. Armed with these insights, Sylip Corporation can make informed decisions to enhance profitability and drive overall success. Explore the power of data-driven recommendations in optimizing retail strategies and maximizing performance in the competitive marketplace.

### Data Source

Company Website: The company had 3 different datasets labelled "Sales Data","Order Data" and the "Purchase Data" generated from the central point of 7 regions, the company website.

### Technology

The following technologies were used in this project:
- Microsoft Excel: Excel was used to store and manage the sales data, and perform preliminary data analysis.
- SQL Server: SQL Server was utilized for data cleaning, transformation, and manipulation to prepare the data for analysis.
- Power BI: Power BI was used for creating a relationship between the datasets, data visualization and presentation, creating interactive and informative dashboards.


### Skills
  
The project required the following skills:
- Data manipulation
- Data analysis
- Data visualization

### Exploratory Data Analysis

To explore the interactive Power BI dashboards and dive deeper into the Sylip Corporation Sales Analysis project, visit the link: [Sylip Corporation Sales Analysis](https://project.novypro.com/qG6C3h)
Feel free to reach out to the project team for any additional information or inquiries. Happy exploring!

![SYLIP DASHBOARD](https://github.com/user-attachments/assets/9088049e-2944-44f9-bab0-cb3dd026ee5c)


The stakeholders wanted a detailed report on the following Metrics

- Compute total profit for all regions
- Rate of Revenue achieved in all regions.
- Determine the gross profit margin for each item type sold.
- Top 4 countries with highest and lowest revenue.
- Compare total quantity sold year by year for each item type.
- Determine the average amount of profit achieved annually

After a Data cleaning process using Excel, the data was imported to SQL to drive further analyses on the datasets. Examples are shown below;

```sql
-- KPI 4 - RATE OF REVENUE ACHIEVED IN ALL REGIONS

SELECT DISTINCT REGION,

SUM(TOTAL_REVENUE)*100/(SELECT SUM(TOTAL_REVENUE) AS 'TOTAL REVENUE'
FROM PURCHASE_TABLE) AS '% RATE OF REVENUE'

FROM PURCHASE_TABLE

JOIN
CUSTOMER_TABLE
ON
PURCHASE_TABLE.Order_ID = CUSTOMER_TABLE.Order_ID
GROUP BY REGION;
```

```sql
-- KPI 5 - DETERMINE THE GROSS PROFIT MARGIN FOR EACH ITEM SOLD

SELECT DISTINCT ITEM_TYPE, SUM(TOTAL_REVENUE) AS 'TOTAL REVENUE',
SUM(TOTAL_COST) AS 'TOTAL COST', SUM(TOTAL_REVENUE-TOTAL_COST) AS 'TOTAL PROFIT',
ROUND (SUM(TOTAL_PROFIT*100)/SUM(TOTAL_REVENUE), 2) AS 'GROSS PROFIT MARGIN'
FROM
ORDER_TABLE
JOIN
PURCHASE_TABLE
ON
ORDER_TABLE.Order_ID = PURCHASE_TABLE.ORDER_ID
GROUP BY ITEM_TYPE;

```

```sql
-- KPI 8 - DETERMINE THE REVENUE GROWTH RATE YEAR ON YEAR (YOY)

SELECT 
    YEAR(ORDER_DATE),
    TOTAL_REVENUE,
    LAG(TOTAL_REVENUE) OVER (ORDER BY YEAR(ORDER_DATE)) AS 'PREVIOUS YEAR REVENUE',

    CASE 

        WHEN LAG(TOTAL_REVENUE) OVER (ORDER BY YEAR(ORDER_DATE) IS-NULL THEN NULL
        ELSE ROUND(((TOTAL_REVENUE - LAG(TOTAL_REVENUE) OVER (ORDER BY YEAR(ORDER_DATE))) / LAG(TOTAL_REVENUE) OVER (ORDER BY YEAR(ORDER_DATE)) * 100, 2)
    END AS 'REVENUE GROWTH RATE'

FROM 
    ORDER_TABLE
JOIN
PURCHASE_TABLE
ON
ORDER_TABLE.Order_ID = PURCHASE_TABLE.ORDER_ID

WHERE 
    YEAR(ORDER_DATE) BETWEEN YEAR(2010) - 8 AND YEAR(2017)
ORDER BY 
    YEAR(ORDER_DATE);
```



### Results

The Sylip Corporation Sales Analysis project involved utilizing sales data from a retail company that specializes in various products. The aim was to provide the company with valuable insights into key performance indicators (KPIs) such as region-wise profits, annual revenue, and yearly units sold. The project involved data manipulation, analysis, and visualization to provide actionable recommendations that could improve the company's profitability and overall performance. The following results were deduced from the analyses;

- High-Margin Categories: Clothes (67.52%) offer the highest gross profit margin, while Cereal (43.49%) and Vegetables (41.51%) balance affordability with profitability. Low-margin items include Meat (13.62%) and high-cost products like Office Supplies (19.44%).
- Top Revenue Regions: Sub-Saharan Africa (28.88%, $12.18M profit) and Europe (24.30%, $11.08M profit) dominate revenue generation. Moderate contributors include Asia (15.54%, $6.11M profit) and Australia/Oceania (10.26%, $4.72M profit), while North America lags with only 4.11% revenue and $1.46M profit.
- Revenue Disparity by Countries: Honduras (£6.34M), Myanmar (£6.16M), Djibouti (£6.05M), and Turkmenistan (£5.82M) lead revenue, totaling £24.37M. Conversely, Kuwait (£4.87K), Kyrgyzstan (£19.10K), New Zealand (£20.40K), and Slovakia (£26.34K) generate a combined £70.72K, highlighting significant disparities.
- Profit Distribution: Sub-Saharan Africa and Europe are the most profitable regions, with $12.18M and $11.08M respectively. Asia ($6.11M) and MENA ($5.76M) show moderate profits, while North America ($1.46M) underperforms due to inefficiencies.


### Recommendations

Based on the analysis, we recommend the following actions:
- Prioritize High-Performing Regions and Products: Focus on Sub-Saharan Africa (28.88% revenue, $12.18M profit) and Europe (24.30% revenue, $11.08M profit) for market expansion. Invest in high-margin products like Clothes (67.52%), Cereal (43.49%), and Vegetables (41.51%) to maximize profitability.

- Improve Efficiency in Moderate and Emerging Markets: Optimize supply chains and target marketing in regions like Asia (15.54% revenue, $6.11M profit) and MENA (10.23% revenue, $5.76M profit). Explore growth potential in emerging markets to increase profitability and market share.

- Address Underperformance in Low-Contributing Regions: Conduct market analysis in underperforming regions like North America (4.11% revenue, $1.46M profit) and Central America and the Caribbean (6.68% revenue, $2.85M profit) to address inefficiencies and better align products with consumer needs.


