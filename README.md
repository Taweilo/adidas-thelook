# theLook CRM

## 1. Summary

## 2. Introduction
Data: https://console.cloud.google.com/marketplace/product/bigquery-public-data/thelook-ecommerce?hl=en&project=causal-flame-283208
## 2. Objective

## 3. Analysis
1. Ask overall performance
   
```SELECT ROUND(SUM(t2.sale_price),2) AS total_revenue
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
AND status NOT IN ('Cancelled', 'Return')
AND brand IN ('Adidas', 'Nike', 'Puma', 'Under Armour','Reebok','New Balance') ; ```


3. 




## 4. Recommendation
