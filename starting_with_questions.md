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
- Visitors to site typically like to buy the apparel there, it seems apparel categories are of the highest sellers




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

```
SELECT "Name",
	SUM("Total_Ordered") AS ProductSales,
	"Country"
FROM "Sales_Report" sr
JOIN "All_Sessions" al USING("ProductSKU")
GROUP BY "Country", "Name"
ORDER BY ProductSales DESC NULLS LAST

SELECT "Name",
	SUM("Total_Ordered") AS ProductSales,
	"City"
FROM "Sales_Report" sr
JOIN "All_Sessions" al USING("ProductSKU")
GROUP BY "City", "Name"
ORDER BY ProductSales DESC NULLS LAST
```

Answer:

| Country  | Product |
| ------------- |:-------------:|
| United States   | 17oz Stainless Steel Sport Bottle    |
| United Kingdom     | Hard Cover Journal    |
|  Germany | Ballpoint LED Light Pen     |
| Canada   | 17oz Stainless Steel Sport Bottle    |
| Italy  | Leatherette Journal    |

- It seems as though western countries such as the United States and Canada buy more sports activity related products, while European countries (United Kingdom, Germany, Italy) buy more things related too writing and books

| City  | Product |
| ------------- |:-------------:|
| Other   | 17oz Stainless Steel Sport Bottle    |
| Mountain View     | Cam Indoor Security Camera - USA    |
|  Los Angeles | 17oz Stainless Steel Sport Bottle     |
| San Francisco   | Android 17oz Stainless Steel Sport Bottle   |
| Palo Alto  | 17oz Stainless Steel Sport Bottle   |

- United States cities buy sports bottle products a lot, perhaps the most



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

```
WITH CountryRevenue AS
(
SELECT SUM("ProductPrice"::Integer * "Total_Ordered") AS Revenue,
	"Country" AS Country
FROM "All_Sessions"
JOIN "Sales_Report" USING("ProductSKU")
GROUP BY "Country"),

TotalRevenue AS
(SELECT SUM(Revenue) AS Total
FROM CountryRevenue)

SELECT
	cr.Country,
	Total,
	cr.Revenue / Total * 100 AS RevPct
FROM CountryRevenue cr
JOIN TotalRevenue tr ON true
WHERE Revenue > 0
Order By RevPct desc


WITH CityRevenue AS
(
SELECT SUM("ProductPrice"::Integer * "Total_Ordered") AS Revenue,
	"City" AS City
FROM "All_Sessions"
JOIN "Sales_Report" USING("ProductSKU")
GROUP BY "City"),

TotalRevenue AS
(SELECT SUM(Revenue) AS Total
FROM CityRevenue)

SELECT
	cr.City,
	Total,
	cr.Revenue / Total * 100 AS RevPct
FROM CityRevenue cr
JOIN TotalRevenue tr ON true
WHERE Revenue > 0
Order By RevPct desc
```


Answer:

| Country  | RevPct |
| ------------- |:-------------:|
| United States     | 77.9    |
| United Kingdom    | 3.68    |
| Canada    | 2.43  |
| India    | 1.74   |
| Italy     | 1.39    |

- The United States has a vastly superior impact of revenue of all the countries, being almost 78% of the total revenue produced.



| City  | RevPct |
| ------------- |:-------------:|
| Other    | 37.68    |
| Mountain View    | 18.31    |
| San Francisco    | 5.52  |
| Sunnyvale    | 5.15   |
| Palo Alto     | 4.8    |

- Most of the total revenue is produced by inspecified/uknown/uncategorized cities. Of the defined cities, the revenue mostly comes from United States cities (Mountain View, San Francisco, Sunnyvale, Palo Alto)



