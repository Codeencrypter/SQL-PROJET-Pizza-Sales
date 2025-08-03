# 🍕 Pizza Sales SQL Analysis

A SQL project based on a fictional pizza sales dataset to practice solving real-world business problems using SQL.

## 🔍 Objective
Analyze sales, revenue, and ordering patterns for a pizza business using SQL.

---

## 📁 Dataset
The dataset contains details about:
- Orders
- Pizzas and categories
- Pizza sizes and prices

---

## 📊 SQL Questions & Use Cases

### 🟢 Basic


- Retrieve the total number of orders placed.
- Calculate total revenue from pizza sales.
- Identify the highest-priced pizza.
- Most common pizza size ordered.
- Top 5 most ordered pizza types (by quantity).



### 🟢 Basic Queries

```sql
SELECT count(order_id) AS total_orders 
FROM ORDERS;
```

```sql
SELECT 
    ROUND(SUM(orders_details.quantity * pizzas.price),
            2) AS total_sales
FROM
    orders_details
        JOIN
    pizzas ON pizzas.pizza_id = orders_details.pizza_id;
```

## 📸 Output Screenshots

  
<img width="921" height="413" alt="Basic" src="https://github.com/user-attachments/assets/c41a3282-7a6a-42df-bab2-6f4c27cd9628" />



### 🟡 Intermediate
- Total quantity per pizza category.
- Orders distribution by hour of the day.
- Category-wise pizza distribution.
- Daily average of pizzas ordered.
- Top 3 most ordered pizza types by revenue.

  ### 🟡 Intermediate Queries
  
```sql
 SELECT 
    ROUND(AVG(quantity), 0) AS avg_pizza_ordered_per_day
FROM
    (SELECT 
        orders.order_date, SUM(orders_details.quantity) AS quantity
    FROM
        orders
    JOIN orders_details ON orders.order_id = orders_details.order_id
    GROUP BY orders.order_date) AS order_quantity;
 ```
 

  

```sql
 SELECT 
    HOUR(order_time) AS hour, COUNT(order_id) AS order_count
FROM
    orders
GROUP BY HOUR(order_time);
 ```

   ## 📸 Output Screenshots 

<img width="918" height="477" alt="Intermediate" src="https://github.com/user-attachments/assets/0691c15a-ac8b-4b01-8f3f-0ab6b2fdeeb6" />



### 🔴 Advanced
- % revenue contribution of each pizza type.
- Cumulative revenue over time.
- Top 3 pizza types by revenue for each category.

### 🔴 Advanced Queries

```sql
SELECT order_date,
SUM(revenue) over(order by order_date) AS cum_revenue
FROM 
(SELECT orders.order_date,
SUM(orders_details.quantity * pizzas.price) AS revenue
FROM orders_details JOIN pizzas
ON orders_details.pizza_id = pizzas.pizza_id
JOIN orders
ON orders.order_id - orders_details.order_id
GROUP BY orders.order_date) AS sales;
 ```



```sql
SELECT 
    pizza_types.name,
    SUM(orders_details.quantity * pizzas.price) AS revenue
FROM
    pizza_types
        JOIN
    pizzas ON pizzas.pizza_type_id = pizza_types.pizza_type_id
        JOIN
    orders_details ON orders_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.name
ORDER BY revenue DESC
LIMIT 3;
 ```

  ## 📸 Output Screenshots


 <img width="915" height="513" alt="Advanced" src="https://github.com/user-attachments/assets/cec09046-239f-4b6b-b7a6-e2774759147b" />

---

## 🧠 Skills Used
- JOINs, GROUP BY, CTEs, Subqueries
- Date/time functions
- Window functions
- Aggregations and formatting

