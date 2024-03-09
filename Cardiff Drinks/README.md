# ☕ #1: CARDIFF DRINKS

# Table of Contents
  - Description
  - Entity Relationship Diagram
  - Questions and Solutions
#

# Description
Cardiff Drinks is a fictitious company that sells fizzy drinks, juice and wine, to customers all
over the world. The database schema and problem questions are from my univeristy module Manipulating and Exploiting Data. 
All solutions were completed by me.  

# ERD
<img width="452" alt="cardiff_drinks_erd" src="https://github.com/luca28-04/SQL-PROBLEM-CHALLENGES/assets/109167297/9f9dbd35-6d9f-478e-a7c3-1a429bb86b8d">


# Question and Solution

1. Pull out the 10 earliest orders. The output table should include order_id, order_date, and total_gbp.

```
SELECT order_id, order_date, total_gbp
FROM placed_orders
ORDER BY order_date
LIMIT 10;
```

