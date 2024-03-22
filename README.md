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
   
<p align="center" width="100%">
    <img width="60%" src="https://github.com/Taweilo/theLook_CRM/blob/main/Image/2.%20Sales%20Trend.jpg">
</p>

<p align="center" width="100%">
| Time   | Total Revenue | Total Cost | Gross Profit |
|--------|---------------|------------|--------------|
| 2023-01| 653.74        | 281.38     | 372.36       |
| 2023-02| 453.73        | 206.91     | 246.82       |
| 2023-03| 390.11        | 163.15     | 226.96       |
| 2023-04| 440.15        | 181.56     | 258.59       |
| 2023-05| 867.98        | 421.19     | 446.79       |
| 2023-06| 598.77        | 263.04     | 335.73       |
| 2023-07| 817.9         | 360.38     | 457.52       |
| 2023-08| 691.95        | 293.02     | 398.93       |
| 2023-09| 348.8         | 170.47     | 178.33       |
| 2023-10| 1276.68       | 605.4      | 671.28       |
| 2023-11| 839.52        | 361.42     | 478.1        |
| 2023-12| 1952.84       | 865.8      | 1087.04      |
| 2024-01| 1623.87       | 682.8      | 941.07       |
</p>


4. Product performance
5. Customer profile
6. Delivery efficiency
7.  New customer's preference

## 4. Recommendation
