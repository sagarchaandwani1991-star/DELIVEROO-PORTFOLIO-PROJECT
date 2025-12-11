🛵 Deliveroo Strategic Performance Analyst: Operations & CRM (2023)
![alt text](https://img.shields.io/badge/Power_BI-Desktop-yellow?style=for-the-badge&logo=power-bi)

![alt text](https://img.shields.io/badge/SQL-Data_Validation-blue?style=for-the-badge&logo=postgresql)

![alt text](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)
📖 Client Background
Client: Deliveroo | Industry: Food Delivery & Logistics
Deliveroo is a British online food delivery company that operates a hyper-local three-sided marketplace, connecting consumers, restaurants, and riders. It is one of the dominant players in the UK "Gig Economy," processing millions of orders via its app-based platform. The business model relies on speed, logistics optimization, and high-frequency customer retention.
⚠️ The Business Scenario & Problem
The Scenario:
Deliveroo is scaling rapidly across major UK hubs (London, Leeds, Manchester, Birmingham), generating £236.9K in revenue from a sample of 5,000 recent orders. While top-line revenue is strong, the "Growth at all costs" strategy has created cracks in the operation.
The Business Problem:
The leadership team has flagged two critical threats to profitability:
Operational Meltdown: A dangerously high Late Delivery Rate (47.9%), leading to customer complaints, refunds, and brand damage.
The Leaky Bucket: Despite acquiring new users, the Churn Rate is 59.4%. Customers are ordering once or twice and then abandoning the platform.
📑 Table of Contents
Executive Summary & Impact
Key Business Questions Solved
Data Structure (Star Schema)
Dashboard Deep Dive
Strategic Recommendations
Technical Implementation
Data Dictionary
Assumptions & Future Scope
🏆 Executive Summary & Quantified Impact
This analysis integrated Operations, CRM, and Financial data to provide a holistic view of performance.
Revenue Health: Strong Average Order Value (£47.39), significantly higher than industry standards, driven by "Plus" members and premium cuisines (Sushi, Vegan).
Operational Crisis: 47.9% of all deliveries are late. London is the biggest bottleneck with a 49.8% late rate, indicating a severe shortage of riders during peak hours.
Retention Alert: The churn rate is 59.4%, meaning the platform is losing customers faster than it retains them. However, "Active" customers are highly profitable, validating the need for a retention-first strategy.
🎯 Key Business Questions Solved
Where are we losing money operationally?
Identified that 1-Star and 2-Star rated drivers have significantly higher late delivery rates.
Pinpointed London and Leeds as the cities with the highest delivery delays.
Who are our best customers?
"Plus" members have a visibly higher Average Order Value compared to Standard members.
Created a "Whale" segment of customers with high frequency and high lifetime spend (£400+).
Which Partners drive growth?
Turtle Bay is the top revenue-generating restaurant (£10K), while Sushi cuisine offers the highest margins per order.
🗂 Data Structure & Modelling
Designed a Star Schema to optimize performance and enable slice-and-dice analysis across four dimensions.
ORDERS (Fact Table): Transactional data including timestamps, delivery fees, and ratings.
Customers (Dimension): Demographics, Membership Tier (Plus/Standard), and Sign-up dates.
Restaurant (Dimension): Cuisine type, City, and Restaurant Names.
Relationships: One-to-Many relationships established between Dimensions and the Fact table using Customer_ID and Restaurant_ID.
🖼️ Dashboard Deep Dive
1. Executive Overview
A high-level health check of the business designed for the C-Suite.
![alt text](Screenshots/1_Executive_Overview.png)
Revenue Volatility: The "Revenue Trend by Month" chart shows significant volatility with sharp dips in February and September. This suggests a need for seasonal marketing pushes during these low-demand months.
Market Concentration: Leeds and London combined account for ~60% of Total Revenue, making them "Must-Win" battlegrounds. Any operational failure in these cities disproportionately impacts the bottom line.
Premium Positioning: The Average Order Value (AOV) of £47.39 is high. The "AOV by Cuisine" visual proves that niche categories like Vegan (£48) and Indian (£47) are driving this premium spend, rather than fast food.
2. Operations & Logistics
Diagnosing the root cause of the 47.9% Late Delivery Rate.
![alt text](Screenshots/2_Operations_Logistics.png)
Speed Analysis: The "Avg Delivery Time by Hour" chart reveals bottlenecks during peak lunch (12 PM) and dinner (7 PM) rushes.
Driver Performance: A clear correlation exists between low driver ratings and late deliveries.
3. Customer Insights (CRM)
Analyzing the "Leaky Bucket" retention problem.
![alt text](Screenshots/3_Customer_Insights.png)
Churn Segmentation: The Donut chart exposes the massive 59.4% Churned segment versus only 26.6% Active.
Value Matrix (Scatter Plot): Identifies specific "Whale" customers (Top Right quadrant) who order frequently and spend heavily. These are the VIPs to protect.
4. Partner & Restaurant Performance
Identifying the most valuable B2B partnerships.
![alt text](Screenshots/4_Partner_Performance.png)
Revenue Drivers: Turtle Bay generates nearly double the revenue of other top partners.
Operational Drag: Asian and Burger cuisines have high volumes but suffer from slower prep/delivery times compared to Sushi.
💡 Strategic Recommendations
1. CRM: The "Win-Back" Campaign
Finding: 59.4% of customers have churned (no order in 60 days), representing a massive loss of potential revenue.
Recommendation: Launch Operation "COMEBACK25".
Action: Target the specific "At Risk" customer list generated in the CRM Dashboard.
Incentive: Send a personalized push notification with code COMEBACK25 for 25% off their next order.
Goal: Reactivate 10% of the churned base, potentially recovering £30K+ in revenue.
2. Operation: Fix the "London Bottleneck"
Finding: London has a 49.8% late delivery rate.
Recommendation: Implement surge pricing for drivers in London during the 7 PM peak to increase driver supply and reduce wait times.
3. Partner: Optimize Prep Times
Finding: Asian cuisine orders have high delivery times.
Recommendation: Work with Asian restaurant partners to streamline kitchen prep workflows during peak hours.
🛠 Technical Implementation & Expertise
Data Modelling & DAX
Customer Segmentation: Created dynamic calculated columns using SWITCH(TRUE) to categorize customers into "Active," "At Risk," and "Churned" based on days since last order.
Time Intelligence: Calculated Order_Hour to analyze intraday logistical trends.
Conditional Formatting: Applied dynamic coloring (Red/Teal) to highlight underperforming KPIs like Late Delivery %.
SQL Validation
Used SQL to validate the integrity of the dataset before import, ensuring no orphan records existed between Orders and Customers.
📚 Data Dictionary
Reference guide to the core tables.
Table	Column	Description
ORDERS	Delivery_Time_Min	Time taken from order placement to delivery.
ORDERS	Driver_Rating	Customer rating of the driver (1-5 Stars).
Customers	Membership_Tier	"Plus" (Subscription) or "Standard" (Pay-as-you-go).
Restaurant	Cuisine	Category of food (e.g., Sushi, Burger, Vegan).
Restaurant	City	Operational region (London, Leeds, Manchester, Birmingham).
🧠 Assumptions & Future Scope
Assumptions:
Late Definition: A delivery is considered "Late" if it takes longer than 45 minutes.
Churn Definition: A customer is "Churned" if they have not placed an order in the last 60 days.
Future Scope:
Geospatial Analysis: Add a Map visual to plot exact delivery routes and identify traffic hotspots.
Basket Analysis: Analyze which items are frequently bought together to optimize menu recommendations.
