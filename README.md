 🍕  Pizza_Sales--SQL

 --Project Overview--
This project analyzes pizza sales data to answer key business questions like:
- Total revenue generated
- Top 3 pizzas per category based on revenue
- Daily and cumulative revenue trends
- Average pizzas ordered per day
- Percentage contribution of each pizza type to total revenue
  

 --Tech Stack--
- **Database:** MySQL
- **Language:** SQL
- **Dataset:** Custom pizza sales dataset (CSV)
  

--Folder Structure--
- Database schema with CREATE TABLE statements
-  All analysis SQL queries
-  Key findings and business insights
-  Sample data used for testing

  
 --Example Query--
Top 3 most ordered pizza types per category by revenue
SELECT category, pizza_id, revenue
FROM (
    SELECT 
        pt.category,
        p.pizza_id,
        SUM(od.quantity * p.price) AS revenue,
        RANK() OVER (PARTITION BY pt.category ORDER BY SUM(od.quantity * p.price) DESC) AS ranking
    FROM 
        pizza_types pt
    JOIN pizzas p ON pt.pizza_type_id = p.pizza_type_id
    JOIN order_details od ON od.pizza_id = p.pizza_id
    GROUP BY pt.category, p.pizza_id
) AS ranked
WHERE ranking <= 3;
