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


# Question 3: 

## SQL Queries:

## Answer:



# Question 4: 

## SQL Queries:

## Answer:



# Question 5: 

## SQL Queries:

## Answer:
