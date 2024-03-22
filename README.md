# theLook CRM Project
```
├── Image                       
│
├── Code_A_B_test.ipynb                               <- code
├── README.md                                         <- read me
├── ab_test_results_aggregated_views_clicks_2.csv     <- dataset

```
## 1. Summary

## 2. Introduction
TheLook is a fictitious eCommerce clothing site developed by the Looker team. The dataset contains information about customers, products, orders, logistics, and web events. 

- Data source: https://console.cloud.google.com/marketplace/product/bigquery-public-data/thelook-ecommerce?hl=en&project=causal-flame-283208
- ER Diagram
<p align="center" width="100%">
    <img width="60%" src="https://github.com/Taweilo/theLook_CRM/blob/main/Image/theLook_ERD.jpg">
</p>

- Entity & Column
  
| Table Name           | Columns                                                                                                                                                                        |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| users                | id, first_name, last_name, email, age, gender, state, street_address, postal_code, city, country, latitude, longitude, traffic_source, created_at                            |
| order_items          | id, order_id, user_id, product_id, inventory_item_id, status, created_at, shipped_at, delivered_at, returned_at, sale_price                                                    |
| distribution_centers | id, name, latitude, longitude                                                                                                                                                   |
| inventory_items      | id, product_id, created_at, sold_at, cost, product_category, product_name, product_brand, product_retail_price, product_department, product_sku, product_distribution_center_id |
| products             | id, cost, category, name, brand, retail_price, department, sku, distribution_center_id                                                                                          |
| orders               | order_id, user_id, status, gender, created_at, returned_at, shipped_at, delivered_at, num_of_item                                                                               |
| events               | id, user_id, sequence_number, session_id, created_at, ip_address, city, state, postal_code, browser, traffic_source, uri, event_type                                         |


## 2. Objective
The goal is to utilize SQL queries to delve into the dataset and extract valuable insights that can enhance business performance for Adidas. This includes areas such as sales optimization, marketing effectiveness, and supply chain management efficiency.

## 3. Analysis
1. Overall KPI
   
| Brand         | Total Revenue | Total Cost | Gross Profit | Market Share (%) |
|---------------|---------------|------------|--------------|------------------|
| Adidas        | 1623.87       | 682.8      | 941.07       | 29%              |
| New Balance   | 50.25         | 26.96      | 23.29        | 1%               |
| Nike          | 1820.58       | 879.08     | 941.5        | 32%              |
| Puma          | 782.01        | 346.22     | 435.79       | 14%              |
| Reebok        | 361           | 156.98     | 204.02       | 6%               |
| Under Armour  | 1057.31       | 475.51     | 581.8        | 19%              |

Total overall revenue: 5695.02

2. Sales trends
3. Product performance
4. Customer profile
5. Delivery efficiency
6.  New customer's preference

## 4. Recommendation
