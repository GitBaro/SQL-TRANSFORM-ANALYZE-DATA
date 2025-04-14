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

```
SELECT "V2ProductCategory",
	COUNT("V2ProductCategory") AS CategoryQuant,
	"Country"
FROM "All_Sessions"
WHERE "VisitID" IS NOT NULL
GROUP BY "Country", "V2ProductCategory"
ORDER BY CategoryQuant DESC

SELECT "V2ProductCategory",
	COUNT("V2ProductCategory") AS CategoryQuant,
	"City"
FROM "All_Sessions"
WHERE "VisitID" IS NOT NULL
GROUP BY "City", "V2ProductCategory"
ORDER BY CategoryQuant DESC
```

Answer:
- Visitors in the United States dominate in how much quantity they buy in most categories, especially in apparel and shop by brand categories. The next closest countries are India and the United Kingdom for shop by brand and apparel categories.
- Visitors in Cities in the 'Other' section, which are the most dominant city ranges, mostly buy apparel, shop by brand, and electronic materials. Mountain View city then has the most with visitors buying apparel
- Visitors to different placed typically like to buy apparel and clothing, most likely as souvenirs/things to wear as memorabelia for the location



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







