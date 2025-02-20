# INSTALL - VERIFY MYSQL ENTERPRISE EDITION  

## Introduction

2c) Verify the new MySQL Installation on Linux and import test databases
Objectives: 
•	understand better how MySQL connection works
•	install test databases for labs (world and employees)
•	have a look on useful statements

Server: serverB

Verify the new MySQL Installation on Linux and import test databases
Understand better how MySQL connection works
Install test databases for labs (world and employees)
Have a look on useful statements


Estimated Time: -- minutes

### Objectives

In this lab, you will:
* Discuss MySQL Connection 
* Connect to Ports 3306 and 3307
* Remove MySQL Community Installation and Iimport Databses
* Learn Useful SQL Statements

**Use ServerB for this lab**

### Prerequisites

This lab assumes you have:
* An Oracle account
* All previous labs successfully completed

## Task 1: Discuss MySQL Connection 

Please note that now you have 2 instances on the same server: one on 3306 and one on 3307. To connect to the correct one, always use the IP address, otherwise you may connect to wrong instance. Here we practice connecting to the right one (por t3310 is intentionally wrong). To help you understand “why” these check lines (not all are always available…)

- Current user:
- Connection:
- UNIX socket:
- TCP port:

## Task 2: 	Connect to Ports 3306 and 3307

1.  **shell>** 

    ```
    <copy>mysql -u root -p</copy>
    ```
2.  **mysql>**

    ```
    <copy>status</copy>
    ```
3.  **mysql>** 

    ```
    <copy>exit</copy>
    ```
4.  **shell>** 

    ```
    <copy>mysql -u root -p -P3306</copy>
    ```
5.  **mysql>** 

    ```
    <copy>status</copy>
    ```

6.  **mysql>**

    ```
    <copy>exit</copy>
    ```
	
7.  **shell>**

    ```
    <copy>mysql -uroot -p -h localhost -P3310</copy>
    ```

8.  **mysql>**

    ```
    <copy>status</copy>
    ```

9.  **mysql>**

    ```
    <copy>exit</copy>
    ```

10.  **shell>** 

    ```
    <copy>mysql -uroot -p -S /var/lib/mysql/mysql.sock</copy>
    ```

11.  **mysql>** 

    ```
    <copy>status</copy>
    ```

12.  **mysql>**

    ```
    <copy>exit</copy>
    ```
	
13.  **shell>** 

    ```
    <copy>mysql -uadmin -p -h 127.0.0.1 -P3307</copy>
    ```

14.  **mysql>** 

    ```
    <copy>status</copy>
    ```

15.  **shell>** 

    ```
    <copy>exit</copy>
    ```

16.  **shell>** 

    ```
    <copy>mysql -uadmin -p -h privateip-ServerB -P3307</copy>
    ```
    
17.  **mysql>** 

    ```
    <copy>status</copy>
    ```

18.  **mysql>**

    ```
    <copy>exit</copy>
    ```
19.  **mysql>** 

    ```
    <copy>mysql -uroot -p -S /mysql/temp/mysql.sock</copy>
    ```

20.  **mysql>** 

    ```
    <copy>status</copy>
    ```

21.  **mysql>** 

    ```
    <copy>exit</copy>
    ```

## Task 3: Remove MySQL Community Installation and Iimport Databses
1. Now that you understand how to connect, we can remove the MySQL Community installation

  **shell>** 

    ```
    <copy>sudo yum remove mysql-server</copy>

    ```
2.	Import the world database, that will be used later, from
    `c:\workshop\databases\world`
    
    You can do it with mysql client

  **shell>**

    ```
    <copy>mysql -uroot -p -S /mysql/temp/mysql.sock</copy>
    ``` 
3.	Import the employees demo database that is in /workshop/databases folder.

  **shell>** 
    ```
    <copy>cd /workshop/databases/employees</copy>
    ```

  **shell>** 
    ```
    <copy>mysql -uroot -p -P3307 -h 127.0.0.1 < ./employees.sql</copy>
    ```
## Task 4: Learn Useful SQL Statements

1. **shell>**

    ```
    <copy>mysql -uroot -p -h 127.0.0.1 -P 3307</copy>
    ```
2. **mysql>** 

    ```
    <copy>eSHOW VARIABLES LIKE "%version%";</copy>
    ```

3. **mysql>** 

    ```
    <copy>SELECT table&#95;name, engine FROM INFORMATION&#95;SCHEMA.TABLES WHERE engine <> 'InnoDB';</copy>
    ```
4. **mysql>** 

    ```
    <copy>SELECT table&#95;name, engine FROM INFORMATION&#95;SCHEMA.TABLES WHERE engine = 'InnoDB';</copy>
    ```
5. **mysqll>** 

    ```
    <copy>SELECT table&#95;name, engine FROM INFORMATION&#95;SCHEMA.TABLES where engine = 'InnoDB' and table&#95;schema not in ('mysql','information&#95;schema', 'sys');</copy>
    ```
6. **mysql>**

    ```
    <copy>SELECT ENGINE, COUNT(*), SUM(DATA&#95;LENGTH)/ 1024 / 1024 AS 'Data MB', SUM(INDEX&#95;LENGTH)/1024 / 1024 AS 'Index MB' FROM information&#95;schema.TABLEs group by engine;</copy>
    ```
7. **mysql>**

    ```
    <copy>SELECT table&#95;schema AS 'Schema', SUM( data&#95;length ) / 1024 / 1024 AS 'Data MB', SUM( index&#95;length ) / 1024 / 1024 AS 'Index MB', SUM( data&#95;length + index&#95;length ) / 1024 / 1024 AS 'Sum' FROM information&#95;schema.tables GROUP BY table&#95;schema ;</copy>
    ```
9. The “\G” is like “;” with a different way to show results 

  **mysql>** 

    ```
    <copy>SHOW GLOBAL VARIABLES\G</copy>
    ```
  **mysql>**

    ```
    <copy>SHOW GLOBAL STATUS\G</copy>
    ```
  **mysql>**

    ```
    <copy>SHOW FULL PROCESSLIST;</copy>
    ```
  **mysqll>** 

    ```
    <copy>SHOW ENGINE INNODB STATUS\G</copy>
    ```

## Learn More

*(optional - include links to docs, white papers, blogs, etc)*

* [URL text 1](http://docs.oracle.com)
* [URL text 2](http://docs.oracle.com)

## Acknowledgements
* **Author** - Perside Foster, MySQL Engineering
* **Contributors** -  Marco Carlessi, MySQL Engineering
* **Last Updated By/Date** - <Perside Foster, October 2021
