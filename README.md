# Question 1
## Sales Table

| Column Name | Type    |
|-------------|---------|
| sale_id     | int     |
| product_id  | int     |
| year        | int     |
| quantity    | int     |
| price       | int     |

- (sale_id, year) is the primary key (combination of columns with unique values) of this table.
- product_id is a foreign key (reference column) to Product table.
- Each row of this table shows a sale on the product product_id in a certain year.
- Note that the price is per unit.

## Product Table

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

- product_id is the primary key (column with unique values) of this table.
- Each row of this table indicates the product name of each product.

## Solution

```sql
SELECT p.product_name, s.year, s.price
FROM Sales s
JOIN Product p ON s.product_id = p.product_id;
```

# Question 2
### Problem Statement

A Microsoft Azure Supercloud customer is defined as a company that purchases at least one product from each product category.

Write a SQL query that effectively identifies the company ID of such Supercloud customers.

### Given Data

#### `customer_contracts` Table:

| Column Name | Type    |
|-------------|---------|
| customer_id | integer |
| product_id  | integer |
| amount      | integer |

**Example Input:**

| customer_id | product_id | amount |
|-------------|------------|--------|
| 1           | 1          | 1000   |
| 1           | 3          | 2000   |
| 1           | 5          | 1500   |
| 2           | 2          | 3000   |
| 2           | 6          | 2000   |

#### `products` Table:

| Column Name    | Type    |
|----------------|---------|
| product_id     | integer |
| product_category | string |
| product_name   | string  |

**Example Input:**

| product_id | product_category | product_name          |
|------------|------------------|-----------------------|
| 1          | Analytics        | Azure Databricks      |
| 2          | Analytics        | Azure Stream Analytics|
| 4          | Containers       | Azure Kubernetes Service |
| 5          | Containers       | Azure Service Fabric  |
| 6          | Compute          | Virtual Machines      |
| 7          | Compute          | Azure Functions       |

### Expected Output

The SQL query should return the company IDs of Microsoft Azure Supercloud customers.

### Additional Notes

- The solution should identify customers who have purchased at least one product from each product category.
- The data in the `customer_contracts` and `products` tables were last updated as of 5 Dec 2022.

# Solution
-- Calculate the count of unique product categories purchased by each customer
```sql
WITH Supercloud AS (
    SELECT 
        customers.customer_id, 
        COUNT(DISTINCT products.product_category) AS unique_count
    FROM 
        customer_contracts AS customers
    LEFT JOIN 
        products ON customers.product_id = products.product_id
    GROUP BY 
        customers.customer_id
)
-- Retrieve the customer IDs of Microsoft Azure Supercloud customers
SELECT 
    customer_id 
FROM 
    Supercloud 
WHERE 
    unique_count = 3;
```
