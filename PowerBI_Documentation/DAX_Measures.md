## 1. Operational Measures  
  
**Total Revenue**  
```dax  
Total Revenue = SUM('Orders'[Order_Amount])  
## Late Delivery % (Crucial KPI) Calculates the percentage of orders taking longer than 45 minutes.  
**code**  
**Dax**  
##   
Late Delivery % =   
VAR LateOrders = CALCULATE(COUNTROWS('Orders'), 'Orders'[Delivery_Time_Min] > 45)  
VAR TotalOrders = COUNTROWS('Orders')  
RETURN DIVIDE(LateOrders, TotalOrders, 0)  
**Average Delivery Time**  
**code**  
**Dax**  
##   
**2.**Avg Delivery Time = AVERAGE('Orders'[Delivery_Time_Min])  
  
  
## 3. Customer Insights (CRM) Measures  
## Customer Segmentation Logic (Calculated Column) Segments customers based on Recency (Days since last order).  
**code**  
**Dax**  
##   
Customer Status =   
VAR DaysSince = DATEDIFF(  
    CALCULATE(MAX('Orders'[Date]), FILTER('Orders', 'Orders'[customer_id] = 'Customers'[Customer_ID])),  
    CALCULATE(MAX('Orders'[Date]), ALL('Orders')),   
    DAY  
)  
RETURN  
SWITCH(TRUE(),  
    DaysSince <= 30, "Active / Loyal",  
    DaysSince <= 60, "At Risk",  
    DaysSince > 60, "Lost / Churned",  
    "Unknown"  
)  
**Churn Rate %**  
**code**  
**Dax**  
##   
Churn Rate % =   
VAR ChurnedCount = CALCULATE(COUNTROWS('Customers'), 'Customers'[Customer Status] = "Lost / Churned")  
VAR TotalBase = COUNTROWS('Customers')  
RETURN DIVIDE(ChurnedCount, TotalBase, 0)  
  
  
## 4. Time Intelligence  
## Order Hour (for Peak Analysis) Extracts the hour from the transaction timestamp to identify lunch/dinner rushes.  
**code**  
**Dax**  
##   
Order_Hour = HOUR('Orders'[Date])  
