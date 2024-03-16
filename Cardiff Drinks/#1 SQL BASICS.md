# CARDIFF DRINKS - SQL BASICS



# Question and Solutions

1. Pull out the 10 earliest orders. The output table should include order_id, order_date, and total_gbp.

```sql
SELECT order_id, order_date, total_gbp
FROM placed_orders
ORDER BY order_date
LIMIT 10;
```
Output:
| order_id | order_date          | total_gbp |
|----------|---------------------|-----------|
| 5786     | 2013-12-04 04:22:44 | 627.48    |
| 2415     | 2013-12-04 04:45:54 | 2646.77   |
| 4108     | 2013-12-04 04:53:25 | 2709.62   |
| 4489     | 2013-12-05 20:29:16 | 277.13    |
| 287      | 2013-12-05 20:33:56 | 3001.85   |
| 1946     | 2013-12-06 02:13:20 | 2802.90   |
| 6197     | 2013-12-06 12:55:22 | 7009.18   |
| 3122     | 2013-12-06 12:57:41 | 1992.13   |
| 6078     | 2013-12-06 13:14:47 | 6680.06   |
| 2932     | 2013-12-06 13:17:25 | 2075.94   |

---

2. Write a query to retrieve the top 5 orders in terms of largest total_gbp. Include the order_id, client_id, and total_gbp.

```sql
SELECT order_id, client_id, total_gbp FROM placed_orders
ORDER BY total_gbp DESC LIMIT 5;
```
Output:
| order_id | client_id | total_gbp |
|----------|-----------|-----------|
| 4016     | 4251      | 232207.07 |
| 3892     | 4161      | 112875.18 |
| 3963     | 4211      | 107533.55 |
| 5791     | 2861      | 95005.82  |
| 3778     | 4101      | 93547.84  |

---

3.	Write a query to return the bottom 20 orders in terms of least total. Include the order_id, client_id, and total_gbp.

```sql
SELECT order_id, client_id, total_gbp, total FROM placed_orders
ORDER BY total DESC;

```

Output:
| order_id | client_id | total_gbp | total |
|----------|-----------|-----------|-------|
| 5001     | 1791      | 0.00      | 0     |
| 5612     | 2601      | 0.00      | 0     |
| 5057     | 1851      | 0.00      | 0     |
| ...      | ...       | ...       | ...   |  # Truncated
| 6375     | 3651      | 0.00      | 0     |

---

4.	Get the full rows of the five newest orders

```sql
SELECT * FROM placed_orders
ORDER BY order_date ASC;
```

Output:
| order_id | client_id | order_date          | soda_qty | wine_qty | juice_qty | total | soda_gbp | wine_gbp | juice_gbp | total_gbp |
|----------|-----------|---------------------|----------|----------|-----------|-------|----------|----------|-----------|-----------|
| 5786     | 2861      | 2013-12-04 04:22:44 | 0        | 48       | 33        | 81    | 0.00     | 359.52   | 267.96    | 627.48    |
| 2415     | 2861      | 2013-12-04 04:45:54 | 490      | 15       | 11        | 516   | 2445.10  | 112.35   | 89.32     | 2646.77   |
| ...      | ...       | ...                 | ...      | ...      | ...       | ...   | ...      | ...      | ...       | ...       | # Truncated 

---

5.	Get the full rows of the five oldest orders

```sql
SELECT * FROM placed_orders
ORDER BY order_date DESC

```
Output:
| order_id | client_id | order_date          | soda_qty | wine_qty | juice_qty | total | soda_gbp | wine_gbp | juice_gbp | total_gbp |
|----------|-----------|---------------------|----------|----------|-----------|-------|----------|----------|-----------|-----------|
| 6451     | 3841      | 2017-01-02 00:02:40 | 42       | 506      | 302       | 850   | 209.58   | 3789.94  | 2452.24   | 6451.76   |
| ...      | ...       | ...                 | ...      | ...      | ...       | ...   | ...      | ...      | ...       | ...       |  # Truncated

---

6. Select the 5 first rows and all their columns from the placed_orders table that have anamount of wine_gbp greater than or equal to 1000.

```sql
SELECT salesperson_id, name, flagship_poc FROM clients
WHERE name NOT IN (‘Fluor Corp.’, ‘Xerox’, ‘Duke Energy’) 
```

| order_id | client_id | order_date          | soda_qty | wine_qty | juice_qty | total | soda_gbp | wine_gbp | juice_gbp | total_gbp |
|----------|-----------|---------------------|----------|----------|-----------|-------|----------|----------|-----------|-----------|
| 5786     | 2861      | 2013-12-04 04:22:44 | 0        | 48       | 33        | 81    | 0.00     | 359.52   | 267.96    | 627.48    |
| 2415     | 2861      | 2013-12-04 04:45:54 | 490      | 15       | 11        | 516   | 2445.10  | 112.35   | 89.32     | 2646.77   |
| ...      | ...       | ...                 | ...      | ...      | ...       | ...   | ...      | ...      | ...       | ...       |  # Truncated

---
7.	Pull the first 10 rows and all their columns from placed_orders that have a total_gbpless than 500.

```sql
SELECT * FROM placed_orders
WHERE total_gbp < 500
ORDER BY total_gbp ASC LIMIT 10;
```
   
| order_id | client_id | order_date          | soda_qty | wine_qty | juice_qty | total | soda_gbp | wine_gbp | juice_gbp | total_gbp |
|----------|-----------|---------------------|----------|----------|-----------|-------|----------|----------|-----------|-----------|
| 5786     | 2861      | 2013-12-04 04:22:44 | 0        | 48       | 33        | 81    | 0.00     | 359.52   | 267.96    | 627.48    |
| 2415     | 2861      | 2013-12-04 04:45:54 | 490      | 15       | 11        | 516   | 2445.10  | 112.35   | 89.32     | 2646.77   |
| ...      | ...       | ...                 | ...      | ...      | ...       | ...   | ...      | ...      | ...       | ...       |  # Truncated

---

8.	Filter the clients table to include the company name, website and the flagship person of contact (flagship_poc) for 'Kellogg_Company'

```sql
SELECT name, website, flagship_poc FROM clients
WHERE name = ‘Kellogg_Company’;
```

| name            | website                 | flagship_poc  |
|-----------------|-------------------------|---------------|
| Kellogg_Company | www.kellogg-company.com | Angel Pittman |


---

9.	Create a column that divides the juice_gbp amount by the juice_qty to find the unitprice for juice bottles for each order. Don't show more than 10 orders, complement theinfo with order id and client_id. Anything unexpected?

```sql
SELECT order_id, client_id juice_gbp / juice_qty AS unit_price
FROM placed_orders;
```

| order_id | client_id | unit_price |
|----------|-----------|------------|
| 1        | 1001      | 8.12       |
| 2        | 1001      | 8.12       |
| 3        | 1001      | NULL       |
| ...      | ...       | ...        |  # Truncated

---

10.	What is the percentage of juice bottles purchased in each order? Your query shouldreturn order_id, client_id and juice_bottle_percent.

```sql
SELECT order_id, client_id, juice_qty / (soda_qty + wine_qty + juice_qty) * 100 
FROM placed_orders
```
| order_id | client_id | juice_bottle_percent |
|----------|-----------|----------------------|
| 1        | 1001      | 14.2012              |
| 2        | 1001      | 19.7917              |
| ...      | ...       | ...                  |  # Truncated 




