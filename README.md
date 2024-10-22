# Bird Strikes Database Practicum

## Overview
In this practicum, you will build a database for analyzing bird strikes on aircraft using an existing FAA dataset. Key tasks include building a relational schema, implementing it in MySQL/MariaDB, loading data, running SQL queries, and performing simple analysis in R.

## Learning Objectives
- Set up MySQL/MariaDB
- Connect MySQL/MariaDB to R
- Implement a relational schema
- Load data from CSV into a database via R
- Execute SQL queries in R
- Perform analytics in R
- Debug and resolve programming errors

## Tasks
1. **Setup MySQL/MariaDB (2 hrs)**: Configure MySQL locally or use a cloud instance. Create a new database.  
2. **Create R Notebook (0.1 hrs)**: Name it `LastNameFirstInitial.CS5200.PractI-S23.Rmd` with appropriate title, author, and date.
3. **Connect to Database (0.1 hrs)**: Add R code chunk to connect to the database.
4. **Create Database Schema (3.5 hrs)**: Define tables, constraints, primary/foreign keys for `incidents`, `airports`, `conditions`, and `airlines`.
5. **Populate Tables (8 hrs)**: Load data from `BirdStrikesData.csv` into the defined schema using R. Use synthetic keys as necessary.
6. **Data Queries**:
   - Find the top 10 states with the most incidents (1 hr)
   - Find airlines with above-average bird strikes (1 hr)
   - Analyze incidents by month and flight phase (1 hr)
7. **Visualizations**:
   - Create a scatter plot of incidents by month (2 hrs)
8. **Stored Procedure (3 hrs)**: Create a MySQL procedure to add a new incident.
