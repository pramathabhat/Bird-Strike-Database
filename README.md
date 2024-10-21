Nota Bene
Read this entire page twice before you get started.

Practicums have a due date different than assignments. The due date is Friday, March 3 at 11:59pm ET (the day before Spring Recess). Late submissions are accepted (with the usual penalty of 2.5% per day late) until the end of Spring Recess on March 12 at 11:59pm ET. No submissions are accepted after that. Note that the availability of the instructional staff during recess is very limited, so be sure to plan for that. 

Work on the practicum for at least three hours every day and use the time during the week prior to the practicum to start working on it, especially the configuration of the MySQL Server and the loading of the data.

A gentle reminder that the average of both practicums must be above 70% to pass this course, so be sure to complete on time and seek help right away. Do not procrastinate -- things that appear simple often take more time than expected and, of course, programming is fraught with potholes on the road to success. So plan accordingly.

The average time to complete the practicum is 15-25 hours. Do not wait to start. Seek help early. Submit often and as soon as you have enough code that works. We will only grade the last submission. Check your submission before you submit and after.

Overview
In this practicum you will build a database that can be used to analyze bird strikes on aircraft. For an existing data set from the FAA [1], you will build a logical data model, a relational schema, realize the relational schema in MySQL/MariaDB, load data into the database, execute SQL queries, a finally perform some simple analysis of the data.

Use the provided time estimates for each tasks to time-box your time. Seek assistance if you spend more time than specified on a task -- you are likely not solving the problem correctly. A key objective is to learn how to look things up, how to navigate complex problems, and how to identify and resolve programming errors.

Learning Objectives
In this practicum you will learn how to:

install/procure MySQL or MariaDB
connect to MySQL/MariaDB from R in an R Notebook
implement a relational schema for an existing data set
load data from CSV files into a relational database through R
execute SQL queries against a MySQL/MariaDB database through R
perform simple analytics in R
identify and resolve programming errors
look up details for R, SQL, and MySQL/MariaDB
time-box work
Format
Complete in pairs or individually; working in pairs is not required. We do not pair up students; finding a partner is the student's responsibility.
Add both team members as authors to the submission in the R Notebook and in the submission comments, but only one person needs to make a submission. Both team members will receive the same grade.
If a team member is not contributing, the other team member may simply quit and continue individually using all work done up to that point. It is expected that both team members do an equal amount of work of similar complexity. You must write a submission comment explaining who you worked with, when you started working together, when you split, and why.
A pair = two members in a team, that means two and no more than two; working in a group of three is not a pair and is not allowed.
Prerequisite Tasks
Read the Hints and Tips section below and go back to them often when you encounter problem. Most problems are addressed in that section. Consult the list before contacting us for help as you'll be able to resolve the issue more quickly.
Decide on whether you will use MySQL (or MariaDB) locally or whether you will use a cloud installation: READ FIRST: Which Database to Use? If you use db4free then you cannot use dbWriteTable() and need to insert data row by row. See the tutorials above.
Create an R Project and within that project create an R Notebook in which to do all of your work. Place all files within the project folder and do not use absolute file paths. Embed any diagrams in the R Notebook and be sure to submit them as files in your submission. Keep updating this notebook as you complete tasks. Learn how to use journaling in data analysis work. Use this R Markdown cheat sheet Download R Markdown cheat sheetfor reference. Of course, in practice, you will likely build different programs (perhaps even using different programming language) for database creation, data loading, and the dashboard. But here we will do it all in one R Notebook.
Become familiar with the problem of bird strikes on aircraft. The report in [1] provides an overview. You should scan it to become familiar with the domain but you do not need to read it deeply.
Download the file BirdStrikesData.csv (Links to an external site.) and save it locally to your R Project folder (the same folder that contains you .Rmd and your .Rproj files) or reference it from the URL. You may wish to create a new data file that is a subset of the full data that you use for development so loading takes less time. This is a common strategy in practice. To download the file, use the right mouse button and choose "Save Link As..." or a similar menu choice on your browser. Do not click on the link as that will cause the browser to open and display the file.
Read the Hints & Tips section frequently and before posting questions.

Tasks
Before you start, read all of the questions. Inspect the CSV data file that you downloaded so you are familiar with its columns, data types, and overall structure. Assume that this database will eventually be used for an app that can be used by pilots (of any kind of aircraft) to report wildlife incidents. 

All R and SQL code blocks must be named, as shown in the example below. This is necessary so that you can reference your code blocks in the self-evaluation rubric to be filled out at the end of the practicum. The names of code blocks must be unique.

```{r nameOfRCodeBlock, eval = T, warning = F}```

```{sql nameOfSQLCodeBlock, connection = xDB}```
You may add any additional block parameters as needed.

Use functions to structure your code so that it becomes more readable and easier to develop and debug. Use headers to segment your notebook and add explanations as to what each code block means. Follow common coding practices and format your code so it is readable, and use functions to break down complex code.

(5 pts / 2.0 hrs) Set up, configure a MySQL Server locally or on the cloud using the resources provided here and on Canvas. Once configured, create a new MySQL database. Note that you may use SQLite instead of MySQL but you will not get credit for this question nor credit for the question below that asks you to create a stored procedure as those are not supported in SQLite.

(1 pts / 0.1 hrs) Create an R Notebook named "LastNameFirstInitial.CS5200.PractI-S23.Rmd" where LastName is your last name and FirstInitial is the first letter of your first name, e.g., SchedlbauerM. Set the title of the R Notebook to "Practicum I CS5200", add an author field, and set the date to "Spring 2023".

(4 pts / 0.1 hrs) Add a second level header (##) to the R Notebook called "Connect to Database" and then add an R code chunk that connects to your MySQL database. Use headers for all other questions with appropriate titles so you (and we) can navigate the notebook more easily. If you have difficulty connecting to or setting up MySQL, then use SQLite and proceed. You can always come back to this question and change your configuration so that you connect to MySQL. This is the benefit of relational databases: you can easily switch between databases without changing your code.

(30 pts / 3.5 hrs) Add a second level header to the R Notebook called "Create Database" and then add appropriate R and/or SQL code chunks to create the database schema described below. Add appropriate constraints, primary key and foreign key definitions. In the schema definitions below, primary keys are underlined and foreign keys are bolded.

(5 pts / 0.5 hrs) Create a table incidents that stores wildlife strike incidents with this schema:

incidents (rid : integer,
                  dep.date : date, origin : integer, airline : integer,
                  aircraft : text, flight.phase : {takeoff, landing, inflight, unknown},
                  altitude : integer ≥ 0, conditions : {...},
                  warned: boolean)

The column altitude should be restricted to positive integers. The column flightphase should be restricted to those values (use a value set definition and not a lookup table). For now, make the column conditions of type 'text' or 'varchar'; later we will refine that to using a lookup table. Make warned a Boolean flag and use TRUE if the pilot was warned, FALSE otherwise. Use appropriate data types for the columns and store any date as a date type not as text (subject to the data types your chosen database supports). If date or boolean are not supported, choose another data type that will work or split the dates into month, day, and year columns. Note that some columns contain periods so that will require special treatment in SQL -- investigate how to deal with this common issue.

(5 pts / 0.5 hrs) Create a table that stores airports and states called airports and that follows this schema:

airports (aid : integer, airportName : text, airportCode : text, state : text) 

aid is a synthetic primary key, airportName and state correspond to the airport name and state from the data file. The airport code should be the airport's international code, e.g., BOS for Boston or LGA for LaGuardia. However, you may leave it empty for this database -- it is for future expansion.

(4 pts / 0.3 hrs) Link the incidents and airports tables via the origin foreign key in incidents to the primary key aid in airports. The origin is an FK to the airport in the airports table. Update the above table definitions for airports and incidents as necessary.

(4 pts / 0.5 hrs) Create a lookup table called conditions defined as follows:

conditions (cid, condition, explanation)

Link this lookup table to the incidents table through the conditions foreign key. This table contains the values of all conditions, e.g., 'Overcast'. Leave the explanation column empty (future expansion).

(4 pts / 0.5 hrs) Create a table that stores airlines called airlines and that follows this schema:

airlines (eid : integer, airlineName : text, airlineCode : text, flag : text) 

eid is a synthetic primary key, airlineName corresponds to the airline column from the data file. The airlineCode should be the airlinet's abbreviation code, e.g., J6 for JetBlue or AA for American Airlines. However, you may leave it empty for this database -- it is for future expansion. The flag column is the flag under which this airline flies, e.g., Lufthansa flies under the flag of "Germany".  However, you may leave it empty for this database -- it is for future expansion.

(3 pts / 0.3 hrs) Link the incidents and airlines tables via the airline foreign key in incidents to the primary key eid in airlines. 

(2 pts / 0.3 hrs) Add one or more code chunks that are not evaluated (eval = F) when the Notebook is knitted but can be used to test your table definitions. Add whatever test code you need to assure yourself that your table definitions are correct.

(1 pts / 0.1 hrs) If you haven't yet, download the bird strikes CSV data file from the link provided before. Place the Bird Strikes CSV file into the same folder as your R Notebook and the load it into a dataframe called bds.raw. Do not use a path name when loading. The default path is the local folder that contains the R Notebook when you have the R Notebook in an R Project.

(20 pts / 8 hrs) Using the table definitions and the data in the dataframe bds.raw from above, populate the tables with the data from the appropriate columns. Omit the columns from the CSV that are not referenced in the tables. You do not need to create any additional tables. Because we are not adding additional tables there will be (unnormalized) data and repetitions, for example for aircraft -- that is acceptable for this practicum due to time constraints but would not be if this were an actual analytics database project. Assume "Business" to be an airline name (it is actually a private flight but we assume it is the airline called "Business") and store those incidents.

Use default values where the data file does not contain values or leave empty. If there is no airport or airline, then link to a "sentinel" airline or airport, i.e., add an "unknown" airline and airport to the tables rather than leaving the value NULL. Assign synthetic key values as and where needed and use them as primary keys. Whether you generate them in R code or the database is up to you -- each has pros and cons and part of the objective of this practicum is for you to think through such decisions.

Map the values in the data file to appropriate values in any lookup tables using reasonable rules that you may define as necessary.

See the Hints below for information on db4free. All data manipulation and importing work must occur in R. You may not modify the original data outside of R -- that would not be reproducible work. It may be helpful to create a subset of the data for development and testing as the full file is quite large and takes time to load.

(1 pts / 0.5 hr) Show that the loading of the data worked by displaying parts of each table (do not show the entire tables).  

(3 pts / 1 hr) Create a SQL query against your database to find the 10 states with the greatest number of incidents. You may either use a {sql} code chunk or an R function to execute the query. It must be a single query. Display the state and the number of incidents. Note that every row in the incidents table constitutes one "incident".

(10 pts / 1 hr) Create a SQL query against your database to find the airlines that had an above average number bird strike incidents. You may either use a {sql} code chunk or an R function to execute the query. It must be a single query. To do this, find the number of bird strike incidents for each airline (remember that each row in the incidents table is a single bird strike incident). Then calculate the average across all airlines and from there find those airlines which had an above average number of bird strike incidents. List the names of the airlines and the number of incidents for each.

(8 pts / 1 hr) Create a SQL query against your database to find the number of bird strike incidents by month and by flight phase (across all years). Save the result of the query in a dataframe. Include all airlines and all flights. You may either use a {sql} code chunk or an R function to execute the query. It must be a single query. This query can help answer the question which month and flight phase, historically, are the most dangerous for bird strikes. Display the first six rows of the dataframe.

(5 pts / 2 hrs) Using the dataframe from Question 10 above, build a scatter plot that plots month along the x-axis versus number of incidents (across all airlines and flight phases). Adorn the graph with appropriate axis labels, titles, legend, data labels, etc. You should use the standard R plot() function; you do not need to use packages such as ggplot, ggplot2, or plotly -- although you may, of course. This tutorialLinks to an external site. may help you get started.

(10 pts / 3 hrs) Create a stored procedure in MySQL (note that if you used SQLite, then you cannot complete this step) that adds a new incident to the database. You may decide what you need to pass to the stored procedure to add a bird strike incident and you must account for there being potentially a new airport and/or airline. After insertion, show (in R) that your procedure worked. Note that if you used SQLite rather than the required MySQL for the practicum, then you cannot complete this question as SQLite does not support stored procedures.

(5 pts) Professionally developed code that is well documented and all chunks are labeled.
Resources
[1] Data Visualization - Bird Strike Dataset by H. Haveliwala | data.worldLinks to an external site.
[2] R Markdown Cheat SheetDownload R Markdown Cheat Sheet
[3] Using MySQL and MariaDB with R (jagg19.github.io)Links to an external site.
[4] RMariaDB: MariaDB Driver for R - MariaDB Knowledge BaseLinks to an external site.

Hints and Tips
Ask clarifying questions in the Assignments channel on Teams.
If you find it helpful, draw an ERD.
Ask questions as soon as you encounter them.
While you need to look up details for functions and R, the solution cannot be found via Google.
Do not spend extraordinary time on code errors; ask for help if you cannot resolve them within 30-minutes. First through the Assignment channel on Teams and then by going to TA office hours -- the TAs will alert the instructor if there are doubts they cannot resolve.
If you have trouble connecting, be sure to disable any firewall or anti-virus software that may be clocking port 3306 -- or add port 3306 to the list of open ports in your firewall software configuration.
The function dbWriteTable() is disabled for bulk loading on the MySQL cloud installation on db4free. It does work fine for MySQL on AWS and for local installations of MySQL if you allow for batch loading.
Be sure to click the activation link in the email from db4free.net after you create your database; if you get "Access denied..." error messages then you did not activate your account.
Be sure to shut down your AWS RDS database if you are not using it; otherwise you might exceed the monthly free time. And, be sure to delete the database after the course is done or you will be billed.
Batch loading (via dbWriteTable()) is disabled for security reasons by default on local installations of MySQL. Here's how to enable it: mysql - ERROR: Loading local data is disabled - this must be enabled on both the client and server sides - Stack OverflowLinks to an external site.. Note that you cannot enable this for db4free.net -- it does not give you privileged access to do this.
Enable functions, procedures, and triggers on Amazon AWS RDS:
https://aws.amazon.com/premiumsupport/knowledge-center/rds-mysql-functions/Links to an external site.
On AWS, if you get errors that the service is not reachable, then you need to edit the "inbound rules" of the security group that is attached to the RDS -- add the MySQL/Aurora type and port range 3306 with cidr 0.0.0.0/0
If you use sqldf for manipulating or querying internal data frames, be mindful of conflicts between SQLite and MySQL; see mysql - How to use sqldf in R to manipulate local dataframes? - Stack Overflow.Links to an external site. A potential issue with sqldf can occur when you connect to MySQL or a non-SQLite database as sqldf attempts to use your existing database connection as a backing store for its data; this will often not work due to security constraints. So, you need to add the R code options(sqldf.driver = 'SQLite') which forces sqldf to use SQLite as its backing store.
sqldf is very slow for querying or extracting data from a data frame as it actually copies the data frame to an in-memory SQLite database and then runs a SQL query; so, only use sqldf is there's no simple way to do a native R "query" with logical operations and which() and any(), e.g., use sqldf to do grouping but not much else
If you get errors connecting to MySQL, make sure you have the latest version of R and upgrade R and all packages as necessary.
Using mixed upper and lower case for table names sometimes causes issues with dbSendStatement() and dbWriteTable() when using MySQL; make all table names and attributes names fully lower case; SQL is not case sensitive when it comes to keywords like INSERT vs insert BUT it is when it comes to table and attribute names
Put columns that contain special character such as period (.) or have names that are keywords into backticks, e.g., SELECT `condition` FROM incidents;
If you get a message "Can't initialize character set unknown", see https://stackoverflow.com/questions/52613809/rmysql-error-cant-initialize-character-set-unknownLinks to an external site. and https://github.com/pBlueG/SA-MP-MySQL/issues/203Links to an external site.
There appears to be a bug in MySQL stored procedures that contain a SELECT as the last statement in the procedure; if you get the message "Commands out of sync; you can't run this command now", you must use INTO with your SELECT; see https://stackoverflow.com/questions/6583020/mysql-stored-procedure-caused-commands-out-of-syncLinks to an external site.
All your work must be within your R Notebook; we will run your R Notebook against one of our MySQL servers with a blank database (or SQLite if that's what you used) and it has to run from beginning to end; so if you did work outside of your R Notebook then we cannot reproduce your work you'll get a grade of 0.
Before submitting, test that you code runs and your Notebook knits in a clean environment. So, remove all objects first by either including this code in the beginning of your R Notebook rm(list = ls()) or by clearing your environment in R Studio with the menu item Session/Clear Workspace.
Explain your approaches and any manipulations, omissions, deletions, or modifications of data.
Be sure to install packages within your code (but only if not installed) to ensure they get installed when the graders run your code. Here's an elegant way to do this: https://statsandr.com/blog/an-efficient-way-to-install-and-load-r-packages/Links to an external site.
In R, if you want to change a global variable (one used first outside a function), then you need to use a special assignment operator: <<- instead of <-. 
If your data frames are not written to the database when you use dbWriteTable() then check to see if your data frame contains columns of type date -- there may be issues in converting R dates to SQL dates; for more information on this, see Lesson 6.306 Dates in R and SQLiteLinks to an external site.
MySQL Cloud Servers
Amazon RDS Free Tier | Cloud Relational Database | Amazon Web ServicesLinks to an external site.
db4free.net - MySQL DatabaseLinks to an external site.
Hosting with PHP, MySQL and cPanel (freehosting.host)Links to an external site.
Hosting with PHP, MySQL (AwardSpace.com)Links to an external site.
Submission Details
Before submitting your code, complete the self-evaluation rubric (separate "assignment"; see Canvas).

Provide in your R Notebook:
names and emails of all members of your pair; only one submission per pair (one person submits); add both team members as authors to the submission in the R Notebook and in the submission comments.
table creation SQL for MySQL/MariaDB (or SQLite)
results of queries, visualizations, computations to show that your code works as expected
clear explanations of your code that is decomposed into chunks and preceded by headers
Submit the .Rmd source file of your R Notebook. The code must run from start to end, so be sure to test carefully, load any required libraries, and ensure that your chunks run sequentially from start to end.
Submit a knitted PDF of your Rmd; the PDF must be a compact document, so pay attention to formatting, headers, and how much data you print. If you have trouble knitting on your local installation of R Studio, consider using the cloud version of R Studio to do the knitting. Not submitting a PDF results in a loss of 5 points. Submitting a poorly formatted PDF results in a loss up to 5 points.
All your work must be within your R Notebook; during the demonstration, we will ask you to run your R Notebook against one of our MySQL servers with a blank database and it has to run from beginning to end; so if you did work outside of your R Notebook (e.g., in Excel or MySQL Workbench) then we won't be able to reproduce your work and you will get a grade of 0.
Your code has to run, obviously, but it also has to run somewhat efficiently... if everyone else's code runs in 10-30 minutes but yours takes several hours then clearly is due to poor programming and not due to the inherent complexity of the problem... follow common coding strategies for writing efficient code such as factoring out invariants from loops, not calling functions repeatedly, pre-allocating memory, not copying objects needlessly, not calling expensive functions when simpler ones will do (e.g., call substring() instead of doing regular expressions), use which() when searching and don't use sqldf, and so forth. These practices are not specific to R, although there are R specific performance issues, but those are less likely to be a concern here.
