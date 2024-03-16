# CARDIFF DRINKS - SQL BASICS



# Question and Solutions

1. Pull out the 10 earliest orders. The output table should include order_id, order_date, and total_gbp.

```
SELECT order_id, order_date, total_gbp
FROM placed_orders
ORDER BY order_date
LIMIT 10;
```

