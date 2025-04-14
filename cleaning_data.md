What issues will you address by cleaning the data?
Date/Time Issues:
- Changed Date Columns of All_Sessions and Analytics tables to proper "YYYY-MM-DD" Format


MISC Issues
- Updated Unit Cost in Analytics Table to be divided by 1,000,000

Queries:
Below, provide the SQL queries you used to clean your data.

Date/Time:
--Updated date format for All_Sessions and Analytics
Update "All_Sessions"
SET "Date" = "Date"::date

Update "Analytics"
SET "Date" = "Date"::date

--Updated Unit Cost in Analytics Table to be divided by 1,000,000

UPDATE "Analytics"
SET "Unit_Price" = CAST("Unit_Price" as Integer) / 1000000
