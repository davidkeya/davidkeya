---
title:  "How to import a csv file into PostgreSQL"
category: posts
date: 2020-11-19
excerpt: "Here’s How to import a csv file into PostgreSQL"
---

### What you need
1.	Sqlite3
2.	Db Browser for SQLite
3.	Text editor like atom

Follow through the steps below
1. Import and create table
-	Download the .csv file
-	Open Db Browser for SQLite
-	Navigate to file, import menu, then Import table from CSV file
-	Table name same as csv file, can rename in the Table name field and click ok.
-	Boom!! A table is automatically created in the preferred database with the same column names.

2. Export Table as .sql file
-	Open Db Browser for SQLite
-	Navigate to file, export menu, then Data base to CSV file
-	On the export window, select the preferred table to export and save on a preferred location.
-	Export completed!!

3. Gather code into PostgreSQL
-	Using a preferred text editor open the exported .sql file, copy and paste into the PostgreSQL editor
-	Run the query create table
