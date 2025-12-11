-- 1. REVENUE & ORDER VALIDATION  
-- Verifying total revenue and order count by City  
-- Verifying total revenue and order count by City  
SELECT   
    r.City,  
    COUNT(o.Order_ID) AS Total_Orders,  
    SUM(o.Order_Amount) AS Total_Revenue,  
    SUM(o.Order_Amount) AS Total_Revenue,  
    AVG(o.Order_Amount) AS Avg_Order_Value  
    AVG(o.Order_Amount) AS Avg_Order_Value  
FROM Orders o  
JOIN Restaurant r ON o.Restaurant_ID = r.Restaurant_ID  
JOIN Restaurant r ON o.Restaurant_ID = r.Restaurant_ID  
GROUP BY r.City  
ORDER BY Total_Revenue DESC;  
ORDER BY Total_Revenue DESC;  
  
-- 2. OPERATIONAL BOTTLENECK CHECK  
-- 2. OPERATIONAL BOTTLENECK CHECK  
-- Calculating Late Delivery % (Orders taking > 45 mins)  
SELECT   
SELECT   
    r.City,  
    COUNT(CASE WHEN o.Delivery_Time_Min > 45 THEN 1 END) * 100.0 / COUNT(o.Order_ID) AS Late_Delivery_Pct,  
    AVG(o.Delivery_Time_Min) AS Avg_Delivery_Time  
    AVG(o.Delivery_Time_Min) AS Avg_Delivery_Time  
FROM Orders o  
JOIN Restaurant r ON o.Restaurant_ID = r.Restaurant_ID  
JOIN Restaurant r ON o.Restaurant_ID = r.Restaurant_ID  
GROUP BY r.City;  
  
-- 3. CUSTOMER CHURN LOGIC REPLICATION  
-- 3. CUSTOMER CHURN LOGIC REPLICATION  
-- Identifying customers who haven't ordered in 60 days  
WITH Last_Order AS (  
WITH Last_Order AS (  
    SELECT   
    SELECT   
        Customer_ID,  
        MAX(Date) AS Last_Order_Date  
        MAX(Date) AS Last_Order_Date  
    FROM Orders  
    FROM Orders  
    GROUP BY Customer_ID  
    GROUP BY Customer_ID  
)  
SELECT   
SELECT   
    CASE   
    CASE   
        WHEN DATEDIFF(day, Last_Order_Date, GETDATE()) <= 30 THEN 'Active'  
        WHEN DATEDIFF(day, Last_Order_Date, GETDATE()) <= 30 THEN 'Active'  
        WHEN DATEDIFF(day, Last_Order_Date, GETDATE()) <= 60 THEN 'At Risk'  
        ELSE 'Churned'  
        ELSE 'Churned'  
    END AS Customer_Status,  
    END AS Customer_Status,  
    COUNT(Customer_ID) AS Customer_Count  
FROM Last_Order  
GROUP BY   
GROUP BY   
    CASE   
    CASE   
        WHEN DATEDIFF(day, Last_Order_Date, GETDATE()) <= 30 THEN 'Active'  
        WHEN DATEDIFF(day, Last_Order_Date, GETDATE()) <= 30 THEN 'Active'  
        WHEN DATEDIFF(day, Last_Order_Date, GETDATE()) <= 60 THEN 'At Risk'  
        WHEN DATEDIFF(day, Last_Order_Date, GETDATE()) <= 60 THEN 'At Risk'  
        ELSE 'Churned'  
    END;  
    END;  
  
-- 4. PARTNER PERFORMANCE RANKING  
-- 4. PARTNER PERFORMANCE RANKING  
-- Ranking restaurants by Revenue  
-- Ranking restaurants by Revenue  
SELECT TOP 10  
    r.Restaurant_Name,  
    r.Cuisine,  
    SUM(o.Order_Amount) AS Total_Revenue  
    SUM(o.Order_Amount) AS Total_Revenue  
FROM Orders o  
FROM Orders o  
JOIN Restaurant r ON o.Restaurant_ID = r.Restaurant_ID  
JOIN Restaurant r ON o.Restaurant_ID = r.Restaurant_ID  
GROUP BY r.Restaurant_Name, r.Cuisine  
GROUP BY r.Restaurant_Name, r.Cuisine  
ORDER BY Total_Revenue DESC;  
