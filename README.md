**Due Date: Feb 10 2022**

# Goals of the exercise. 

 * Learn to work with AWS and create an AWS RDS instance.
 * Learn to set up and upload structered data for eg: [MLB Data](data/readme2012.txt) in to MySQL RDS instance. 
 * Query and analyze structured data with MLB data as an example.

# Checklist of assignment Steps


- Accept the assignment at github classroom
- Update the notebooks in the assignment with your username as discussed in [AcceptingaGithubassignment.pdf](AcceptingaGithubassignment.pdf)
- Ensure you have AWS Academy access through the classroom
- Follow the steps to create the database in AWS.
- Finish the queries and save the response in the mlb.ipynb notebook. Save the results to show the execution results.
- Profile the queries as described in the last step and save the profile results in the notebook as well.
- Copy the assignment github url and submit to  brightspace
- Delete your mysql instance from AWS when you are sure that you are done. Remember to always pause the database when you are not using it and turn it on when you are going to be doing the assignment.


# Prior Reading
  
 * Make sure to go through the SQL content for  week 2 in Brightspace
 * You can refer to the videos at : https://brightspace.vanderbilt.edu/d2l/le/content/342996/Home for help with on the steps that are outlined below. Also, a previous version of the detailed pdf instructions are available at [SetupAWS-RDS-MySQL-Load-Data-From-Workbench.pdf](SetupAWS-RDS-MySQL-Load-Data-From-Workbench.pdf). The only catch is that instead of AWS educate you are using AWS academy.

## Helpful Links and  Instructions

For this assignment you may  need to refer to the following instructions from the instructions repository.

- [about github](https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/github)
- [about aws educate](https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/aws)
- [about colab](https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/colab)
- [about colab and SQL on aws](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [about code profiling](https://jakevdp.github.io/PythonDataScienceHandbook/01.07-timing-and-profiling.html)


**Remember** - Update the notebooks in the repository with your username as discussed in [AcceptingaGithubassignment.pdf](AcceptingaGithubassignment.pdf). You can also use the open in colab chrome extension as shown at https://colab.research.google.com/github/googlecolab/colabtools/blob/master/notebooks/colab-github-demo.ipynb. Pay special attention to the section on opening private repositories.

# Assignment Description (100 points)

In this assignment you are using a database that contains batting and pitching statistics from 1871 onwards, plus fielding statistics, standings, team stats, managerial records, post-season data, and more. See [readme2012.txt](data/readme2012.txt) for details about this MLB data.

## Software Required and initial steps

I encourage the use of [MySQL Workbench](https://www.mysql.com/products/workbench/)  to practice SQL and work with the data. This will help you determine the query to be used which you can then paste as a string in the colab notebook and run it.

Also note that each repository can be downloaded to your local machine. But you can also work with opening the notebook directly from google colab.  

To download the repository locally follow these steps

## Repository Setup
Repositories will be created for each student. You should see yours at

https://github.com/vu-topics-in-big-data-2022/programming-assignment-1-<GITHUB USERNAME\> 
Clone the repository to your home directory on the cluster using:

git clone https://github.com/vu-topics-in-big-data-2022/programming-assignment-1-<GITHUB USERNAME\>.git
I may push updates to this homework assignment in the future. To setup an upstream repo, do the following:

git remote add upstream https://github.com/vu-topics-in-big-data-2022/programming-assignment-1.git
To pull updates do the following: git fetch upstream git merge upstream/master

You will need to resolve conflicts if they occur.
 
## AWS
Make sure you have received the invitation and accepted the invitation

To access AWS go to AWS academy and use the account you created when you were invited to the class. Then, get to the AWS console. 

Ensure that you can access this account and can land into an AWS console as shown below. Please see https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/aws

![AWS](images/AWS.png)

## Step-1 Create the MYSQL Instance

Follow the instructions at https://aws.amazon.com/getting-started/tutorials/create-mysql-db/ to create a mysql database instance. Follow the instructions carefully to remain within **free tier**. That last part is very important. 

To ensure that you can connect this from google colab you will need to ensure that you choose Public accessibliity (see the image on https://aws.amazon.com/getting-started/tutorials/create-mysql-db/ in the configure advanced settings section.). 

Lastly, you should choose the default VPC. But create a new VPC security group. Once that group is created you can open the inbound connection to 0.0.0.0/0 (Anywhere) for port 3306 - the mysql port. See https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html for reference.

Note that once you start it can take 10-15 minutes for the RDS instance to be provisioned

## Step 2 - Populate the MySQL instance

Download MySQL Workbench and connect to the database you created in the first step. Follow the Step 2 at https://aws.amazon.com/getting-started/tutorials/create-mysql-db/. 

Then load the lahman data into mysql from [data/lahman2012.sql](data/lahman2012.sql.gz). Remember to gunzip the file to get .sql extension. See [readme2012.txt](data/readme2012.txt) for details about this MLB data. To load the data first connect your SQL workbench to your database on AWS and then load sql script referenced above (lahman2012.sql) from Run SQL Script prompt. Choose default schema. It will create a database called lahman.

![SQL script](images/MySQLWB.png)

Once it has been loaded you can execute the query "show databases" and it will show you a number of databases included lahman. See below

![SQL script](images/sqlworkbench1.png)

You can also issue the queries "use lahman" (i.e. select this database for use), followed by another query "show tables" and then click on the inspector icon to open the inspector for database where you can get a view like below that describes all tables. You can explore this view and also see all the columns in tables. see the two images below.

![SQL script](images/sqlworkbench.png)

![SQL script](images/sqlworkbench2.png)

**Very Important** : Remember to shutoff the RDS instance when you are not using it.  


## Step 3- Check initial Colab Connection

Run the Colab notebook [mlb.ipynb](mlb.ipynb) and ensure that you get the connection and the number of db tables correctly. Make sure that you update the database name, the username and the password.  

**Remember that you have to change the initial url to include your name correctly just as you did in assignment 0. Then go ahead and click on - open in colab**.

Note that if the button is not available - or the direct click from github does not work - you can also login to google colab and choose open (from github),  enable private repos and search for your repo in the list and open. 

If you do not have access to colab - then you can run the notebook locally through anaconda jupter server. See the instructions about [class python environment](https://github.com/vu-topics-in-big-data-2022/lectures/tree/main/python-environment). 

**Very Important** : Remember to shutoff the RDS instance when you are not using it.

## Step 4 - Implement Queries   

Implement all the SQL queries identified in mlb.ipynb . Record the answers in the mlb.ipynb and save it back to your repository.

The queries are

1. The number of all stars in allstarfull.
2. The most home runs in a season by a single player (using the batting table).
3. The playerid of the player with the most home runs in a season.
4. The number of leagues in the batting table.
5. Barry Bond's average batting average (playerid = 'bondsba01') where batting average is hits / at-bats. Note you will nead to cast hits to get a decimal: cast(h as real)
6. The teamid with the fewest hits in the year 2000 (ie., yearid = '2000'). Return both the teamid, and the number of hits. Note you can use ORDER BY column and LIMIT 1.
7. The teamid in the year 2000 (i.e., yearid = '2000')  with the highest average batting average. Return the teamid and the average. To prevent divsion by 0, limit at-bats > 0.
8. The number of all stars the giants (teamid = 'SFN') had in 2000.
9. The yearid which the giants had the most all stars.
10. The average salary in year 2000.
11. The number of positions (e.g., catchers, pitchers) that have average salaries greather than 2000000 in yearid 2000. You will need to join fielding with salaries. Also consider using a HAVING clause.
12. The number of errors Barry Bonds had in 2000. 
13. The average salary of all stars in 2000. Report answer as integer.
14. The average salary of non-all stars in 2000.  Report answer as integer.

You can test each query result using the  corresponding tests in the notebook.

To start solving this here are few hints. First understand the table and the data from [data/readme2012.txt](data/readme2012.txt) . Then execute the query describe tablename on mysql. you can describe other tables as well.

For example here is the response for 

```
describe batting
```
```
playerID	varchar(9)	NO	PRI	
yearID	int	NO	PRI	
stint	int	NO	PRI	
teamID	varchar(3)	YES		
lgID	varchar(2)	YES		
G	int	YES		
G_batting	int	YES		
AB	int	YES		
R	int	YES		
H	int	YES		
2B	int	YES		
3B	int	YES		
HR	int	YES		
RBI	int	YES		
SB	int	YES		
CS	int	YES		
BB	int	YES		
SO	int	YES		
IBB	int	YES		
HBP	int	YES		
SH	int	YES		
SF	int	YES		
GIDP	int	YES		
G_old	int	YES		
```

You will notice that playerid, yearid and stintid together forms a composite primary key.



### Hint 1:

To solve the third query I can first find the max and then create an inner join as follows

```
select * from batting INNER Join (select MAX(HR) as m from batting) as data ON batting.hr=data.m
```

### Hint 2:

Remember you can formulate the queries and execute them directly through workbench. Once that is done and you like the result, copy the query to the python notebook

Solve the other queries similarly.

## Step 5 - Implement Profiling for the queries

Profile the queries as shown in the notebook. Use the profiling instructions shown in brightspace.

# Grading Rubrics

- Each query is carries equal points. Query 1,3 and 9 are already solved. So you have to implement 11 queries.
- 4 points for implementing the profiling code that will run each test and record the time taken to execute. Save all answers in notebook and save it back to github
- When finished submit your url to brightspace for the assignment

```SQL
q1 = 'select count(*) from allstarfull;'
q3 = 'select playerid from batting INNER Join (select MAX(HR) as m from batting) as data ON batting.hr=data.m'
q9 = "SELECT yearid FROM allstarfull WHERE teamid = 'SFN' group by yearid having count(distinct playerid\)
      =(select max(nump) from (SELECT yearid, count(distinct playerid) as nump FROM allstarfull WHERE teamid = 'SFN' group by yearid) as innertable)"
```



**Due Date: Feb 10 2022**

# Goals of the exercise. 

 * Learn to work with AWS and create an AWS RDS instance.
 * Learn to set up and upload structered data for eg: [MLB Data](data/readme2012.txt) in to MySQL RDS instance. 
 * Query and analyze structured data with MLB data as an example.

# Checklist of assignment Steps


- Accept the assignment at github classroom
- Update the notebooks in the assignment with your username as discussed in [AcceptingaGithubassignment.pdf](AcceptingaGithubassignment.pdf)
- Ensure you have AWS Academy access through the classroom
- Follow the steps to create the database in AWS.
- Finish the queries and save the response in the mlb.ipynb notebook. Save the results to show the execution results.
- Profile the queries as described in the last step and save the profile results in the notebook as well.
- Copy the assignment github url and submit to  brightspace
- Delete your mysql instance from AWS when you are sure that you are done. Remember to always pause the database when you are not using it and turn it on when you are going to be doing the assignment.


# Prior Reading
  
 * Make sure to go through the SQL content for  week 2 in Brightspace
 * You can refer to the videos at : https://brightspace.vanderbilt.edu/d2l/le/content/342996/Home for help with on the steps that are outlined below. Also, a previous version of the detailed pdf instructions are available at [SetupAWS-RDS-MySQL-Load-Data-From-Workbench.pdf](SetupAWS-RDS-MySQL-Load-Data-From-Workbench.pdf). The only catch is that instead of AWS educate you are using AWS academy.

## Helpful Links and  Instructions

For this assignment you may  need to refer to the following instructions from the instructions repository.

- [about github](https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/github)
- [about aws educate](https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/aws)
- [about colab](https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/colab)
- [about colab and SQL on aws](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [about code profiling](https://jakevdp.github.io/PythonDataScienceHandbook/01.07-timing-and-profiling.html)


**Remember** - Update the notebooks in the repository with your username as discussed in [AcceptingaGithubassignment.pdf](AcceptingaGithubassignment.pdf). You can also use the open in colab chrome extension as shown at https://colab.research.google.com/github/googlecolab/colabtools/blob/master/notebooks/colab-github-demo.ipynb. Pay special attention to the section on opening private repositories.

# Assignment Description (100 points)

In this assignment you are using a database that contains batting and pitching statistics from 1871 onwards, plus fielding statistics, standings, team stats, managerial records, post-season data, and more. See [readme2012.txt](data/readme2012.txt) for details about this MLB data.

## Software Required and initial steps

I encourage the use of [MySQL Workbench](https://www.mysql.com/products/workbench/)  to practice SQL and work with the data. This will help you determine the query to be used which you can then paste as a string in the colab notebook and run it.

Also note that each repository can be downloaded to your local machine. But you can also work with opening the notebook directly from google colab.  

To download the repository locally follow these steps

## Repository Setup
Repositories will be created for each student. You should see yours at

https://github.com/vu-topics-in-big-data-2022/programming-assignment-1-<GITHUB USERNAME\> 
Clone the repository to your home directory on the cluster using:

git clone https://github.com/vu-topics-in-big-data-2022/programming-assignment-1-<GITHUB USERNAME\>.git
I may push updates to this homework assignment in the future. To setup an upstream repo, do the following:

git remote add upstream https://github.com/vu-topics-in-big-data-2022/programming-assignment-1.git
To pull updates do the following: git fetch upstream git merge upstream/master

You will need to resolve conflicts if they occur.
 
## AWS
Make sure you have received the invitation and accepted the invitation

To access AWS go to AWS academy and use the account you created when you were invited to the class. Then, get to the AWS console. 

Ensure that you can access this account and can land into an AWS console as shown below. Please see https://github.com/vu-topics-in-big-data-2022/instructions/tree/main/aws

![AWS](images/AWS.png)

## Step-1 Create the MYSQL Instance

Follow the instructions at https://aws.amazon.com/getting-started/tutorials/create-mysql-db/ to create a mysql database instance. Follow the instructions carefully to remain within **free tier**. That last part is very important. 

To ensure that you can connect this from google colab you will need to ensure that you choose Public accessibliity (see the image on https://aws.amazon.com/getting-started/tutorials/create-mysql-db/ in the configure advanced settings section.). 

Lastly, you should choose the default VPC. But create a new VPC security group. Once that group is created you can open the inbound connection to 0.0.0.0/0 (Anywhere) for port 3306 - the mysql port. See https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html for reference.

Note that once you start it can take 10-15 minutes for the RDS instance to be provisioned

## Step 2 - Populate the MySQL instance

Download MySQL Workbench and connect to the database you created in the first step. Follow the Step 2 at https://aws.amazon.com/getting-started/tutorials/create-mysql-db/. 

Then load the lahman data into mysql from [data/lahman2012.sql](data/lahman2012.sql.gz). Remember to gunzip the file to get .sql extension. See [readme2012.txt](data/readme2012.txt) for details about this MLB data. To load the data first connect your SQL workbench to your database on AWS and then load sql script referenced above (lahman2012.sql) from Run SQL Script prompt. Choose default schema. It will create a database called lahman.

![SQL script](images/MySQLWB.png)

Once it has been loaded you can execute the query "show databases" and it will show you a number of databases included lahman. See below

![SQL script](images/sqlworkbench1.png)

You can also issue the queries "use lahman" (i.e. select this database for use), followed by another query "show tables" and then click on the inspector icon to open the inspector for database where you can get a view like below that describes all tables. You can explore this view and also see all the columns in tables. see the two images below.

![SQL script](images/sqlworkbench.png)

![SQL script](images/sqlworkbench2.png)

**Very Important** : Remember to shutoff the RDS instance when you are not using it.  


## Step 3- Check initial Colab Connection

Run the Colab notebook [mlb.ipynb](mlb.ipynb) and ensure that you get the connection and the number of db tables correctly. Make sure that you update the database name, the username and the password.  

**Remember that you have to change the initial url to include your name correctly just as you did in assignment 0. Then go ahead and click on - open in colab**.

Note that if the button is not available - or the direct click from github does not work - you can also login to google colab and choose open (from github),  enable private repos and search for your repo in the list and open. 

If you do not have access to colab - then you can run the notebook locally through anaconda jupter server. See the instructions about [class python environment](https://github.com/vu-topics-in-big-data-2022/lectures/tree/main/python-environment). 

**Very Important** : Remember to shutoff the RDS instance when you are not using it.

## Step 4 - Implement Queries   

Implement all the SQL queries identified in mlb.ipynb . Record the answers in the mlb.ipynb and save it back to your repository.

The queries are

1. The number of all stars in allstarfull.
2. The most home runs in a season by a single player (using the batting table).
3. The playerid of the player with the most home runs in a season.
4. The number of leagues in the batting table.
5. Barry Bond's average batting average (playerid = 'bondsba01') where batting average is hits / at-bats. Note you will nead to cast hits to get a decimal: cast(h as real)
6. The teamid with the fewest hits in the year 2000 (ie., yearid = '2000'). Return both the teamid, and the number of hits. Note you can use ORDER BY column and LIMIT 1.
7. The teamid in the year 2000 (i.e., yearid = '2000')  with the highest average batting average. Return the teamid and the average. To prevent divsion by 0, limit at-bats > 0.
8. The number of all stars the giants (teamid = 'SFN') had in 2000.
9. The yearid which the giants had the most all stars.
10. The average salary in year 2000.
11. The number of positions (e.g., catchers, pitchers) that have average salaries greather than 2000000 in yearid 2000. You will need to join fielding with salaries. Also consider using a HAVING clause.
12. The number of errors Barry Bonds had in 2000. 
13. The average salary of all stars in 2000. Report answer as integer.
14. The average salary of non-all stars in 2000.  Report answer as integer.

You can test each query result using the  corresponding tests in the notebook.

To start solving this here are few hints. First understand the table and the data from [data/readme2012.txt](data/readme2012.txt) . Then execute the query describe tablename on mysql. you can describe other tables as well.

For example here is the response for 

```
describe batting
```
```
playerID	varchar(9)	NO	PRI	
yearID	int	NO	PRI	
stint	int	NO	PRI	
teamID	varchar(3)	YES		
lgID	varchar(2)	YES		
G	int	YES		
G_batting	int	YES		
AB	int	YES		
R	int	YES		
H	int	YES		
2B	int	YES		
3B	int	YES		
HR	int	YES		
RBI	int	YES		
SB	int	YES		
CS	int	YES		
BB	int	YES		
SO	int	YES		
IBB	int	YES		
HBP	int	YES		
SH	int	YES		
SF	int	YES		
GIDP	int	YES		
G_old	int	YES		
```

You will notice that playerid, yearid and stintid together forms a composite primary key.



### Hint 1:

To solve the third query I can first find the max and then create an inner join as follows

```
select * from batting INNER Join (select MAX(HR) as m from batting) as data ON batting.hr=data.m
```

### Hint 2:

Remember you can formulate the queries and execute them directly through workbench. Once that is done and you like the result, copy the query to the python notebook

Solve the other queries similarly.

## Step 5 - Implement Profiling for the queries

Profile the queries as shown in the notebook. Use the profiling instructions shown in brightspace.

# Grading Rubrics

- Each query is carries equal points. Query 1,3 and 9 are already solved. So you have to implement 11 queries.
- 4 points for implementing the profiling code that will run each test and record the time taken to execute. Save all answers in notebook and save it back to github
- When finished submit your url to brightspace for the assignment

```SQL
q1 = 'select count(*) from allstarfull;'
q3 = 'select playerid from batting INNER Join (select MAX(HR) as m from batting) as data ON batting.hr=data.m'
q9 = "SELECT yearid FROM allstarfull WHERE teamid = 'SFN' group by yearid having count(distinct playerid\)
      =(select max(nump) from (SELECT yearid, count(distinct playerid) as nump FROM allstarfull WHERE teamid = 'SFN' group by yearid) as innertable)"
```



