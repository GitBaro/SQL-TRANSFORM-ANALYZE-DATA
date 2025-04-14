## What issues will you address by cleaning the data?
# Date/Time Issues
- Changed Date Columns of All_Sessions and Analytics tables to proper "YYYY-MM-DD" Format

# Country/Location Issues

# MISC Issues
- Updated Unit Cost in Analytics Table to be divided by 1,000,000

## Queries:
Below, provide the SQL queries you used to clean your data.

# Date/Time

--Updated date format for All_Sessions and Analytics

Update "All_Sessions"
SET "Date" = "Date"::date

Update "Analytics"
SET "Date" = "Date"::date

--Updated Unit Cost in Analytics Table to be divided by 1,000,000

```
UPDATE "Analytics"
SET "Unit_Price" = CAST("Unit_Price" as Integer) / 1000000
```

# Country/Location
--Changed to "Other" where City and Country was "not available in demo dataset" and "(not set)"

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
```
