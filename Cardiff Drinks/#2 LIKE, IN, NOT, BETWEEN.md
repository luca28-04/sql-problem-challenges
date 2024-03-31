# CARDIFF DRINKS - SQL LIKE, IN, NOT, BETWEEN



# Question and Solutions

1. From the clients table, find name, flagship_poc and salesperson for Apple, Sunny RealEstate Investments, and SanDisk. Give two alternative options: only using LIKE andonly using IN
  
```sql
SELECT c.name, c.flagship_poc, s.name
FROM clients AS c, salespersons AS s
WHERE c.name IN ('Apple', 'Sunny Real Estate Investments', 'SanDisk');
```
Output:

| name    | flagship_poc    | name                |
|---------|-----------------|---------------------|
| SanDisk | Barbara Hoffman | Wilma Erdmann       |
| SanDisk | Barbara Hoffman | Sarah Heilman       |
...

---
2. 	List all enterprise names that start with 'A'.
```sql
SELECT name AS Enterprise FROM clients
WHERE NAME LIKE 'A%' LIMIT 10;
```
Output:
| Enterprise            |
|-----------------------|
| Advance_Auto_Parts    |
| Anixter_International |
...

---

3. List all enterprise names that end with 'X'.

```sql
SELECT name AS Enterprise FROM clients
WHERE name LIKE '%x';
```
Output:
| Enterprise         |
|--------------------|
| STX                |
| Publix             |
...


---
4. Retrieve all companies whose name has the string 'tech' somewhere in the name.
SELECT name AS “Company Name” FROM clients
```sql
SELECT name AS “Company Name” FROM clients
WHERE name LIKE ‘%tech%’
```
Output:
| Company Name                        |
|-------------------------------------|
| Multi_Tech_Development              |
| Mikrotechnic                        |
| Alliant_Techsystems                 |
...


---
5. Let's explore the online activity. Get all the info for those people who were contactedvia online coupons and youtube ads. Make sure to present the latest contacts first, andthen sort alphabetically by platform.

```sql
SELECT * FROM online_activity
WHERE platform = ‘online_coupon’ OR platform = ‘youtube_ad’
ORDER BY activity_date DESC, platform ASC; 
```

Output:
| activity_id | client_id | activity_date       | platform      |
|-------------|-----------|---------------------|---------------|
| 7271        | 3001      | 2017-01-01 23:51:09 | youtube_ad    |
| 8167        | 3841      | 2017-01-01 13:12:29 | online_coupon |
| 5828        | 1961      | 2017-01-01 09:31:44 | online_coupon |
| 5318        | 1681      | 2017-01-01 08:45:40 | youtube_ad    |
---

6. From the clients table, retrieve the following information: Client name, flagship pocand salesperson id for all stores except Fluor Corp., Xerox and Duke Energy

```sql
SELECT salesperson_id, name, flagship_poc FROM clients
WHERE name NOT IN (‘Fluor Corp.’, ‘Xerox’, ‘Duke Energy’);
```


Output:

| salesperson_id | name                        | flagship_poc        |
|----------------|-----------------------------|---------------------|
| 321500         | Quality_Merchant_Services   | Christopher Shanley |
| 321510         | Earthworks_Yard_Maintenance | Myra Hobbs          |
| 321520         | Baldor_Electric_Company     | James Esquivez      |
| 321530         | Advance_Auto_Parts          | Lois Putman         |
---

7. Retrieve all information available for the remaining of the clients listed in the previous exercise.

```sql
SELECT client_id, name, website, flagship_poc, salesperson_id
WHERE name IN (‘Fluor Corp.’, ‘Xerox’, ‘Duke Energy’);
```

Output:
| client_id | name  | website       | flagship_poc    | salesperson_id |
|-----------|-------|---------------|-----------------|----------------|
| 3941      | Xerox | www.xerox.com | Barry Nasworthy | 321940         |

---
8. List all business names not starting with 'F'.

Output:
| name                        |
|-----------------------------|
| Quality_Merchant_Services   |
| Earthworks_Yard_Maintenance |
| Baldor_Electric_Company     |
...
---

9. List all business names not containing 'earth' in their name.

```sql
SELECT name FROM clients
WHERE name NOT LIKE ‘%earth%’ LIMIT 10;
SELECT name FROM clients
WHERE name NOT LIKE ‘f%’;
```

Output:
| name                        |
|-----------------------------|
| Quality_Merchant_Services   |
| Baldor_Electric_Company     |
| Advance_Auto_Parts          |
| Hi-Point_Firearms           |
| Butler_America              |


---

10. List all information of business whose last letter is not 'E'.

```sql
SELECT * FROM clients
WHERE name NOT LIKE ‘%E’;
```


Output:

| client_id | name                       | website                            | flagship_poc        | salesperson_id |
|-----------|----------------------------|------------------------------------|---------------------|----------------|
| 1001      | Quality_Merchant_Services  | www.quality-merchant-services.com  | Christopher Shanley | 321500         |
| 1021      | Baldor_Electric_Company    | www.baldor-electric-company.com    | James Esquivez      | 321520         |
...


---

11. Define a select query to obtain all the placed orders where the soda_qty is above 500,the juice_qty is 0, and not a lot of wine was ordered.

```sql
SELECT * FROM placed_orders
WHERE soda_qty > 500 AND juice_qty = 0 AND wine_qty <= 50;
```

Output:
| order_id | client_id | order_date          | soda_qty | wine_qty | juice_qty | total | soda_gbp | wine_gbp | juice_gbp | total_gbp |
|----------|-----------|---------------------|----------|----------|-----------|-------|----------|----------|-----------|-----------|
| 17       | 1011      | 2016-12-21 10:59:34 | 527      | 14       | 


---
12. From the clients table find all the companies with names not starting with 'S' and with'z'. Which company are we leaving out with the first WHERE?

```sql
SELECT name AS “Company Name” FROM clients
WHERE name NOT LIKE ‘s%z’
```
Output:

| Company Name                |
|-----------------------------|
| Quality_Merchant_Services   |
| Earthworks_Yard_Maintenance |
| Baldor_Electric_Company     |
| Advance_Auto_Parts          |
| Hi-Point_Firearms           |
| Butler_America              |

The company being left out is Starz:
+--------------+
| Company Name |
+--------------+
| Starz        |


---

13. We need information of people who were contacted via youtube ads or online coupons
and who became clients in 2016. Sort from newest to oldest. Explain your decision forthe date filter (i.e., when does a year start and end in mysql?).

```sql
SELECT * FROM online_activity
WHERE platform=’youtube_ad’ OR platform=’online_coupon’ AND activity_date = 2016
ORDER BY activity_date ASC; 
```
Output:

| activity_id | client_id | activity_date       | platform   |
|-------------|-----------|---------------------|------------|
| 7587        | 3251      | 2013-12-06 07:52:09 | youtube_ad |
| 7465        | 3141      | 2013-12-09 05:28:27 | youtube_ad |
| 5523        | 1791      | 2013-12-09 19:17:50 | youtube_ad |
| 8871        | 4341      | 2013-12-10 09:26:27 | youtube_ad |
...

---

14. We only need a list of ids of placed orders. Specifically, those where either the numberof wine or juice bottles was above 4k.

```sql
SELECT order_id FROM placed_orders
WHERE wine_qty > 4000 OR juice_qty > 4000;
```
Output:
| order_id |
|----------|
| 362      |
| 731      |
| 1191     |
| 1913     |
...
---


15. Same as above, but this time only those where no soda was purchased, and either ofthe other two drinks were above 1000 each.

```sql
SELECT order_id FROM placed_orders
WHERE soda_qty = 0 AND wine_qty > 1000 OR juice_qty > 1000;
```

Output:

| order_id |
|----------|
| 129      |
| 234      |
| 362      |
| 1080     |
| 1191     |
| 1268     |
...


---

16. Let's pull out orders dominated by wine. I.e., those orders which, by including wine(because it was the largest order), amounted to an overall of more than 1000 bottles.

```sql
SELECT order_id, soda_qty, wine_qty, juice_qty, total FROM placed_orders
WHERE total > 1000 AND wine_qty > soda_qty AND wine_qty > juice_qty;
```
Output:
| order_id | soda_qty | wine_qty | juice_qty | total |
|----------|----------|----------|-----------|-------|
| 214      | 485      | 1345     | 21        | 1851  |
| 458      | 340      | 918      | 14        | 1272  |
| 731      | 555      | 12012    | 31        | 12598 |
| 873      | 118      | 1467     | 35        | 1620  |
| 897      | 486      | 605      | 11        | 1102  |
| 1113     | 497      | 646      | 1         | 1144  |
...


---
17. Pull out those business names starting with an 'A' or 'B', and the flagship poc contains'jess' or 'stev', but it doesn't contain 'stevenson'. Which row are leaving out?

```sql
SELECT name AS “Company Name”, flagship_poc FROM clients
WHERE name LIKE ‘ab%’ AND flagship_poc NOT LIKE ‘%stevenson%’ AND flagship_poc LIKE ‘%jess%’ AND flagship_poc LIKE ‘%stev%’;
```

Output:
| Company Name                    | flagship_poc     |
|---------------------------------|------------------|
| Anixter_International           | Steven Pierre    |
| Analog_Devices                  | Sandra Stevenson |
| Martha_Stewart_Living_Omnimedia | Steven Mattson   |
| Bank_of_New_York_Mellon         | Steven Mcdowell  |
...

---










