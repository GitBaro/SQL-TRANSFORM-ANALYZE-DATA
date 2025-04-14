# Question 1: What is the total Number of Unique Visitors?

## SQL Queries:

```
SELECT "FullVisitorID"
FROM "Analytics"

UNION

SELECT "FullVisitorID"
FROM "All_Sessions"
```


## Answer: 47559


# Question 2: What is the total number of unique visitors by referring sites?

## SQL Queries:

```
With VisitorCount AS
(SELECT COUNT(DISTINCT("FullVisitorID")) AS TotalVisitors
	FROM "Analytics"
) 
	
SELECT 
    "PagePathLevel1",
    COUNT(*) AS SessionCount,
    vc.TotalVisitors
FROM "All_Sessions" s
JOIN VisitorCount vc ON TRUE
GROUP BY "PagePathLevel1", vc.TotalVisitors
ORDER BY SessionCount DESC;
```


## Answer:

| PagePathLevel1  | SessionCount |  Total Visitors  |
| ------------- |:-------------:|  --------------  |
| /google+redesign/ | 14318    | 34991           |
| /store.html     | 384   | 34991       |
| /asearch.html    | 382    | 34991           |
| /yourinfo.html   | 13    | 34991           |


# Question 3: What is the percentage of viewers to the site that actually make a purchace?

## SQL Queries:

```
WITH VisitorCount AS (
SELECT -- "Units_Sold",
	COUNT(DISTINCT("FullVisitorID")) AS TotalVisitors
	FROM "Analytics"),


Purchasers AS (SELECT COUNT(DISTINCT "FullVisitorID") AS TotalUniquePurchasers
FROM "Analytics"
WHERE "Units_Sold"::INTEGER > 0)

SELECT TotalVisitors,
	TotalUniquePurchasers,
	(TotalUniquePurchasers::real / TotalVisitors::real) * 100.00 AS PurchasePct
FROM VisitorCount
JOIN Purchasers ON true
```


## Answer: 13%

