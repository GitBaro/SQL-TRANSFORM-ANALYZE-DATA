Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

```
SELECT "Country",
	SUM("TransactionRevenue"::INTEGER) AS TransactionRev,
	SUM("TotalTransactionRevenue"::INTEGER) AS TotalTransactionRev
FROM "All_Sessions"
GROUP BY  "Country"
ORDER BY  TransactionRev, TotalTransactionRev DESC NULLS LAST
LIMIT 5

SELECT "City",
	SUM("TransactionRevenue"::INTEGER) AS TransactionRev,
	SUM("TotalTransactionRevenue"::INTEGER) AS TotalTransactionRev
FROM "All_Sessions"
GROUP BY  "City"
ORDER BY  TransactionRev, TotalTransactionRev DESC NULLS LAST
LIMIT 5

```

Answer: Countries with the top 5 highest level of transaction revenues are:
| Country  | City |
| ---------|:-------------:|
| United States | Sunnyvale |
|     Israel    |   Other   |
| Australia    |San Francisco    |
| Canada   | Atlanta    |
| Switzerland    | Palo Alto    |





**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

```
SELECT AVG("Total_Ordered") AS AvgOrdered,
	"Country"
FROM "Sales_Report"
JOIN "All_Sessions" USING("ProductSKU")
GROUP BY "Country"
ORDER BY AvgOrdered DESC NULLS LAST

SELECT AVG("Total_Ordered") AS AvgOrdered,
	"City"
FROM "Sales_Report"
JOIN "All_Sessions" USING("ProductSKU")
GROUP BY "City"
ORDER BY AvgOrdered DESC NULLS LAST
```

Answer: Top 5

| Country  | AvgOrdered |
| ------------- |:-------------:|
| Saudi Arabia      | 96.29    |
| Kuwait      | 85.75    |
| Oman     | 85    |
| Ethiopia      | 85   |
| Laos      | 85    |


| City  | AvgOrdered |
| ------------- |:-------------:|
| Riyadh   | 319    |
| Brno     | 319    |
| Rexburg     | 250    |
| Sacramento     | 189    |
| Lisbon     | 189 |



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







