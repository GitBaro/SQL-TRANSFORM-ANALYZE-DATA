What are your risk areas? Identify and describe them.

- Visitor IDs Columns, There are no Tables with Distinct FullVisitorIDs to use as a Key. The FullVisitorIDs are only found in the Analytics and All_Sessions tables and they each have duplicates and overlaps, which makes it difficult to work with distinct website visitors.
- Date information not being in the proper format, just being stored as numbers with no proper formatting.
- Missing or undocumented cities, countries information.


# QA Process:
Describe your QA process and include the SQL queries used to execute it.

## 1. Profiling 


- Checking the DataType of the Columns, the result is character varying


```
SELECT *
FROM "Analytics"

SELECT *
FROM "All_Sessions"
```


- Checking DataType of Date columns in 
## 2. Validation

- Checking for missing and duplicate data in each table

```
SELECT COUNT(*)
FROM "Analytics"
WHERE "FullVisitorID" IS NULL

SELECT COUNT(*)
FROM "All_Sessions"
WHERE "FullVisitorID" IS NULL

SELECT "FullVisitorID",
	COUNT(*)
FROM "All_Sessions"
GROUP BY "FullVisitorID"
HAVING COUNT(*) > 1

SELECT "FullVisitorID",
	COUNT(*)
FROM "Analytics"
GROUP BY "FullVisitorID"
having COUNT(*) > 1
```

- Checking Unique Values in the column

```
SELECT COUNT(DISTINCT("FullVisitorID"))
FROM "All_Sessions"

SELECT COUNT(DISTINCT("FullVisitorID"))
FROM "Analytics"
```

- Checking the values in the Date columns, the result is all numbers, no formatting
```
SELECT "Date"
FROM "Analytics"

SELECT "Date"
FROM "All_Sessions"
```


- Although there are no nulls for the FullVisitorID in each table, there are duplicate values in both, and the distinct values for FullVisitorID in both tables are different by roughly 10000 records

## 3. Cleansing

- Created a new Table called FullVisitors to hold all unique FullVisitorIDs, so it can be referenced for other tables

![image](https://github.com/user-attachments/assets/c0d6f9b2-5317-4178-a373-a305f23a3a2f)

- Inserted values of all unique FullVisitorIDs

```
INSERT INTO "FullVisitors" ("FullVisitorID")
SELECT DISTINCT "FullVisitorID"
FROM "All_Sessions"

UNION

SELECT DISTINCT "FullVisitorID"
FROM "Analytics"
ON CONFLICT ("FullVisitorID") DO NOTHING;
```


- Updating the Date columns to be a Date datatype and in date format. The result is datatypes changed to date and format is "YYYY-MM-DD"

```
Update "All_Sessions"
SET "Date" = "Date"::date

Update "Analytics"
SET "Date" = "Date"::date
```



## 4. Testing 

- Querying the FullVisitors Table. The result is 47559, which is all the unique FullVisitorIDs from the other tables.

```
SELECT * FROM "FullVisitors"
```

- Querying the tables once again to see updated to date format.

```
SELECT *
FROM "Analytics"

SELECT *
FROM "All_Sessions"
```

- Querying to see dates after 2016, the result is filtered responses of all the dates after 2016

```
SELECT "Date"::date
FROM "All_Sessions"
WHERE "Date"::date > '2016-01-01'

SELECT "Date"::date
FROM "Analytics"
WHERE "Date"::date > '2016-01-01'
```
