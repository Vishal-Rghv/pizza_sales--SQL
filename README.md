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
```sql
--  Daily and cumulative revenue analysis

SELECT 
    order_date,
    ROUND(revenue, 2) AS daily_revenue,
    ROUND(SUM(revenue) OVER (ORDER BY order_date), 2) AS cum_revenue -- adding revenue day by day,
															      -- order by order, or month by month
FROM
(
    SELECT 
        orders.order_date,
        SUM(order_details.quantity * pizzas.price) AS revenue
    FROM 
        order_details 
    JOIN 
        pizzas ON order_details.pizza_id = pizzas.pizza_id
    JOIN 
        orders ON orders.order_id = order_details.order_id
    GROUP BY 
        orders.order_date
) AS daily_sales
ORDER BY 
    order_date;

-- Daily and Cumulative Revenue--

![Cumulative Revenue Output](https://github.com/Vishal-Rghv/pizza_sales--SQL/blob/424f8b2aba57bfc42dc0a1d71744c14260ebd881/Screenshot%20.png
)


