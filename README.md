# theLook CRM

## 1. Summary

## 2. Introduction
Data: https://console.cloud.google.com/marketplace/product/bigquery-public-data/thelook-ecommerce?hl=en&project=causal-flame-283208


## 2. Objective

## 3. Analysis
1. Overall sales performance
- Total market: $   4322.98
```
SELECT round(SUM(t2.sale_price),2) AS total_revenue
FROM `bigquery-public-data.thelook_ecommerce.orders` AS t1 
LEFT JOIN (
    SELECT id, order_id, user_id, product_id, sale_price 
    FROM `bigquery-public-data.thelook_ecommerce.order_items`
) AS t2
ON t1.order_id = t2.order_id
LEFT JOIN `bigquery-public-data.thelook_ecommerce.users` AS t3
ON t2.user_id = t3.id
LEFT JOIN `bigquery-public-data.thelook_ecommerce.products` AS t4
ON t2.product_id = t4.id
WHERE EXTRACT(YEAR FROM TIMESTAMP(t1.created_at)) = 2024
AND EXTRACT(MONTH FROM TIMESTAMP(t1.created_at)) = 1
AND status NOT IN ('Cancelled', 'Returned')
AND brand IN ('adidas', 'Nike', 'PUMA', 'Under Armour','Reebok','New Balance') ;
```
-  
-  Brand performance in 2024 Jan
   Adidas's Revenue: 1279.21 , Adidas's Cost: 625.52, Adidas's Gross Profit: 653.69
   
```
SELECT 
    brand, 
    ROUND(SUM(t2.sale_price), 2) AS total_revenue, 
    ROUND(SUM(t4.cost), 2) AS total_cost, 
    ROUND(SUM(t2.sale_price) - SUM(t4.cost), 2) AS gross_profit, 
    (ROUND(SUM(t2.sale_price) / (SELECT ROUND(SUM(t2.sale_price), 2) AS total_revenue
                                 FROM `bigquery-public-data.thelook_ecommerce.orders` AS t1 
                                 LEFT JOIN (
                                     SELECT id, order_id, user_id, product_id, sale_price 
                                     FROM `bigquery-public-data.thelook_ecommerce.order_items`
                                 ) AS t2
                                 ON t1.order_id = t2.order_id
                                 LEFT JOIN `bigquery-public-data.thelook_ecommerce.users` AS t3
                                 ON t2.user_id = t3.id
                                 LEFT JOIN `bigquery-public-data.thelook_ecommerce.products` AS t4
                                 ON t2.product_id = t4.id
                                 WHERE EXTRACT(YEAR FROM TIMESTAMP(t1.created_at)) = 2024
                                 AND EXTRACT(MONTH FROM TIMESTAMP(t1.created_at)) = 1
                                 AND status NOT IN ('Cancelled', 'Returned')
                                 AND brand IN ('adidas', 'Nike', 'PUMA', 'Under Armour','Reebok','New Balance')), 2)) AS market_share
FROM 
    `bigquery-public-data.thelook_ecommerce.orders` AS t1 
LEFT JOIN 
    (
        SELECT id, order_id, user_id, product_id, sale_price 
        FROM `bigquery-public-data.thelook_ecommerce.order_items`
    ) AS t2
ON 
    t1.order_id = t2.order_id
LEFT JOIN 
    `bigquery-public-data.thelook_ecommerce.users` AS t3
ON 
    t2.user_id = t3.id
LEFT JOIN 
    `bigquery-public-data.thelook_ecommerce.products` AS t4
ON 
    t2.product_id = t4.id
WHERE 
    EXTRACT(YEAR FROM TIMESTAMP(t1.created_at)) = 2024
    AND EXTRACT(MONTH FROM TIMESTAMP(t1.created_at)) = 1
    AND status NOT IN ('Cancelled', 'Returned')
    AND brand IN ('adidas', 'Nike', 'PUMA', 'Under Armour', 'Reebok', 'New Balance')
GROUP BY 
    brand; ;
```
-  Country performance
```
SELECT 
    country,
    ROUND(SUM(t2.sale_price), 2) AS total_revenue, 
    ROUND(SUM(t4.cost), 2) AS total_cost, 
    ROUND(SUM(t2.sale_price) - SUM(t4.cost), 2) AS gross_profit,    
FROM 
    `bigquery-public-data.thelook_ecommerce.orders` AS t1 
LEFT JOIN 
    (
        SELECT id, order_id, user_id, product_id, sale_price 
        FROM `bigquery-public-data.thelook_ecommerce.order_items`
    ) AS t2
ON 
    t1.order_id = t2.order_id
LEFT JOIN 
    `bigquery-public-data.thelook_ecommerce.users` AS t3
ON 
    t2.user_id = t3.id
LEFT JOIN 
    `bigquery-public-data.thelook_ecommerce.products` AS t4
ON 
    t2.product_id = t4.id
WHERE 
    EXTRACT(YEAR FROM TIMESTAMP(t1.created_at)) = 2024
    AND EXTRACT(MONTH FROM TIMESTAMP(t1.created_at)) = 1
    AND status NOT IN ('Cancelled', 'Returned')
    AND brand ='adidas'
GROUP BY country
ORDER BY total_revenue DESC;
```

2. Sales trend

```
 SELECT 
        year,
        month,
        ROUND(SUM(t2.sale_price), 2) AS total_revenue, 
        ROUND(SUM(t4.cost), 2) AS total_cost, 
        ROUND(SUM(t2.sale_price) - SUM(t4.cost), 2) AS gross_profit
    FROM 
        (SELECT *,
        EXTRACT(YEAR FROM TIMESTAMP(created_at)) AS year,
        EXTRACT(MONTH FROM TIMESTAMP(created_at)) AS month,
        FROM `bigquery-public-data.thelook_ecommerce.orders`) AS t1 
    LEFT JOIN (
            SELECT id, order_id, user_id, product_id, sale_price 
            FROM `bigquery-public-data.thelook_ecommerce.order_items`
        ) AS t2
    ON t1.order_id = t2.order_id
    LEFT JOIN `bigquery-public-data.thelook_ecommerce.users` AS t3
    ON t2.user_id = t3.id
    LEFT JOIN `bigquery-public-data.thelook_ecommerce.products` AS t4
    ON t2.product_id = t4.id
    WHERE 
        ((EXTRACT(YEAR FROM TIMESTAMP(t1.created_at)) = 2023
        AND EXTRACT(MONTH FROM TIMESTAMP(t1.created_at)) IN (1,2,3,4,5,6,7,8,9,10,11,12)) OR
         (EXTRACT(YEAR FROM TIMESTAMP(t1.created_at)) = 2024 AND EXTRACT(MONTH FROM TIMESTAMP(t1.created_at)) = 1))
        AND status NOT IN ('Cancelled', 'Returned')
        AND brand ='adidas'
    GROUP BY year, month
    ORDER BY year DESC, month DESC;
```

4. product level
- The most popular product, category
- The most cancelled product, category
- The most returned product, category
  
6. Customer profile
- customer location
- age
- gender
- average spend
- CLV, RMF




## 4. Recommendation
