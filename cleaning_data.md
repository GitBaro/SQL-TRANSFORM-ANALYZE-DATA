# What issues will you address by cleaning the data?
## Date/Time Issues
- Changed Date Columns of All_Sessions and Analytics tables to proper "YYYY-MM-DD" Format

## Null Value Issues

## Country/Location Issues

## MISC Issues
- Updated Unit Cost in Analytics Table to be divided by 1,000,000

# Queries:

Below, provide the SQL queries you used to clean your data.

## Date/Time

- Changed date format for All_Sessions and Analytics

```
Update "All_Sessions"
SET "Date" = "Date"::date

Update "Analytics"
SET "Date" = "Date"::date
```

- Changed Unit Cost and Product Price in Analytics and All_Sessions Tables to be divided by 1,000,000

```
UPDATE "Analytics"
SET "Unit_Price" = CAST("Unit_Price" as Integer) / 1000000

UPDATE "All_Sessions"
SET "ProductPrice" = CAST("ProductPrice" as Integer) / 1000000
```

## Null Value Issues
- Changed all null integer/numeric values in all Tables to be 0, and changed all null string values to be 'None'

```
SELECT Coalesce("TotalTransactionRevenue"::Integer, 0) AS TotalTransactionRevenue,
	Coalesce("Transactions"::Integer, 0) AS Transactions,
	Coalesce("SessionQualityDim"::Integer, 0) AS SessionQualityDim,
	Coalesce("ProductRefundAmount"::Integer, 0) AS ProductRefundAmount,
	Coalesce("ProductQuantity"::Integer, 0) AS ProductQuantity,
	Coalesce("ItemQuantity"::Integer, 0) AS ItemQuantity,
	Coalesce("ItemRevenue"::Integer, 0) AS ItemRevenue,
	Coalesce("TransactionRevenue"::Integer, 0) AS TransactionRevenue
FROM "All_Sessions"

SELECT Coalesce("SearchKeyword", 'None') AS SearchKeyword,	
	Coalesce("TransactionID", 'None') AS TransactionID,
	Coalesce("ECommerceAction_Option", 'None') AS ECommerceAction_Option
FROM "All_Sessions"

SELECT Coalesce("UserID"::Integer, 0) AS UserID,
	Coalesce("Units_Sold"::Integer, 0) AS Units_Sold,
	Coalesce("TimeOnSite"::Integer, 0) AS TimeOnSite,
	Coalesce("Revenue"::Integer, 0) AS Revenue
FROM "Analytics"

SELECT Coalesce("SentimentScore", 0) AS SentimentScore,
	Coalesce("SentimentMagnitude", 0) AS SentimentMagnitude
FROM "Products"


```

# Country/Location

- Changed to "Other" where City, Country and V2ProductCategory were "not available in demo dataset" and "(not set)"

```
UPDATE "All_Sessions"
SET "City" = 'Other'
WHERE "City" = 'not available in demo dataset'

UPDATE "All_Sessions"
SET "Country" = 'Other'
WHERE "Country" = 'not available in demo dataset'

UPDATE "All_Sessions"
SET "City" = 'Other'
WHERE "City" = '(not set)'

UPDATE "All_Sessions"
SET "Country" = 'Other'
WHERE "Country" = '(not set)'

UPDATE "All_Sessions"
SET "V2ProductCategory" = 'Other'
WHERE "V2ProductCategory" = '(not set)'
```
