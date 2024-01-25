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
