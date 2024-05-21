```sql
SELECT * FROM sql_store.orders;
select first_name, last_name, points+10 from customers;

select name, unit_price , unit_price * 1.1 as new_price from products;

SELECT * FROM customers WHERE last_name REGEXP 'field|mac|rose';
-- ^ -- beginning of regexp
-- $ -- end of regexp
-- 'field|mac' -- list of string 
-- '[gim]e' - ge, ie, me
-- '[a-h]e' - a to f
select * from customers;
SELECT * from customers where first_name REGEXP 'elka|ambur';
select * from customers where last_name REGEXP '^my|se';

select * from customers LIMIT 6, 3; -- 6 offset skip first 6 records then show 3
-- page 1: 1-3
-- page 2: 4-6
-- page 3: 7-9
select * from customers order by points desc limit 3;
```

## JOINS
1. Inner Join (Join)
2. Outer Join

Composite primary key - contains more than one column.

Compound Join
```sql
select * from order_items oi
join order_item_notes oin
on oi.order_id = oin.order_id and oi.product_id = oin.product_id;
```



OUTER JOIN
1. LEFT JOIN 
2. RIGHT JOIN


```sql
SELECT 
    o.order_id, c.first_name
FROM
    orders o
        JOIN
    customers c -- ON o.customer_id = c.customer_id;
    using (customer_id) -- if join columns have same name then we can use using clause
```


NATURAL JOIN - SQL will do join based on the same column name.
CROSS JOIN - every record from first table join every record from second table
```sql
SELECT 
    c.first_name AS customer, p.name AS product
FROM
    customers c
        CROSS JOIN
    products p
ORDER BY c.first_name;
```

UNION - combine results from multiple queries can be of same table or different tables.
but no. of columns that each query return must be same.

Name of the column will be based on the first_query


Copy a table 

```sql
-- create
CREATE TABLE orders_archived AS
SELECT * FROM orders;

-- insert 
INSERT INTO orders_archived
SELECT * FROM orders;
```

## Aggregate Functions


MAX()
MIN()
AVG()
SUM()
COUNT()

```SQL
SELECT 
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(invoice_total) AS number_of_invoices,
    COUNT(DISTINCT client_id) AS total_clients
FROM
    invoices;
```

## GROUP BY 
```SQL
SELECT 
    client_id, SUM(invoice_total) AS total_sales
FROM
    invoices
GROUP BY client_id
ORDER BY total_sales DESC;


SELECT 
    state, city, SUM(invoice_total) AS total_sales
FROM
    invoices i
JOIN clients c USING (client_id) 
GROUP BY state, city;
```

## HAVING 

To filter data after group by and only include columns present in SELECT clause.

```SQL
SELECT 
    client_id,
    SUM(invoice_total) AS total_sales,
    COUNT(*) AS number_of_invoices
FROM
    invoices
GROUP BY client_id
HAVING total_sales > 500
    AND number_of_invoices > 5;
```

RULE if you aggregate function in your select clause you should group by all the columns present in select clause.

```SQL
--ROLLUP to summarize data
SELECT 
    client_id, SUM(invoice_total) AS total_sales
FROM
    invoices
GROUP BY client_id WITH ROLLUP;
```
