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
SELECT AVG("ProductQuantity"::Integer) AS AvgQuantity,
	"Country"
FROM "All_Sessions"
GROUP BY "Country"
ORDER BY AvgQuantity Desc NULLS LAST

SELECT AVG("ProductQuantity"::INteger) AS AvgQuantity,
	"City"
FROM "All_Sessions"
GROUP BY "City"
ORDER BY AvgQuantity Desc NULLS LAST
```

Answer:

| Country  | AvgQuantity |
| ------------- |:-------------:|
| Spain      | 10    |
| United States      | 4.02    |

- The following countries are tied for next most average at 1: India, France, Argentina, Mexico, Ireland, Finland, Colombia, Canada

| City  | AvgQuantity |
| ------------- |:-------------:|
| Madrid      | 10    |
| Salem     | 8    |
| Other     | 6.48    |
| Atlanta     | 4    |
| Houston     | 2 |
| New York     | 1.17    |

- The following countries are tied for next most average at 1: Seattle, Detroit, San Franciscom, Los Angeles, Bengaluru, Ann Arbor, Columbus, Sunnyvale, Dallas, Chicago, San Jose, Dublin, Palo Alto, Mountain View


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







