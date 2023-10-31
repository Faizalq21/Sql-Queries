# Sql-Queries
Sql queries from beginner to intermediate
--THIS IS A SINGLE LINE COMMENT 
/* THIS IS A MULTI LINE COMMENT.
IT CAN GO MULTIPLE LINES
THUS ENHANCES CODE READIBILITY  */


CREATE DATABASE AJ_SQL_DEMO_DATABASE;
USE DATABASE AJ_SQL_DEMO_DATABASE;
DROP DATABASE AJ_SQL_DEMO_DATABASE;

use schema public

---- to retreive only mentioned rows within query------
select * from "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER" LIMIT 1000;

---- to display all column names within table 
SHOW COLUMNS IN "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."STORE";

select * from "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER" limit 100;

----- to retreive count of all the rows within table----------
SELECT COUNT(*) FROM  "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER";
SELECT DISTINCT * FROM  "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER";

SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER" LIMIT 1000;

SHOW COLUMNS IN "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."STORE";

SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."ITEM" LIMIT 30;

----- to retreive filtered data by using where clause--------
SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER" WHERE C_FIRST_NAME = 'Joseph';

SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER" WHERE (C_BIRTH_YEAR = 1973 AND C_BIRTH_MONTH = 9);

--TELL ME THE DETAILS OF ALL C_CUSTOMER_SK WHO WAS BORN IN YEAR 1973,2003,1990,1945 AND IN THE 8TH MONTH AND HAVING EMAIL ID
--AND LAST NAME
SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER" WHERE C_BIRTH_YEAR IN (1973,2003,1990,1945) AND C_BIRTH_MONTH = 8 


SELECT DISTINCT C_BIRTH_YEAR FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."CUSTOMER";

SELECT TRUNC(TO_DATE('13-AUG-22','DD-MON-YY'), 'YEAR')
  --"SQL DATE TRUNC CLASS" FROM DUAL;

USE DATABASE "AJ_SQL_DEMO_DATABASE";

CREATE TABLE  "AGENTS" 
   (	
    "AGENT_CODE" CHAR(6) NOT NULL PRIMARY KEY, 
	"AGENT_NAME" CHAR(40), 
	"WORKING_AREA" CHAR(35), 
	"COMMISSION" NUMBER(10,2), 
	"PHONE_NO" CHAR(15), 
	"COUNTRY" VARCHAR2(25) 
	 );

-----inserting values within tables--------
INSERT INTO AGENTS VALUES ('A007', 'Ramasundar', 'Bangalore', '0.15', '077-25814763', '');
INSERT INTO AGENTS VALUES ('A003', 'Alex ', 'London', '0.13', '075-12458969', '');
INSERT INTO AGENTS VALUES ('A008', 'Alford', 'New York', '0.12', '044-25874365', '');
INSERT INTO AGENTS VALUES ('A011', 'Ravi Kumar', 'Bangalore', '0.15', '077-45625874', '');
INSERT INTO AGENTS VALUES ('A010', 'Santakumar', 'Chennai', '0.14', '007-22388644', '');
INSERT INTO AGENTS VALUES ('A012', 'Lucida', 'San Jose', '0.12', '044-52981425', '');
INSERT INTO AGENTS VALUES ('A005', 'Anderson', 'Brisban', '0.13', '045-21447739', '');
INSERT INTO AGENTS VALUES ('A001', 'Subbarao', 'Bangalore', '0.14', '077-12346674', '');
INSERT INTO AGENTS VALUES ('A002', 'Mukesh', 'Mumbai', '0.11', '029-12358964', '');
INSERT INTO AGENTS VALUES ('A006', 'McDen', 'London', '0.15', '078-22255588', '');
INSERT INTO AGENTS VALUES ('A004', 'Ivan', 'Torento', '0.15', '008-22544166', '');
INSERT INTO AGENTS VALUES ('A009', 'Benjamin', 'Hampshair', '0.11', '008-22536178', '');

-------using aggregate functions to rretreive data from table---------
SELECT * FROM AGENTS;

-------using aggregate functions to rretreive data from table---------
SELECT MIN("COMMISSION") AS minimum,MAX("COMMISSION") AS maximum FROM AGENTS
SELECT SUM("COMMISSION") FROM AGENTS

------ USING UPDATE TO UPDATE RECORDS WITHIN TABLE------
UPDATE  AGENTS
SET COUNTRY = 'IND'
WHERE AGENT_CODE = 'A010';

------- USING ALTER COMMAND TO ADD CONSTRAINT WITHIN COLUMN OF A TABLE-----
ALTER TABLE AGENTS
ALTER COLUMN PHONE_NO NOT NULL;

------- USING ALTER COMMAND TO DROP COLUMN WITHIN TABLE------
ALTER TABLE AGENTS
DROP COLUMN COUNTRY;

-------- ADDING COLUMN WITHIN TABLE USING ALTER COMMAND------
ALTER TABLE AGENTS
ADD EMAIL VARCHAR(100)

--- NUMBER OF AGENTS IN EACH WORKING AREA
SELECT WORKING_AREA,COUNT(DISTINCT AGENT_CODE) AS AGENTS_WORKING_AREA
FROM AGENTS
GROUP BY 1
ORDER BY 1 ;

----- To find description of the whole table-------
DESC TABLE AGENTS;
SHOW COLUMNS IN AGENTS;


CREATE TABLE  "CUSTOMER" 
   (	
    "CUST_CODE" VARCHAR2(6) NOT NULL PRIMARY KEY, 
	"CUST_NAME" VARCHAR2(40) NOT NULL, 
	"CUST_CITY" CHAR(35), 
	"WORKING_AREA" VARCHAR2(35) NOT NULL, 
	"CUST_COUNTRY" VARCHAR2(20) NOT NULL, 
	"GRADE" NUMBER, 
	"OPENING_AMT" NUMBER(12,2) NOT NULL, 
	"RECEIVE_AMT" NUMBER(12,2) NOT NULL, 
	"PAYMENT_AMT" NUMBER(12,2) NOT NULL, 
	"OUTSTANDING_AMT" NUMBER(12,2) NOT NULL, 
	"PHONE_NO" VARCHAR2(17) NOT NULL, 
	"AGENT_CODE" CHAR(6) NOT NULL REFERENCES AGENTS
);   

INSERT INTO CUSTOMER VALUES ('C00013', 'Holmes', 'London', 'London', 'UK', '2', '6000.00', '5000.00', '7000.00', '4000.00', 'BBBBBBB', 'A003');
INSERT INTO CUSTOMER VALUES ('C00001', 'Micheal', 'New York', 'New York', 'USA', '2', '3000.00', '5000.00', '2000.00', '6000.00', 'CCCCCCC', 'A008');
INSERT INTO CUSTOMER VALUES ('C00020', 'Albert', 'New York', 'New York', 'USA', '3', '5000.00', '7000.00', '6000.00', '6000.00', 'BBBBSBB', 'A008');
INSERT INTO CUSTOMER VALUES ('C00025', 'Ravindran', 'Bangalore', 'Bangalore', 'India', '2', '5000.00', '7000.00', '4000.00', '8000.00', 'AVAVAVA', 'A011');
INSERT INTO CUSTOMER VALUES ('C00024', 'Cook', 'London', 'London', 'UK', '2', '4000.00', '9000.00', '7000.00', '6000.00', 'FSDDSDF', 'A006');
INSERT INTO CUSTOMER VALUES ('C00015', 'Stuart', 'London', 'London', 'UK', '1', '6000.00', '8000.00', '3000.00', '11000.00', 'GFSGERS', 'A003');
INSERT INTO CUSTOMER VALUES ('C00002', 'Bolt', 'New York', 'New York', 'USA', '3', '5000.00', '7000.00', '9000.00', '3000.00', 'DDNRDRH', 'A008');
INSERT INTO CUSTOMER VALUES ('C00018', 'Fleming', 'Brisban', 'Brisban', 'Australia', '2', '7000.00', '7000.00', '9000.00', '5000.00', 'NHBGVFC', 'A005');
INSERT INTO CUSTOMER VALUES ('C00021', 'Jacks', 'Brisban', 'Brisban', 'Australia', '1', '7000.00', '7000.00', '7000.00', '7000.00', 'WERTGDF', 'A005');
INSERT INTO CUSTOMER VALUES ('C00019', 'Yearannaidu', 'Chennai', 'Chennai', 'India', '1', '8000.00', '7000.00', '7000.00', '8000.00', 'ZZZZBFV', 'A010');
INSERT INTO CUSTOMER VALUES ('C00005', 'Sasikant', 'Mumbai', 'Mumbai', 'India', '1', '7000.00', '11000.00', '7000.00', '11000.00', '147-25896312', 'A002');
INSERT INTO CUSTOMER VALUES ('C00007', 'Ramanathan', 'Chennai', 'Chennai', 'India', '1', '7000.00', '11000.00', '9000.00', '9000.00', 'GHRDWSD', 'A010');
INSERT INTO CUSTOMER VALUES ('C00022', 'Avinash', 'Mumbai', 'Mumbai', 'India', '2', '7000.00', '11000.00', '9000.00', '9000.00', '113-12345678','A002');
INSERT INTO CUSTOMER VALUES ('C00004', 'Winston', 'Brisban', 'Brisban', 'Australia', '1', '5000.00', '8000.00', '7000.00', '6000.00', 'AAAAAAA', 'A005');
INSERT INTO CUSTOMER VALUES ('C00023', 'Karl', 'London', 'London', 'UK', '0', '4000.00', '6000.00', '7000.00', '3000.00', 'AAAABAA', 'A006');
INSERT INTO CUSTOMER VALUES ('C00006', 'Shilton', 'Torento', 'Torento', 'Canada', '1', '10000.00', '7000.00', '6000.00', '11000.00', 'DDDDDDD', 'A004');
INSERT INTO CUSTOMER VALUES ('C00010', 'Charles', 'Hampshair', 'Hampshair', 'UK', '3', '6000.00', '4000.00', '5000.00', '5000.00', 'MMMMMMM', 'A009');
INSERT INTO CUSTOMER VALUES ('C00017', 'Srinivas', 'Bangalore', 'Bangalore', 'India', '2', '8000.00', '4000.00', '3000.00', '9000.00', 'AAAAAAB', 'A007');
INSERT INTO CUSTOMER VALUES ('C00012', 'Steven', 'San Jose', 'San Jose', 'USA', '1', '5000.00', '7000.00', '9000.00', '3000.00', 'KRFYGJK', 'A012');
INSERT INTO CUSTOMER VALUES ('C00008', 'Karolina', 'Torento', 'Torento', 'Canada', '1', '7000.00', '7000.00', '9000.00', '5000.00', 'HJKORED', 'A004');
INSERT INTO CUSTOMER VALUES ('C00003', 'Martin', 'Torento', 'Torento', 'Canada', '2', '8000.00', '7000.00', '7000.00', '8000.00', 'MJYURFD', 'A004');
INSERT INTO CUSTOMER VALUES ('C00009', 'Ramesh', 'Mumbai', 'Mumbai', 'India', '3', '8000.00', '7000.00', '3000.00', '12000.00', 'Phone No', 'A002');
INSERT INTO CUSTOMER VALUES ('C00014', 'Rangarappa', 'Bangalore', 'Bangalore', 'India', '2', '8000.00', '11000.00', '7000.00', '12000.00', 'AAAATGF', 'A001');
INSERT INTO CUSTOMER VALUES ('C00016', 'Venkatpati', 'Bangalore', 'Bangalore', 'India', '2', '8000.00', '11000.00', '7000.00', '12000.00', 'JRTVFDD', 'A007');
INSERT INTO CUSTOMER VALUES ('C00011', 'Sundariya', 'Chennai', 'Chennai', 'India', '3', '7000.00', '11000.00', '7000.00', '11000.00', 'PPHGRTS', 'A010');

SELECT * FROM CUSTOMER;

CREATE TABLE  "ORDERS1" 
   (
    "ORD_NUM" NUMBER(6,0) NOT NULL PRIMARY KEY, 
	"ORD_AMOUNT" NUMBER(12,2) NOT NULL, 
	"ADVANCE_AMOUNT" NUMBER(12,2) NOT NULL, 
	"ORD_DATE" DATE NOT NULL, 
	"CUST_CODE" VARCHAR2(6) NOT NULL REFERENCES CUSTOMER, 
	"AGENT_CODE" CHAR(6) NOT NULL REFERENCES AGENTS, 
	"ORD_DESCRIPTION" VARCHAR2(60) NOT NULL
   );

INSERT INTO ORDERS1 VALUES('200100', '1000.00', '600.00', '08/01/2008', 'C00013', 'A003', 'SOD');
INSERT INTO ORDERS1 VALUES('200110', '3000.00', '500.00', '04/15/2008', 'C00019', 'A010', 'SOD');
INSERT INTO ORDERS1 VALUES('200107', '4500.00', '900.00', '08/30/2008', 'C00007', 'A010', 'SOD');
INSERT INTO ORDERS1 VALUES('200112', '2000.00', '400.00', '05/30/2008', 'C00016', 'A007', 'SOD'); 
INSERT INTO ORDERS1 VALUES('200113', '4000.00', '600.00', '06/10/2008', 'C00022', 'A002', 'SOD');
INSERT INTO ORDERS1 VALUES('200102', '2000.00', '300.00', '05/25/2008', 'C00012', 'A012', 'SOD');
INSERT INTO ORDERS1 VALUES('200114', '3500.00', '2000.00', '08/15/2008', 'C00002', 'A008', 'SOD');
INSERT INTO ORDERS1 VALUES('200122', '2500.00', '400.00', '09/16/2008', 'C00003', 'A004', 'SOD');
INSERT INTO ORDERS1 VALUES('200118', '500.00', '100.00', '07/20/2008', 'C00023', 'A006', 'SOD');
INSERT INTO ORDERS1 VALUES('200119', '4000.00', '700.00', '09/16/2008', 'C00007', 'A010', 'SOD');
INSERT INTO ORDERS1 VALUES('200121', '1500.00', '600.00', '09/23/2008', 'C00008', 'A004', 'SOD');
INSERT INTO ORDERS1 VALUES('200130', '2500.00', '400.00', '07/30/2008', 'C00025', 'A011', 'SOD');
INSERT INTO ORDERS1 VALUES('200134', '4200.00', '1800.00', '09/25/2008', 'C00004', 'A005', 'SOD');
INSERT INTO ORDERS1 VALUES('200108', '4000.00', '600.00', '02/15/2008', 'C00008', 'A004', 'SOD');
INSERT INTO ORDERS1 VALUES('200103', '1500.00', '700.00', '05/15/2008', 'C00021', 'A005', 'SOD');
INSERT INTO ORDERS1 VALUES('200105', '2500.00', '500.00', '07/18/2008', 'C00025', 'A011', 'SOD');
INSERT INTO ORDERS1 VALUES('200109', '3500.00', '800.00', '07/30/2008', 'C00011', 'A010', 'SOD');
INSERT INTO ORDERS1 VALUES('200101', '3000.00', '1000.00', '07/15/2008', 'C00001', 'A008', 'SOD');
INSERT INTO ORDERS1 VALUES('200111', '1000.00', '300.00', '07/10/2008', 'C00020', 'A008', 'SOD');
INSERT INTO ORDERS1 VALUES('200104', '1500.00', '500.00', '03/13/2008', 'C00006', 'A004', 'SOD');
INSERT INTO ORDERS1 VALUES('200106', '2500.00', '700.00', '04/20/2008', 'C00005', 'A002', 'SOD');
INSERT INTO ORDERS1 VALUES('200125', '2000.00', '600.00', '10/10/2008', 'C00018', 'A005', 'SOD');
INSERT INTO ORDERS1 VALUES('200117', '800.00', '200.00', '10/20/2008', 'C00014', 'A001', 'SOD');
INSERT INTO ORDERS1 VALUES('200123', '500.00', '100.00', '09/16/2008', 'C00022', 'A002', 'SOD');
INSERT INTO ORDERS1 VALUES('200120', '500.00', '100.00', '07/20/2008', 'C00009', 'A002', 'SOD');
INSERT INTO ORDERS1 VALUES('200116', '500.00', '100.00', '07/13/2008', 'C00010', 'A009', 'SOD');
INSERT INTO ORDERS1 VALUES('200124', '500.00', '100.00', '06/20/2008', 'C00017', 'A007', 'SOD'); 
INSERT INTO ORDERS1 VALUES('200126', '500.00', '100.00', '06/24/2008', 'C00022', 'A002', 'SOD');
INSERT INTO ORDERS1 VALUES('200129', '2500.00', '500.00', '07/20/2008', 'C00024', 'A006', 'SOD');
INSERT INTO ORDERS1 VALUES('200127', '2500.00', '400.00', '07/20/2008', 'C00015', 'A003', 'SOD');
INSERT INTO ORDERS1 VALUES('200128', '3500.00', '1500.00', '07/20/2008', 'C00009', 'A002', 'SOD');
INSERT INTO ORDERS1 VALUES('200135', '2000.00', '800.00', '09/16/2008', 'C00007', 'A010', 'SOD');
INSERT INTO ORDERS1 VALUES('200131', '900.00', '150.00', '08/26/2008', 'C00012', 'A012', 'SOD');
INSERT INTO ORDERS1 VALUES('200133', '1200.00', '400.00', '06/29/2008', 'C00009', 'A002', 'SOD');

SELECT * FROM ORDERS1;

SHOW COLUMNS IN ORDERS1;

----- to display the length of character using len string function-------
SELECT LEN('ANAND') AS TOT_CHAR ;

-- SUBSTRING(string, start, length) using string function to display specific characters using parameters-----
SELECT SUBSTRING('ANANDJHA_1990@YAHOO.COM',-9,9) AS LEN_SUB_STRING;

--LTRIM/RTRIM AS left and right trimto remove spaces from LEFT AND RIGHT OF THE CHARACTERS AND DISPLAYING ITS LENGTH FOR DIFFERENCES------ 
SELECT LEN(LTRIM('      ANAND JHA')) AS LEFT_TRIMMED_STRING;
SELECT LEN(RTRIM('ANAND JHA      ')) AS TRIMMED_STRING;
SELECT LEN('      ANAND JHA') AS LEFT_TRIMMED_STRING;

SELECT RTRIM('ANAND JHA        ') AS RIGHT_TRIMMED_STRING;

-- REPLACE() FUNCTION --  TO REPLACE BLANK SPACE WITH SOMETHING WITHIN CHARACTERS-----
--REPLACE(string,old_string,new_string)
SELECT REPLACE('SQL CLASSES',' ','-') AS REPLACED_STRING;

--LOWERCASE/UPPERCASE IN SQL TO DISPLAY CHARACTERS IN DESIRED FORMAT YOU WANT------
SELECT UPPER('Kamal') as upper_name;
SELECT LOWER('KAMAL') as lower_name;

--USING INNER JOINS FOR JOINING CUSTOMERS, ORDERS & THEIR AGENTS TABLE AND CREATING MASTER TABLE as well displaying only records that match all three conditions-----
CREATE OR REPLACE TABLE CUST_ORDER_MASTER_TABLE_INNER_JOIN AS
SELECT cust.*,ord_num,ORD_AMOUNT,ADVANCE_AMOUNT,ORD_DATE,ORD_DESCRIPTION,agent_name,agt.phone_no AS agt_phone,commission
FROM CUSTOMER cust
INNER JOIN ORDERS odr ON cust. CUST_CODE = odr.CUST_CODE
INNER JOIN AGENTS agt ON cust.AGENT_CODE = agt.AGENT_CODE ;


------ TO GET DISTINCT COUNT FOR DIFFERENT COLUMNS WITHIN TABLE------
SELECT * FROM CUST_ORDER_MASTER_TABLE_INNER_JOIN;
select count(distinct cust_code) from CUST_ORDER_MASTER_TABLE_INNER_JOIN; --25 distinct customer
select count(distinct cust_name) from CUST_ORDER_MASTER_TABLE_INNER_JOIN; --25 distinct customer
select count(distinct agent_name) from CUST_ORDER_MASTER_TABLE_INNER_JOIN; --12 distinct agents

--- how many customer each agent has served using group by and order by---
SELECT AGENT_NAME,COUNT(DISTINCT CUST_CODE) AS CUST_SERVED
FROM CUST_ORDER_MASTER_TABLE_INNER_JOIN
GROUP BY 1
ORDER BY 1;

------ LEFT JOIN USE CASEE
--using left JOIN to retreive all CUSTOMERS & THEIR ORDER
CREATE OR REPLACE TABLE CUST_ORDER_MASTER_TABLE_LEFT_JOIN AS
SELECT cust.*,ord_num,ORD_AMOUNT,ADVANCE_AMOUNT,ORD_DATE,ORD_DESCRIPTION,agent_name,agt.phone_no AS agt_phone,commission
FROM CUSTOMER cust
LEFT JOIN ORDERS odr ON cust.CUST_CODE = odr.CUST_CODE
LEFT JOIN AGENTS agt ON cust.AGENT_CODE = agt.AGENT_CODE ;


SELECT * FROM CUST_ORDER_MASTER_TABLE_LEFT_JOIN;
select count(distinct cust_code) from CUST_ORDER_MASTER_TABLE_INNER_JOIN; --25 distinct customer
select count(distinct cust_name) from CUST_ORDER_MASTER_TABLE_INNER_JOIN; --25 distinct customer
select count(distinct agent_name) from CUST_ORDER_MASTER_TABLE_INNER_JOIN; --12 distinct agents

--- how many cust each agent has served
SELECT AGENT_NAME,COUNT(DISTINCT CUST_CODE) AS CUST_SERVED
FROM CUST_ORDER_MASTER_TABLE_INNER_JOIN
GROUP BY 1
ORDER BY 1;

create database "DEMODATABASE"
USE DATABASE "DEMODATABASE";

CREATE OR REPLACE TABLE AJ_WOMENS_CLOTHING_DATASET 
(
  ROW_NUM INT,
  CLOTHING_ID INT PRIMARY KEY,
  AGE INT,
  TITLE VARCHAR(100),
  REVIEW_TEXT VARCHAR(1000),
  RATING INT,
  RECOMMENDED_IND BOOLEAN,
  POS_FEEDBACK_COUNT INT,
  DIVISION_NAME STRING,
  DEPARTMENT_NAME STRING,
  CLASS_NAME STRING
);  


-- SUBSTRING(string, start, length) TO DISPLAY ONLY SPECIFIC NUMBER OF CHARACTERS WITHIN TABLE----
SELECT SUBSTRING('ANAND KUMAR JHA',3,2);

create or replace table Consumer_Complaints (
Date_Received VARCHAR,
Product_Name VARCHAR(30),
Sub_Product VARCHAR(50),
Issue VARCHAR(60),
Sub_Issue VARCHAR(50),
Consumer_Complaint_Narrative STRING,
Consumer_Pubic_Response STRING,
Company VARCHAR(100),
State_Name CHAR(4),
Zip_Code STRING,
Tags VARCHAR(50),
Consumer_Consent_Provided CHAR(25),
Submitted_Via STRING,
Date_Sent_To_Company STRING,
Company_Response_To_Consumer VARCHAR(60),
Timely_Response CHAR(4),
Consumer_Disputed CHAR(4),
Complaint_Id NUMBER(12,0) NOT NULL PRIMARY KEY)


SELECT * FROM CONSUMER_COMPLAINTS
SELECT * FROM CONSUMER_COMPLAINTS LIMIT 1000

----USING COUNT TO DISPLAY THE OVERALL COUNTS OF PRODUCT NAME WITHIN TABLE-----
select count(distinct(Product_Name)) from Consumer_Complaints where Company = 'Wells Fargo & Company' 

------ USING MIN TO FIND MINIMUM DATE WITHIN TABLE-----
SELECT MIN(DATE_RECEIVED) AS Min_Date from Consumer_Complaints

-------------------------Need the count of complaints for each product for all the companies which would chow products for each
--company and than other by grouping
SELECT Company, Product_Name, COUNT(Complaint_Id) as Total_Complaints 
From Consumer_Complaints
Group By 1,2
Order by 1,2 DESC

SELECT Company,Product_Name, COUNT(Complaint_Id) as Total_Complaints
from Consumer_Complaints  ---Using having clause to filter individually FOR AGGREGATED COLUMN AND COUNT TO DISPLAY OVERALL COUNT---
Group by 1,2
Having Total_Complaints > 100
Order by 1,2

----Where clause will work with rows individually and having with aggregate to filter--
---HERE BOTH HAVING CLAUSE IS USED IN CONJUNCTION WITH GROUP BY CLAUSE AND WHERE CLAUSE IS USED TO FILTER ROWS WITHOUT AGGREGATION
SELECT Company,Product_Name, COUNT(DISTINCT Complaint_Id) as Total_Complaints 
from Consumer_Complaints
Where Submitted_Via = 'Phone'
Group By 1,2
Having COUNT(Complaint_Id) > 100
Order BY 3 DESC

--------------------- Using In with where clause and using having group by order by to filter data and display specific columns mentioned within select-------------------------
SELECT Company,Product_Name, COUNT(DISTINCT Complaint_Id) as Total_Complaints 
from Consumer_Complaints
Where Submitted_Via = 'Phone' AND State_Name IN ('VA','CA','NY','GA','CT')
Group By 1,2 
Having COUNT(Complaint_Id) > 10
Order BY 3 DESC


------------------Using Like operator to display specific alphabets within characters as % specifies it-------------

SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF10TCL"."ITEM" WHERE I_ITEM_ID LIKE '%EF%'  ----- Any where EF present between 
--characters as % specifies it
SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF10TCL"."ITEM" WHERE I_ITEM_ID LIKE 'EF%'   ----- will display characters if EF 
--present at start of character 
SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF10TCL"."ITEM" WHERE I_ITEM_ID LIKE '%EF'   ----- will display characters if EF present
--at end of character
SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF10TCL"."ITEM" WHERE I_ITEM_ID LIKE '________EF%'  -----will display EF if present 
--after mentioned characters 
SELECT * FROM "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF100"."LINEITEM" WHERE L_COMMENT LIKE '%carefully%' ---- will display whole character present within comments

----------------------- this would give specific columns as per like operator and group by mentioned as well aggregate AND SORT USING ORDER BY ----------------------------------------                             
SELECT L_SHIPMODE, COUNT(DISTINCT L_ORDERKEY) AS TOtal_Orders
From "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF100"."LINEITEM"
WHERE L_COMMENT LIKE '%carefully%'
GROUP BY 1
ORDER BY 1

---------------------------------------------------------------CASE Statement-------------------------------------------------------------------------------

Use "AJ_SQL_DEMO_DATABASE"

Create or replace table Employee(
EmployeeID INT Primary key,
EmployeeName VARCHAR(100) NOT NULL,
Gender VARCHAR(1) NOT NULL,
Statecode VARCHAR(2) NOT NULL,
Salary Number(10,2) NOT NULL)

describe table EMPLOYEE

INSERT INTO Employee VALUES
(212, 'Vikas', 'M', 'IN', 5000.0000),
(201, 'Jerome', 'M', 'FL', 83000.0000),
(202, 'Ray', 'M', 'AL', 88000.0000),
(203, 'Stella', 'F', 'AL', 76000.0000),
(204, 'Gilbert', 'M', 'Ar', 42000.0000),
(205, 'Edward', 'M', 'FL', 93000.0000),
(206, 'Ernest', 'F', 'Al', 64000.0000),
(207, 'Jorge', 'F', 'IN', 75000.0000),
(208, 'Nicholas', 'F', 'Ge', 71000.0000),
(209, 'Lawrence', 'M', 'IN', 95000.0000),
(210, 'Salvador', 'M', 'Co', 75000.0000)

SELECT * FROM EMPLOYEE

----------------------------------- This will create CASE statement with select clause to just display it for reports as temporary COLUMN---------------------
SELECT *,
CASE
    WHEN SALARY >= 10000 AND SALARY < 30000 THEN 'Data Analyst Trainee'
    WHEN SALARY >= 30000 AND SALARY < 50000 THEN 'Data Analyst'
    WHEN SALARY >= 50000 AND SALARY < 80000 THEN 'Consultant'
    WHEN SALARY >= 80000 AND SALARY < 100000 THEN 'Senior Consultant'
    WHEN SALARY > 100000 THEN 'Senior Folks'
ELSE 'Contractor'
END AS Designation
From Employee

select * from employee
----------------------------------- This CASE statement will create a table or bucket to send reports to manager with designation column-------------------------------------
CREATE OR REPLACE TABLE Employee_Bucket AS
SELECT *,
CASE
    WHEN SALARY >= 10000 AND SALARY < 30000 THEN 'Data Analyst Trainee'
    WHEN SALARY >= 30000 AND SALARY < 50000 THEN 'Data Analyst'
    WHEN SALARY >= 50000 AND SALARY < 80000 THEN 'Consultant'
    WHEN SALARY >= 80000 AND SALARY < 100000 THEN 'Senior Consultant'
    WHEN SALARY > 100000 THEN 'Senior Folks'
ELSE 'Contractor'
END AS Designation
From Employee

SELECT * FROM EMPLOYEE_BUCKET
grant select on Employee_Bucket to public;  ---------- to grant or available for everyone within team or role as admin, manager, etc depend on access to table

-----------------------------------Using CASE and Order by together if gender 'F' AND 'M' then it will arrange then will sort in descending and use case within order by clause-------
Select EmployeeName,Gender,Salary
 from Employee
 ORDER BY  CASE Gender WHEN 'F' THEN Salary END DESC ,
           CASE WHEN Gender = 'M' THEN Salary END DESC;
           
 ------- Using CASE with IN operator with multiple conditions --------------------------
 Select *, CASE 
WHEN SALARY IN (42000,64000,71000) THEN 'Medium Salary'
WHEN SALARY IN (75000,76000,83000) Then 'Average Salary'
When SALARY IN (88000,93000, 95000) THEN 'Highest salary'
ELSE 'Less salary'
End as Salary_type
From Employee

---SALARY BUCKET CREATION USING CASE STATMENT

SELECT *,
CASE
    WHEN SALARY >= 10000 AND SALARY <= 20000 THEN '10k-20k-Sal'
    WHEN SALARY > 20000 AND SALARY <= 30000 THEN '20k-30k-Sal'
    WHEN SALARY > 30000 AND SALARY <= 40000 THEN '30k-40k-Sal'
    ELSE 'Beond40kSal'
END AS SALARY_BUCKET    
FROM Employee

--  To view What's my current user, role, warehouse, database, etc?
SELECT CURRENT_USER();
SELECT CURRENT_ROLE();
SELECT CURRENT_WAREHOUSE();
SELECT CURRENT_DATABASE();

--How do I use a specific role, warehouse, database, etc?
SHOW ROLES;
USE ROLE {role};

-----To use specific warehouse
SHOW WAREHOUSES;
USE WAREHOUSE {warehouse};

------ To use specific database and display database
SELECT * FROM INFORMATION_SCHEMA.DATABASES;
USE DATABASE {database};

--How do I set my default warehouse?
--Determine your current warehouse:
SELECT CURRENT_WAREHOUSE();


--Alter your default warehouse so you dont need to change it again
ALTER USER {username} SET DEFAULT_WAREHOUSE = {warehouse};

ALTER USER analyticswithanand SET DEFAULT_WAREHOUSE = demo_warehouse;
--How do I create a new warehouse?
--Check if the warehouse already exists:
SHOW WAREHOUSES;
DESCRIBE WAREHOUSE demo_warehouse;

--Create (or replace) the warehouseusing sql query---
CREATE OR REPLACE WAREHOUSE ANALYTICS
    WITH WAREHOUSE_SIZE = 'X-SMALL'
    MAX_CLUSTER_COUNT = 1
    AUTO_SUSPEND = 300
    AUTO_RESUME = TRUE
    INITIALLY_SUSPENDED = TRUE;
    

--However, with a simple SQL query you can set whatever timeout you need. The timeout value is in seconds.
ALTER WAREHOUSE IF EXISTS {warehouse} SET AUTO_SUSPEND = {seconds};

ALTER WAREHOUSE IF EXISTS ANALYTICS SET AUTO_SUSPEND = 3600;

--How do I create a new database user?
SHOW ROLES;
USE ROLE ACCOUNTADMIN;
-- USE ROLE SECURITYADMIN;
CREATE USER {username} PASSWORD = '{password}' MUST_CHANGE_PASSWORD = TRUE;

-- Grant usage on a database and warehouse to a role
SHOW GRANTS TO ROLE {role};
GRANT USAGE ON WAREHOUSE {warehouse} TO ROLE {role};
GRANT USAGE ON DATABASE {database} TO ROLE {role};

--How to create a role that allows 'create warehouse'
use database analytics;
use warehouse analytics;
create role administrator;
grant create warehouse on account to role ADMINISTRATOR;
grant usage on database ANALYTICS to role ADMINISTRATOR;
show grants on role ADMINISTRATOR;
grant role ADMINISTRATOR to user <username>;
show grants on user <username>;

--Snowflake provides a full set of SQL commands for managing users and security. 
-- These commands can only be executed by users who are granted roles that have the OWNERSHIP privilege on the managed object. 
--This is usually restricted to the ACCOUNTADMIN and SECURITYADMIN roles.

create database DEMO_DATABASE
use database "DEMO_DATABASE";

-- Copy only table structure, no data copying:
create or replace table CUSTOMERS_COPY LIKE "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1000"."CUSTOMER";

DESCRIBE TABLE CUSTOMERS_COPY;
describe table CUSTOMERS_COPY_method1;
SELECT * FROM CUSTOMERS_COPY;
SELECT * FROM CUSTOMERS_COPY_method1;

--Copy both the entire table structure and all the data inside:
--method 1
CREATE OR REPLACE TABLE CUSTOMERS_COPY_method1 clone AJ_customer;
CREATE OR REPLACE TABLE CUSTOMERS_COPY_method3 clone "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1000"."LINEITEM";

select * from CUSTOMERS_COPY_method1;
DELETE FROM CUSTOMERS_COPY_method1 WHERE CUST_NAME = 'anand';

--method 2
CREATE OR REPLACE TABLE CUSTOMERS_COPY_method2 AS
SELECT * from "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1000"."ORDERS" limit 1000;
select * from CUSTOMERS_COPY_METHOD2

CREATE OR REPLACE TABLE AJ_CUST_TRUNC_TEST AS
SELECT * FROM AJ_customer;

SELECT * FROM AJ_CUST_TRUNC_TEST;

--Copy entire table structure along with particular data within table:
create OR REPLACE table AJ_PARTS_COPY as 
select * from "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1000"."PART" 
where P_TYPE = 'ECONOMY ANODIZED COPPER';

--Copy only particular columns into new table along with particular data set:
create OR REPLACE table AJ_PARTS_DETAILS_COPY as 
select P_PARTKEY,P_NAME ,P_MFGR,P_BRAND,P_SIZE,P_RETAILPRICE
from  "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1000"."PART";
--where category = 2;

SELECT * FROM AJ_PARTS_DETAILS_COPY;

-- Query the 
-- GET_DDL function to retrieve a DDL statement that could be executed to recreate the specified table. 
--- The statement includes the constraints currently set on a table.
select get_ddl('table', 'AJ_PARTS_DETAILS_COPY');

--The Snowflake TRUNCATE Table command is a DML(Data Manipulation Language) command that is used to add(insert),delete (delete),and alter(update) data in a database

use database "DEMO_DATABASE";

DROP TABLE aj_retirement;

undrop table aj_retirement ;

describe table aj_retirement;

CREATE or replace TABLE aj_retirement
(
	 source_name VARCHAR(6)   
	,process_name VARCHAR(3)   
	,val_dt VARCHAR(10)   
	,run_dt VARCHAR(10)   
	,line_indicator VARCHAR(4)    
	,total_record_count VARCHAR(12)   
	,total_record_amount VARCHAR(18)  
	,sel_record_count VARCHAR(12)   
	,sel_record_amount VARCHAR(18)   
	,byp_record_count VARCHAR(12)   
	,byp_record_amount VARCHAR(18)   
	,zero_record_count VARCHAR(12)   
	,zero_record_amount VARCHAR(18)   
	,created_date TIMESTAMP WITHOUT TIME ZONE NOT NULL 
);

DROP TABLE aj_retirement;

undrop table aj_retirement ;

describe table aj_retirement;
SELECT * FROM AJ_RETIREMENT; 
DESCRIBE TABLE AJ_RETIREMENT;

-- Query the 
-- GET_DDL command to get the query used to create table that could be executed to recreate the specified table. 
--- The statement includes the constraints currently set on a table.
select get_ddl('table', 'AJ_RETIREMENT');


SHOW COLUMNS IN AJ_RETIREMENT;

-- It is even use to copy someone’s table who is not on job or on leave  
-- GET_DDL function to retrieve a DDL statement that could be executed to recreate the specified table. 
--- The statement includes the constraints currently set on a table.
select get_ddl('table', 'AJ_PARTS_DETAILS_COPY');

--The Snowflake TRUNCATE Table command is a DML(Data Manipulation Language) command that is used to add(insert),delete (delete),and alter(update) data in a database.
Truncate table aj_retirement         ---- to only delete data within table
Delete from  AJ_customer
Where AGE = 22 and  CUST_NAME = 'MANISHA';                          ----- to delete specific data within table
DROP TABLE aj_retirement;                           --- to delete whole table along with structure
undrop table aj_retirement ;                 --- to bring the data back deleted via drop command but within 24 hours 

----- using alter command to add columns or constraints within columns
ALTER TABLE AJ_customer
ADD PRIMARY KEY (cust_id);

ALTER TABLE AJ_customer
ADD UNIQUE(cust_id);

ALTER TABLE AJ_customer
ADD COLUMN AGE INT;

----- using update to add data within rows 
UPDATE retirement.aud_copy_update
SET created_date = '05-05-2022' WHERE row_num >=146 and row_num <= 174

UPDATE retirement.aud_copy_update
SET created_date = '05-06-2022' WHERE row_num =175

-- sql date functions

-- GET CURRENT DATE
SELECT CURRENT_DATE;

-- GET CURRENT TIME AND DATE
SELECT CURRENT_TIMESTAMP;

-- GET CURRENT DATE
SELECT CURRENT_TIME;
 
----- CONVERT TIMEZONE will convert time into utc----------------
select convert_timezone('UTC',CURRENT_TIMESTAMP) AS UTC_TIMEZONE

--setting time to europe
SELECT CONVERT_TIMEZONE('Europe/Dublin', CURRENT_TIMESTAMP) AS Ireland_Time;


-- CONVERT DATE TO SUBSEQUENT 4 MONTHS AHEAD by using ADD_MONTHS---
SELECT ADD_MONTHS(CURRENT_DATE,4) as DATE_AFTER_4_MONTHS;

use database "AJ_SQL_DEMO_DATABASE";

--------This means that any subsequent timestamp data used in the session will be treated as having no time zone information.
alter session set timestamp_type_mapping = timestamp_ntz;

--------This would create table called "ts_test" with a single column named "ts" of the data type "timestamp". This table will be used to store timestamp data.
create or replace table ts_test(ts timestamp);

desc table ts_test;

--This creating a new table called "ts_test" with the same column name "ts", but this time the data type is "timestamp_ltz", 
---which stands for "timestamp with local time zone". This table will store timestamp data with time zone information.
create or replace table ts_test(ts timestamp_ltz);
describe table ts_test

-----This would set timezone within snowflake as mentioned within query
alter session set timezone = 'Europe/Dublin';

insert into ts_test values('2014-01-01 01:00:00');
insert into ts_test values('2014-01-02 01:00:00 +00:00');

-- Note that the time for January 2nd is 02:42:00 in Dublin (which is 01:00 in UTC)

select * from ts_test;

---- get hour within column
select ts, hour(ts) from ts_test;

--- this would convert utc timezone  to Europe/Warsaw as mentioned using convert_timezone and timestamp_ntz will give date without timezone
select convert_timezone('Europe/Warsaw', 'UTC', '2019-01-01 00:00:00'::timestamp_ntz) as conv;
select convert_timezone('Europe/Dublin', 'UTC', '2023-06-12 01:00:00'::timestamp_ntz) as conv;

SELECT
    months_between('2019-03-15'::date,
                   '2019-02-15'::date) as monthsbetween1,
    months_between('2019-03-31'::date,
                   '2020-02-28'::date) as monthsbetween2;


-- Get 3 MONTHS BACK DATE & coverting to string as want in desired format
SELECT TO_CHAR(ADD_MONTHS(CURRENT_DATE,-3),'DD-MM-YYYY') as DATE_BEFORE_3_MONTHS;
SELECT TO_VARCHAR(ADD_MONTHS(CURRENT_DATE,-3),'MM-DD-YYYY') as DATE_BEFORE_3_MONTHS;

-- GET YR FROM DATE using DATE_TRUNC as well the whole format of date but just the starting day
SELECT DATE_TRUNC('YEAR',CURRENT_DATE) AS YR_FROM_DATE;

-- GET MTH FROM DATE using DATE_TRUNC
SELECT DATE_TRUNC('MONTH',CURRENT_DATE) AS MTH_FROM_DATE;

-- GET DAY FROM DATE using DATE_TRUNC
SELECT DATE_TRUNC('DAY',CURRENT_DATE) AS DAY_FROM_DATE;

-- GET WEEK FROM DATE using DATE_TRUNC
SELECT DATE_TRUNC('WEEK',CURRENT_DATE) AS WEEK_FROM_DATE;

---------- This query would give month, day, hour, second, minute within current_timestamp
select day(current_timestamp() ) ,
  hour( current_timestamp() ) ,
  second(current_timestamp()) ,
  minute(current_timestamp()) ,
  month(current_timestamp());

SELECT WEEK(CURRENT_DATE) AS WEEK_FROM_START_OF_THE_YEAR;   --- this would give ongoing week within year for current_date
SELECT MONTH(CURRENT_DATE) AS MNTH_FROM_START_OF_THE_YEAR;
SELECT DAY(CURRENT_DATE) AS MNTH_OF_CURRENT_MONTH;

-- GET LAST DAY OF current MONTH
select last_day(current_date) as last_day_curr_month;

-- GET LAST DAY OF PREVIOUS MONTH
SELECT LAST_DAY(CURRENT_DATE - INTERVAL '1 MONTH') AS LAST_DAY_PREV_MNTH;

----Get last day of previous 2 month + add a day
SELECT LAST_DAY(CURRENT_DATE - INTERVAL '2 MONTHS') + INTERVAL '1 DAY' AS FIRST_DAY;

SELECT QUARTER(CURRENT_DATE) AS QTR;

SELECT EXTRACT(YEAR FROM CURRENT_DATE) AS YR;
SELECT EXTRACT(MONTH FROM CURRENT_DATE) AS MTH;
SELECT EXTRACT(DAY FROM CURRENT_DATE) AS DAY;

--- this would give quarter of the date mentioned
select QUARTER(to_date('2022-08-24'));

---- convert varchar to date using to_date with mm-dd-yyyy as format mentioning in which format the date is mandatory but results would be displayed in yyyy-mm-dd format only------
SELECT to_date('08-23-2022','mm-dd-yyyy');

SELECT TO_DATE('1993-08-17') AS DATE;
SELECT to_date('08-23-2022') AS DATE

--- this would convert the string to date first than again to string into desired format using to_char
SELECT TO_CHAR(TO_DATE('1993-08-17'),'DD-MM-YYYY') AS DATE_DD_MM_YYYY; --THIS WILL BE HIGHLY USED

SELECT TO_CHAR(TO_DATE('1993-08-17'),'MM-YYYY') AS MM_YYYY;

----get month name as mentioned
SELECT TO_CHAR(TO_DATE('1993-08-17'),'MON-YYYY') AS MON_YYYY;

-- get month name and year
SELECT TO_CHAR(TO_DATE('1993-08-17'),'MON-YY') AS DATE_MON_YY;

---get day of week within date converted to string
SELECT TO_CHAR(TO_DATE('1993-08-17'),'DY') AS DATE_DAY;

---- get date in varchar format along with day of week
SELECT TO_CHAR(TO_DATE('1993-08-17'),'DY-DD-MM-YYYY') AS DATE_DAY;

---- get dayname within week for mentioned day
SELECT DAYNAME ('1993-08-23');
SELECT DAYNAME (CURRENT_DATE);

---- get date converted to string within format mentioned 
SELECT TO_CHAR(TO_DATE('1993-08-17'),'YYYY-DD') AS DATE;

SELECT TO_CHAR(TO_DATE('1993-08-17'),'DD-MM') AS DATE;

select MONTH(CURRENT_DATE) as month
SELECT EXTRACT(MONTH FROM CURRENT_DATE) AS MTH;

----add months within date to get desired date using add_months function
SELECT ADD_MONTHS(CURRENT_DATE,-3) AS DATE_3_MNTHS_BACK;
SELECT ADD_MONTHS(CURRENT_DATE,5) AS DATE_5_MNTHS_AHEAD;

--- get day differnce between two dates using datediff function
select datediff('day', '2022-06-01',CURRENT_DATE);
select datediff('day', '2022-07-23','2023-07-19');

--- get month & year differnce between two dates using datediff function
select datediff('MONTH', '2021-06-01',CURRENT_DATE);
select datediff('YEAR', '2014-06-01',CURRENT_DATE);

----- add day, month, year within date usinf dateadd function
select dateadd('day',-23,'2022-06-01');
select dateadd('month',-2,'2022-06-01');
select dateadd('year',-5,'2022-06-01');

select WEEK(CURRENT_DATE); -- FROM 1ST JAN 2023 HOW MNAY EEKS HAVE SURPASSED
select MONTH(CURRENT_DATE); -- -- FROM 1ST JAN 2023 HOW MNAY MONTHS HAVE SURPASSED

select datediff('MONTH', '2022-06-01',CURRENT_DATE);
select datediff('YEAR', '2014-06-01',CURRENT_DATE);

-----------------------------------------------------------------String Functions---------------------------------------------------------------------

Use AJ_SQL_DEMO_DATABASE

 CREATE OR REPLACE TABLE AGENTS(
 AGENT_CODE CHAR(6) NOT NULL PRIMARY KEY,
 AGENT_NAME CHAR(48),
 WORKING_AREA CHAR(35),
 COMMISSION NUMBER(10,2) DEFAULT 0.05,
 PHONE_NO CHAR(15),
 COUNTRY VARCHAR(25))
 
 INSERT INTO AGENTS VALUES
 ('A007','Ramasundar','Bangalore',0.15,'077-25814763','')
 
 insert into agents(AGENT_CODE,AGENT_NAME,WORKING_AREA)
 VALUES('A110','ANAND','GERMANY')
 
 INSERT INTO AGENTS VALUES ('A003', 'Alex ', 'London', '0.13', '075-12458969', '');
INSERT INTO AGENTS VALUES ('A008', 'Alford', 'New York', '0.12', '044-25874365', '');
INSERT INTO AGENTS VALUES ('A011', 'Ravi Kumar', 'Bangalore', '0.15', '077-45625874', '');
INSERT INTO AGENTS VALUES ('A010', 'Santakumar', 'Chennai', '0.14', '007-22388644', '');
INSERT INTO AGENTS VALUES ('A012', 'Lucida', 'San Jose', '0.12', '044-52981425', '');
INSERT INTO AGENTS VALUES ('A005', 'Anderson', 'Brisban', '0.13', '045-21447739', '');
INSERT INTO AGENTS VALUES ('A001', 'Subbarao', 'Bangalore', '0.14', '077-12346674', '');
INSERT INTO AGENTS VALUES ('A002', 'Mukesh', 'Mumbai', '0.11', '029-12358964', '');
INSERT INTO AGENTS VALUES ('A006', 'McDen', 'London', '0.15', '078-22255588', '');
INSERT INTO AGENTS VALUES ('A004', 'Ivan', 'Torento', '0.15', '008-22544166', '');
INSERT INTO AGENTS VALUES ('A009', 'Benjamin', 'Hampshair', '0.11', '008-22536178', '');

SELECT * FROM AGENTS;

/* The SUBSTRING () function returns the position of a string or binary value from the complete string, 
starting with the character specified by substring_start_index. If any input is null, null is returned */

--Example 1: Get the substring from a specific string in Snowflake
select substring(' ANAND KUMAR JHA', 1, 7);
select substring(' ANAND KUMAR JHA', 0, 7);
select substr('Raja Ram',0,3);
select substr('Raja Ram',3);                  ----- this would give all characters starting from 3rd index

select substring('ANAND KUMAR JHA', -7);      ----- get characters from behind

--Example 2: Get the substring from a specific string by using table data
select AGENT_CODE,AGENT_NAME,substring(AGENT_NAME,0,2) AS AGENT_INITIALS from agents;

/* To get a specific substring from an expression or string. 
You can also use the substring function if you want to get the substrings in reverse order from the strings. */

-- If you use the substrings in reverse order, use the starting index as a negative value.
select AGENT_CODE,AGENT_NAME,substring(AGENT_NAME,-3,3) AS NAME_BACKWARDS from agents;

/*
Snowflake CAST is a data-type conversion command. Snowflake CAST works similar to the TO_datatype conversion functions. 
If a particular data type conversion is not possible,
it raises an error. Let’s understand the Snowflake CAST in detail via the syntax and a few examples.
*/

select cast('1.6845' as decimal(6,2));   ----here the 1st parameter is precision like how much length of datatype you want to convert and 2nd parameter is 
                                         ----how many decimals you want which is scale.
select '1.6845'::decimal(6,1);     ---- here precision is 1 so the output returned is rounded value as 1.7
SELECT CAST('123' AS INT)

select cast('10-Sep-2021' as timestamp);      ---- convert string to timestamp using cast

-- When the provided precision is insufficient to hold the input value, the Snowflake CAST command raises an error as follows:
select cast('123.12' as number(6,3));
--Here, precision is set as 4 but the input value has a total of 5 digits, thereby raising the error.

--TRY_CAST( <source_string_expr> AS <target_data_type> )
select try_cast('05-Mar-2016' as timestamp);

--The Snowflake TRY_CAST command returns NULL as the input value 
--has more characters than the provided precision in the target data type.
select try_cast('ANAND' as char(4));

--trim function to eliminate characters within columns
select trim('❄-❄ABC-❄-', '❄-') as trimmed_string;      ---- using TRIM along with parameter to delete from left as well right
select trim('❄-❄ABC-❄-', '') as trimmed_string;        ----this wont delete as mentioned parameter is not within character
SELECT TRIM('********T E S T I N G 1 2 3 4********','*') AS TRIMMED_SPACE;   --using TRIM along with parameter to delete from left as well right

--ltrim
select ltrim('#000000123', '0#');                         ----- will delete characters only from left
select ltrim('#0000AISHWARYA', '0#');
select ltrim('      ANAND JHA', '');

--RTRIM
select rtrim('$125.00', '0.');
select rtrim('ANAND JHA*****', '*');

--To remove the white spaces or the blank spaces from the string TRIM function can be used. 
--It can remove the whitespaces from the start and end both.
select TRIM('  Snwoflake Space Remove  ', ' ');

--To remove the first character from the string you can pass the string in the RTRIM function.
select LTRIM('Snowflake Remove  ', 'S');
--To remove the last character from the string you can pass the string in the RTRIM function.
select RTRIM('Snwoflake Remove  ', 'e');

select BTRIM('  Snwoflake Space Remove  ', ' ');

--LENGTH FUNCTION is used to find length within column
SELECT LEN(trim('  Snowflake Space Remove  ')) as length_string;  --- here trim will eliminate extra spaces and length will find length of column  
SELECT LENGTH(trim('  Snowflake Space Remove  ')) as length_string;

--concat function to merge characters or coulmns
select * from agents;

SELECT CONCAT('KA', ', ', 'India') as state_country;  

SELECT *,concat(AGENT_CODE, '-', AGENT_NAME) AS agent_details from agents;    --- merging 2 columns with separator using separator
 
--Snowflake CONCAT_WS Function
/* The concat_ws function concatenates two or more strings, or concatenates two or more binary values 
and adds separator between those strings.
The CONCAT_WS operator requires at least two arguments, and uses the first argument to separate all following arguments

Following is the concat_ws function syntax
CONCAT_WS( <separator> , <expression1> [ , <expressionN> ... ] ) */

SELECT CONCAT_WS('-', 'KA','India') as state_country;

/*
Snowflake Concat Operator (||)
The concatenation operator concatenates two strings on either side of the || symbol and returns the concatenated string. 
The || operator provides alternative syntax for CONCAT and requires at least two arguments.

For example,
*/
select 'Nested' || ' CONCAT' || ' example!' as Concat_operator;


--Handling NULL Values in CONCAT function and the Concatenation operator
--For both the CONCAT function and the concatenation operator,
--if one or both strings are null, the result of the concatenation is null.
--For example,

select concat('Bangalore, ', NULL) as null_example;
select 'Bangalore, '|| NULL as null_example;

--how to handle it?
select concat('Bangalore ', NVL(NULL,'')) as null_example;
select 'Bangalore'|| NVL(NULL, '') as null_example;

-- REVERSE IN STRING to reverse the character
select reverse('Hello, world!');

-- SPLIT function to split characters or columns using a parameter or separator
select split('127.0.0.1', '.');  
SELECT SPLIT('ANAND-KUMAR-JHA','-');

-----split_part function to split as per index.
select  0, split_part('11.22.33', '.',  0);    ---- using split_part to split as per index of column or characters.

select split_part('aaa--bbb-BBB--ccc', '--',1);
select split_part('aaa--bbb-BBB--ccc', '--',2);
select split_part('aaa--bbb-BBB--ccc', '--',3);
select split_part('aaa--bbb-BBB--ccc', '--',4);

---- Here concat is merging 2 columns but split will split columns by operator or parameter.
SELECT split(AGENT_DETAILS, '-')
FROM (
SELECT *,concat(AGENT_CODE, '-', AGENT_NAME) AS agent_details    
  from agents );
  

SELECT lower('India Is My Country') as lwr_strng;
SELECT UPPER('India Is My Country') as upr_strng;

--REPLACE COMMAND to replace overall space within character or column or sometimes using parameter to remove only specififc characters.
-- REPLACE( <subject> , <pattern> [ , <replacement> ] )

select REPLACE( '   ANAND KUMAR JHA   ' ,' ','*');
select REPLACE( '   ANAND KUMAR JHA   ' ,' '); -- 

SELECT REPLACE('   T  E S T I N G 1 2 3 4   ',' ')

------------------------------------------------------Using Regular Expression(Reg_Exp)--------------------------------------------------------------------
use AJ_SQL_DEMO_DATABASE
create or replace table like_ex(subject varchar(20));
insert into like_ex values
    ('John  Dddoe'),
    ('Joe   Doe'),
    ('John_down'),
    ('Joe down'),
    ('Elaine'),
    (''),    -- empty string
    (null);

select subject
    from like_ex
    where subject like '%Jo%oe%'      ---here jo,oe should be between characters as %--%
    order by subject;

--LIKE ANY
-- Allows case-sensitive matching of strings based on comparison with one or more patterns.
--The operation is similar to LIKE. If the input string matches any of the patterns, this returns the input string.

--<subject> LIKE ANY (<pattern1> [, <pattern2> ... ] ) [ ESCAPE <escape_char> ]

create or replace table like_example(subject varchar(20));
insert into like_example values
    ('John  Dddoe'),
    ('Joe   Doe'),
    ('John_down'),
    ('Joe down'),
    ('Tom   Doe'),
    ('Tim down'),
    (null);
    
select * from like_example;    

select * from like_example 
where subject like any ('%Jo%oe%','T%e')
order by subject;

select * from like_example 
where subject like any ('%J%h%^_do%', 'T%^%e') escape '^'   --- HERE IT WOULD GIVE OUTPUT THAT contains alphabets j&h between characters and do at 
--starting position of 2nd character


order by subject;
  
USE DATABASE AJ_SQL_DEMO_DATABASE;

create or replace table strings (v varchar(50));
insert into strings (v) values
    ('San Francisco'),
    ('San Jose'),
    ('Santa Clara'),
    ('Sacramento');
    
select * from strings
    
--Use wildcards to search for a pattern:
---Using . & * operator
select v from strings
where v regexp 'San* [fF].*'   --- here it would start with San
order by v;    

----Using :: as character class digit and regexp_replace will replace string with blank space and trim will remove whole blank space and give output as digit
SELECT  TRIM(REGEXP_REPLACE(string, '[^[:digit:]]', ' ')) AS Numeric_value
FROM (SELECT ' Area code for employee ID 112244 is 12345.' AS string) a;

CREATE TABLE demo3 (id INT, string1 VARCHAR);
INSERT INTO demo3 (id, string1) VALUES
    (5, 'A MAN A PLAN A CANAL')
    ;

SELECT * FROM DEMO3;
select id, 
    regexp_substr(string1, 'A\\W+(\\w+)', 1, 1, 'e', 1) as "RESULT1",
    regexp_substr(string1, 'A\\W+(\\w+)', 1, 2, 'e', 1) as "RESULT2",
    regexp_substr(string1, 'A\\W+(\\w+)', 1, 3, 'e', 1) as "RESULT3",
    regexp_substr(string1, 'A\\W+(\\w+)', 1, 4, 'e', 1) as "RESULT4"
    from demo3;
----regexp_substr(string1, 'A\\W+(\\w+)', 1, 1, 'e', 1) extracts the first occurrence of a word after the letter 'A' in the string1 column.
--The regular expression 'A\W+(\w+)' looks for the letter 'A' followed by a non-word character (\W) and then captures a word (\w+). 
--The 'e' parameter indicates to return the substring matched by the first capturing group (the word after 'A').
--regexp_substr(string1, 'A\\W+(\\w+)', 1, 2, 'e', 1) extracts the second occurrence of such a word.
--regexp_substr(string1, 'A\\W+(\\w+)', 1, 3, 'e', 1) extracts the third occurrence of such a word.
--regexp_substr(string1, 'A\\W+(\\w+)', 1, 4, 'e', 1) extracts the fourth occurrence of such a word.


/* Snowflake Regular Expression Functions
The regular expression functions are string functions that match a given regular expression. These functions are commonly called as a ‘regex’ functions.

Below are some of the regular expression function that Snowflake cloud data warehouse supports:

REGEXP_COUNT
REGEXP_INSTR
REGEXP_LIKE
REGEXP_SUBSTR
REGEXP_REPLACE
REGEXP
RLIKE */

/* Snowflake REGEXP_COUNT Function
The REGEXP_COUNT function searches a string and returns an integer that indicates the number of 
times the pattern occurs in the string. If no match is found, then the function returns 0.

syntax : REGEXP_COUNT( <string> , <pattern> [ , <position> , <parameters> ] ) */ 
select regexp_count('qqqabcrtrababcbcd', 'abc');
select regexp_count('qqqabcrtrababcbcd', '[abc]') as abc_character_count;
select REGEXP_COUNT('QQQABCRTRABABCBCD', '[ABC]{3}');
select REGEXP_COUNT('AB  C D hello how are you hi an a n d ',' ') AS SPACE_COUNT FROM dual;

select REGEXP_REPLACE('AB  C D hello how are you hi an a n d ','( ){10,}','') as output;

select REGEXP_REPLACE('AB  C D hello how are you hi an a n d ','(){3}','') as output;

select REGEXP_REPLACE('AB  C D hello how are you hi an a n d ',' ','') as output;

/*
The Snowflake REGEXP_REPLACE function returns the string by replacing specified pattern. 
If no matches found, original string will be returned.

Following is the syntax of the Regexp_replace function.

REGEXP_REPLACE( <string> , <pattern> [ , <replacement> , <position> , <occurrence> , <parameters> ] )

1. Extract date from a text string using Snowflake REGEXP_REPLACE Function
The REGEXP_REPLACE function is one of the easiest functions to get the required value when manipulating strings data.
Consider the below example to replace all characters except the date value. */

--For example, consider following query to return only user name.
select regexp_replace( 'anandjha2309@gmail.com', '@.*\\.(com)');
----The pattern specified in the regular expression is '@.*\\.(com)', which matches the '@' symbol, followed by any number of characters ('.*'), 
--and ending with the string '.com'.

select regexp_replace('Customers - (NY)','\\(|\\)','') as customers;

SELECT TRIM(REGEXP_REPLACE(string, '[a-z/-/A-Z/.]', ''))
AS date_value 
FROM (SELECT 'My DOB is 04-12-1976.' AS string) a;

/* 2. Extract date using REGEXP_SUBSTR 
Alternatively, REGEXP_SUBSTR function can be used to get date field from the string data. 

For example, consider the below example to get date value from a string containing text and the date. */
SELECT REGEXP_SUBSTR('I am celebrating my birthday on 05/12/2020 this year','[0-9][0-9]/[0-9][0-9]/[0-9][0-9][0-9][0-9]') as dob;

-- 3. Validate if date is in a valid format using REGEXP_LIKE function
SELECT * FROM (SELECT '04-12-1976' AS string) a where REGEXP_LIKE(string,'\\d{1,2}\\-\\d{1,2}-\\d{4,4}');

--4. String pattern matching using REGEXP_LIKE
WITH tbl
  AS (select t.column1 mycol 
      from values('A1 something'),('B1 something'),('Should not be matched'),('C1 should be matched') t )

SELECT * FROM tbl WHERE regexp_like (mycol,'[a-zA-z]\\d{1,}[\\s0-9a-zA-Z]*');


/*
-- Snowflake REGEXP Function
The Snowflake REGEXP function is an alias for RLIKE.

Following is the syntax of the REGEXP function.

-- 1st syntax
REGEXP( <string> , <pattern> [ , <parameters> ] )

-- 2nd syntax
<string> REGEXP <pattern> */

--For example, consider following query to matches string with query.
SELECT city REGEXP 'M.*' 
FROM   ( 
              SELECT 'Bangalore' AS city 
              UNION ALL 
              SELECT 'Mangalore' AS city ) AS tmp;

/*
Snowflake RLIKE Function
The Snowflake RLIKE function is an alias for REGEXP and regexp_like.

Following is the syntax of the RLIKE function.

-- 1st syntax
RLIKE( <string> , <pattern> [ , <parameters> ] )

-- 2nd syntax
<string> RLIKE <pattern>
*/

--For example, consider following query to matches string with query.
SELECT city RLIKE 'M.*'
FROM   ( 
              SELECT 'Bangalore' AS city 
              UNION ALL 
              SELECT 'Mangalore' AS city ) AS tmp;



/* Snowflake Extract Numbers from the string examples
The regular expression functions come handy when you want to extract numerical values from the string data. 
Though you can use built-in functions to check if a string is numeric. 
But, getting particular numeric values is done easily using regular expressions.

For example, extract the number from the string using Snowflake regexp_replace regular expression Function. */

SELECT  TRIM(REGEXP_REPLACE(string, '[^[:digit:]]', ' ')) AS Numeric_value
FROM (SELECT ' Area code for employee ID 112244 is 12345.' AS string) a;

--For example, consider below query that uses different regex patterns.

SELECT  TRIM(REGEXP_REPLACE(string, '[a-z/-/A-z/./#/*]', '')) AS Numeric_value
FROM (SELECT ' Area code for employee ID 112244 is 12345.' AS string) a;
/* The most common requirement in the data warehouse environment is to extract certain digits from the string.
For example, extract the 6 digit number from string data. 

There are many methods that you can use, however, the easiest method is to use the 
Snowflake REGEXP_SUBSTR regular expressions for this requirement. 

You can modify the regular expression pattern to extract any number of digits based on your requirements. */

--Snowflake Extract 6 digit’s numbers from string value examples
SELECT REGEXP_SUBSTR(string, '(^|[^[:word:]]|[[:space:]])\\d{6}([^[:word:]]|[[:space:]]|$)') AS ID
FROM (SELECT ' Area code for employee ID 112244 is 12345.' AS string) a;

-- Another common requirement is to extract alphanumeric values from a string data.
-- Snowflake Extract Alphanumeric from the string examples
-- For example, consider below example to extract ID which is a combination of ‘ID’ and numeric value.

SELECT REGEXP_SUBSTR('abc jjs Updates ID 123 ID_112233','ID_[0-9][0-9][0-9][0-9][0-9][0-9]') as ID;

--01PI10EC014 1pi10eC014

--How to Remove Spaces in the String in snowflake?

/* Nowadays, data is required everywhere. 
Many organizations automatically capture the data using tools or machines. 
Machines may introduce the unwanted data such as white space when it captures the actual data. 
These junk data is of no use in reporting, thus you need to remove them before loading into the target table.

In a data warehouse, you will receive data from multiple sources. 
You may have to pre-process the data before loading it to target table. 
The pre-process step such as removing white spaces from data is commonly used. 
In this LECTURE we will check how to remove spaces in a string using Snowflake built-in functions. 

Snowflake provides many built-in functions to remove white space or any unwanted data from a string.

You can use any of the following string functions as per your requirements.

Replace String Function
TRIM Function
Translate Function
REGEXP_REPLACE Function */

SELECT REPLACE('AB  C D ', ' ', '') as space_removed_output;    -- to remove empty spaces within ''

SELECT TRANSLATE('AB  C D ', ' ', '') as output;       ---- -- to remove empty spaces within ''

/* Remove White Spaces using REGEXP_REPLACE Function

The Regexp_replace remove all occurrences of white space in a string.
For example, consider following regexp_replace example to replace all spaces in the string with nothing. */

select REGEXP_REPLACE('AB  C D hello how are you hi an a n d ','( ){1,}','') as output;

select regexp_replace('It was the best of times, it was the worst of times', '( ){1,}','') as "result" from dual;

/* The most common requirement in the data warehouse environment is to extract 
certain digits from the string.
For example, extract the 6 digit number from string data. 

There are many methods that you can use, however, the easiest method is to use the 
Snowflake REGEXP_SUBSTR regular expressions for this requirement. 

You can modify the regular expression pattern to extract any number of 
digits based on your requirements. */

--Snowflake Extract 6 digit’s numbers from string value examples
SELECT REGEXP_SUBSTR(string, '(^|[^[:word:]]|[[:space:]])\\d{10}([^[:word:]]|[[:space:]]|$)') AS ID
FROM (SELECT ' Phone Number for employee ID 112244 is 9008276611.' AS string) a;

-- Another common requirement is to extract alphanumeric values from a string data.
-- Snowflake Extract Alphanumeric from the string examples
-- For example, consider below example to extract ID which is a combination of ‘ID’ 
--and numeric value.

SELECT REGEXP_SUBSTR('abc jjs Updates ID 123 ID_112233','ID_[0-9][0-9][0-9][0-9][0-9][0-9]') as ID;

--Using identity or autoincrement to table in Snowflake

/* In Snowflake, you can set the default value for a column, 
which is typically used to set an autoincrement or identity as the default value, 
so that each time a new row is inserted a unique id for that row is generated and stored and can be used as a primary key. 

You can specify the default value for a column using create table or alter table.

However, if you try to alter a table to add an autoincrement column that already has data in it, we will get an error in Snowflake. 
This is not supported in Snowflake, due to the underlying architecture.

It’s not as easy as altering the existing table, but there are two ways we can add an identity or autoincrement column to an existing table. */

--Method 1: Using autoincrement or identity as a default value.
--First we are going to create a simple table that we want to add an identity/autoincrement field to:

use database "AJ_SQL_DEMO_DATABASE";

create or replace table AJ_COLORS as
    select name
    from (values ('blue'),('red'),('green')) colors (name);

select * from AJ_COLORS
    
-- Next we create a new table with the same structure as the existing table and add an idenity column using like to copy table structure of table.  
create or replace table aj_identity_column_example like AJ_COLORS;

alter table aj_identity_column_example add column id int identity(1,1);


insert into aj_identity_column_example(name) 
    select name from aj_colors;

/* The identityautoincrement columns take two optional parameters:
         -> start the starting value of the column
          -> increment the specific amount to increment each row
          
In the example above we set the column to start at 1 and increment by 1.

autoincrement and identity are synonymous with each other and the default value for start and increment, if not specified, is 1 for both*/

--To replace our existing colors table with the new table:
alter table AJ_IDENTITY_COLUMN_EXAMPLE rename to colors;

-- Method 2: Using sequences
/*
In the example above we only had one column, so specifying the column manually in the insert worked fine for our use case. 
But, sometimes existing tables have a lot of columns and we don’t want to have to specify each column, either to save time or also to avoid errors.

We can programatically add an autoincrement or identity field to a wide table, but we have to do it a little differently.
*/

-- Let’s use an existing Snowflake sample data table to see why we can’t just alter the existing table:

create or replace table identity_column_example like "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."CUSTOMER";

alter table identity_column_example add column id int identity(1,1) not null;

insert into identity_column_example as
select *from "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."CUSTOMER";

-- The main problem here and the reason we get an error is when we use * the number of columns returned is one less than the new table we created. 
-- We can’t specify an empty value in a select statement, so we can’t force the identity column to populate in the way we want. 
-- We could specifiy the columns we want to populate manually, leaving out only the id column, but that’s what we are trying to avoid.

-- Let’s see what happens when we fill that column with an expression that auto-increments.
insert into identity_column_example 

select *,row_number() over (order by null)
from "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."CUSTOMER";

-- BINGOOOOOOOOO It works!!! BUT WAIT, let’s take a look at what happens when we insert a new record into the color table:
insert into identity_column_example(c_custkey, c_name, c_address, c_nationkey, c_phone, c_acctbal, c_mktsegment, c_comment)
values (219874, 'Customer#000219874', 'sadhjekj', 9, '19-505-461-2873', 999.99, 'asjdasgdj', 'sdadtyhkjer');

select * from identity_column_example order by id limit 3;

-- As you can see we have a duplicate value in our id field, because the identity column counter was never triggered, 
--- so when we insert a new record it starts over at 1.

--In this case, we have to use a sequence. The identity and autoincrement default values use sequences under the hood, 
-- so we will be essentially recreating that functionality.

-- When we create our own sequence we have access to the next value in the sequence. 
-- This allows us to add the next incremental value when we backfill the new table with the old table.

--First,we create a sequence that starts at 1 and increment by 1 &name it seq1 as to insert auto-increment within data table alresdy present need to create sequence
create or replace sequence seq1 start=1 increment=1;
show sequences

--creating 2nd sequence
create or replace sequence seq2 start=100 increment=1;

--Next, we’ll recreate our table and add a column id with the nextval of the seq1 sequence as the default:
create or replace table identity_column_example like "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."CUSTOMER";

select get_ddl('table', 'identity_column_example'); --to check the structure of table from datatypes to columns to keys

--ADDING COLUMNS ID and then will add identity or auto-increment with NEXTVAL
alter table identity_column_example 
add column id int DEFAULT seq1.NEXTVAL;

--SYNTAX : alter table <table-name> modify column <column-name> default <new-sequence-name>.nextval;
alter table identity_column_example MODIFY COLUMN id  DEFAULT seq2.NEXTVAL; 

-- To Remove the default value
alter table <table-name> modify column <column-name> drop default;

--Then, we can backfill the new table using nextval as nextval will add values from sequence created within identity or auto-increment column.
insert into identity_column_example 
select *,
       seq2.nextval
from "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."CUSTOMER";

select * from identity_column_example


-- Now, when we add a new record, the id column autoincrements properly and will remain unique:
insert into identity_column_example(c_custkey, c_name, c_address, c_nationkey, c_phone, c_acctbal, c_mktsegment, c_comment)
values (219874, 'Customer#000219874', 'sadhjekj', 9, '19-505-461-2873', 999.99, 'asjdasgdj', 'sdadtyhkjer');

select * from identity_column_example 
where c_custkey = 219874
order by id;

----------------------------------------Views ---------------------------------------------

--fist row should always use this use database command
USE DATABASE AJ_SQL_DEMO_DATABASE;

--next create the required table 
create or replace table aj_hospital_table (patient_id integer,
                             patient_name varchar, 
                             billing_address varchar,
                             diagnosis varchar, 
                             treatment varchar,
                             cost number(10,2));

-- insert the data 
insert into aj_hospital_table 
        (patient_id, patient_name, billing_address, diagnosis, treatment, cost) 
    values
        (1, 'Mark Knopfler', '1982 Telegraph Road', 'Industrial Disease', 
            'a week of peace and quiet', 2000.00),
        (2, 'Guido van Rossum', '37 Florida St.', 'python bite', 'anti-venom', 
            70000.00),
        (3, 'Devin', '197 Brigade Road Texas', 'dog bite', 'Rabies Injection', 
            40000.00),
        (4, 'Mark', '38 denver St Chicago', 'Dengue', 'Malaria', 
            50000.00),
        (5, 'Peter', '78 New Yor City', 'Accident', 'Operation', 
            340000.00);
--check the tablke and its contents            
describe table  aj_hospital_table      ;    
SELECT * FROM  aj_hospital_table; 

--create view and --check its contents                      
create or replace view aj_doctor_view as
    select patient_id, patient_name, diagnosis, treatment from aj_hospital_table;

describe view aj_doctor_view;
SELECT * FROM aj_DOCTOR_VIEW;

create or replace view aj_accountant_view as
    select patient_id, patient_name, billing_address, cost from aj_hospital_table;

describe view aj_doctor_view;
SELECT * FROM aj_accountant_view;

-- A view can be used almost anywhere that a table can be used (joins, subqueries, etc.). 
-- For example, using the views created above:

-- Show all of the types of medical problems for each patient to view ceratin columns within view
select distinct diagnosis from aj_doctor_view;
    
   
-- A view can be used almost anywhere that a table can be used (joins, subqueries, etc.). 
-- For example, using the views created above:
--Show all of the types of medical problems for each patient:
select distinct diagnosis from aj_doctor_view;

--Show the cost of each treatment (without showing personally identifying information about specific patients): using multiple views join like concept USING MULTIPLE VIEWS
select treatment, cost 
from aj_doctor_view as aj_dv, aj_accountant_view as aj_av
where aj_av.patient_id = aj_dv.patient_id;


---A CREATE VIEW command can use a fully-qualified, partly-qualified, or unqualified table name. 
--For example:

--create view v1 as select ... from my_database.my_schema.my_table;
create or replace view v1 AS 
SELECT S_STORE_NAME,S_NUMBER_EMPLOYEES,S_HOURS 
FROM "SNOWFLAKE_SAMPLE_DATA"."TPCDS_SF100TCL"."STORE";

SELECT * FROM V1 LIMIT 30;

--FROM RESPECTIVE SCHEMAS
create view v1 as select ... from my_schema.my_table;
--FROM RESPECTIVE TABLE
create view v1 as select ... from my_table;

--For example, you can create one view for the doctors, and one for the nurses, 
-- and then create the medical_staff view by referring to the doctors view and nurses view:

create OR REPLACE table employees (id integer, title varchar);
insert into employees (id, title) values
    (1, 'doctor'),
    (2, 'nurse'),
    (3, 'janitor')
    ;

---- creating multiple views within a column
create view doctors as select * from employees where title = 'doctor';
create view nurses as select * from employees where title = 'nurse';
create view medical_staff as
    select * from doctors
    union
    select * from nurses
    ;

select * 
    from medical_staff
    order by id;

---------------------------------Rollup and Cube------------------------------------------------------

USE DATABASE AJ_SQL_DEMO_DATABASE;

-- download the sale data from IBM DATASETS 
CREATE OR REPLACE TABLE SALES 
             (SALES_DATE DATE, 
              SALES_PERSON VARCHAR(15), 
              REGION VARCHAR(15), 
              SALES INTEGER);
              
SHOW COLUMNS IN SALES;

----LOAD THE DATA 

SELECT * FROM SALES;

SELECT WEEK(SALES_DATE) AS WEEK, 
       DAYOFWEEK(SALES_DATE) AS DAY_WEEK, 
       SALES_PERSON, SALES AS UNITS_SOLD 
FROM SALES 
WHERE WEEK(SALES_DATE) = 13;

--- by week number units sold(sales)
-- Example 1:  Here is a query with a basic GROUP BY clause over 3 columns:
SELECT WEEK(SALES_DATE) AS WEEK,
       DAYOFWEEK(SALES_DATE) AS DAY_WEEK,
       SALES_PERSON, SUM(SALES) AS UNITS_SOLD       
  FROM SALES
  WHERE WEEK(SALES_DATE) = 13
  GROUP BY WEEK(SALES_DATE), DAYOFWEEK(SALES_DATE), SALES_PERSON
  ORDER BY WEEK, DAY_WEEK, SALES_PERSON;
  
-- Produce the result based on two different grouping sets of rows from the SALES table.
-- Example 2:  Produce the result based on two different grouping sets of rows from the SALES table.
SELECT WEEK(SALES_DATE) AS WEEK,
         DAYOFWEEK(SALES_DATE) AS DAY_WEEK,
         SALES_PERSON, SUM(SALES) AS UNITS_SOLD       
FROM SALES 
WHERE WEEK(SALES_DATE) = 13
GROUP BY GROUPING SETS ((WEEK(SALES_DATE), SALES_PERSON),
                         (DAYOFWEEK(SALES_DATE), SALES_PERSON))
ORDER BY WEEK, DAY_WEEK, SALES_PERSON;

-- The rows with WEEK 13 are from the first grouping set and the other rows are from the second grouping set.

-- Example 3:  If you use the 3 distinct columns involved in the grouping sets of Example 2 
-- and perform a ROLLUP, you can see grouping sets for (WEEK,DAY_WEEK,SALES_PERSON), (WEEK, DAY_WEEK), (WEEK) and grand total.
--- This would give output as weekly and daily with subtotals and grandtotals but not a  combination between each rows.
SELECT WEEK(SALES_DATE) AS WEEK,
        DAYOFWEEK(SALES_DATE) AS DAY_WEEK,
        SALES_PERSON, SUM(SALES) AS UNITS_SOLD       
  FROM SALES
  WHERE WEEK(SALES_DATE) = 13
  GROUP BY ROLLUP ( WEEK(SALES_DATE), DAYOFWEEK(SALES_DATE), SALES_PERSON )
  ORDER BY WEEK, DAY_WEEK, SALES_PERSON;
  
--- Example 4:  If you run the same query as Example 3 only replace ROLLUP with CUBE, 
-- you can see additional grouping sets for (WEEK,SALES_PERSON), (DAY_WEEK,SALES_PERSON), (DAY_WEEK), (SALES_PERSON) in the result.  
--- This would give output as weekly and daily with subtotals and grandtotals and all possible combination between each rows or categories.
  SELECT WEEK(SALES_DATE) AS WEEK,
         DAYOFWEEK(SALES_DATE) AS DAY_WEEK,
         SALES_PERSON, SUM(SALES) AS UNITS_SOLD       
  FROM SALES
  WHERE WEEK(SALES_DATE) = 13
  GROUP BY CUBE ( WEEK(SALES_DATE), DAYOFWEEK(SALES_DATE), SALES_PERSON )
  ORDER BY WEEK, DAY_WEEK, SALES_PERSON;


-- Example 5:  Obtain a result set which includes a grand-total of selected rows from the SALES table 
-- together with a group of rows aggregated by SALES_PERSON and MONTH.

  SELECT SALES_PERSON,
         MONTH(SALES_DATE) AS MONTH,
         SUM(SALES) AS UNITS_SOLD
  FROM SALES
  GROUP BY GROUPING SETS ( (SALES_PERSON, MONTH(SALES_DATE)),
                           ()        
                         )
  ORDER BY SALES_PERSON, MONTH;

-- Example 6:  This example shows two simple ROLLUP queries followed by a query which treats the two ROLLUPs 
-- as grouping sets in a single result set and specifies row ordering for each column involved in the grouping sets.
-- Example 6-1:

 SELECT WEEK(SALES_DATE) AS WEEK,
         DAYOFWEEK(SALES_DATE) AS DAY_WEEK,
         SUM(SALES) AS UNITS_SOLD
  FROM SALES
  GROUP BY ROLLUP ( WEEK(SALES_DATE), DAYOFWEEK(SALES_DATE) )
  ORDER BY WEEK, DAY_WEEK;

-- Example 6-2:
 SELECT MONTH(SALES_DATE) AS MONTH,
         REGION,
         SUM(SALES) AS UNITS_SOLD
  FROM SALES
  GROUP BY ROLLUP ( MONTH(SALES_DATE), REGION )
  ORDER BY MONTH, REGION;

-- Example 6-3:
 -----Using grouping and rollup together to get output as 0 for null and 1 for subtotals.
SELECT WEEK(SALES_DATE) AS WEEK,
       DAYOFWEEK(SALES_DATE) AS DAY_WEEK,
       MONTH(SALES_DATE) AS MONTH,
       REGION,
       SUM(SALES) AS UNITS_SOLD
FROM SALES
GROUP BY GROUPING SETS ( ROLLUP(WEEK(SALES_DATE),DAYOFWEEK(SALES_DATE)),
                         (ROLLUP(MONTH(SALES_DATE),REGION))
ORDER BY WEEK, DAY_WEEK, MONTH, REGION;

-------------Window Functions --------------------------------------------
USE DATABASE AJ_SQL_DEMO_DATABASE;

DROP TABLE TOP_SCORERS;
--another way to insert data using UNION ALL
CREATE OR REPLACE TABLE TOP_SCORERS AS
SELECT
  'James Harden' AS player,
  2335 AS points,
  2020 AS season
UNION ALL
(SELECT
  'Damian Lillard' AS player,
  1978 AS points,
  2020 AS season)
UNION ALL
(SELECT
  'Devin Booker' AS player,
  1863 AS points,
  2020 AS season)
UNION ALL
(SELECT
  'James Harden' AS player,
  2818 AS points,
  2019 AS season)
UNION ALL
(SELECT
  'Paul George' AS player,
  1978 AS points,
  2019 AS season)
UNION ALL
(SELECT
  'Kemba Walker' AS player,
  2102 AS points,
  2019 AS season)
UNION ALL
(SELECT
  'Damian Lillard' AS player,
  2067 AS points,
  2019 AS season)
UNION ALL
( SELECT 
 'Richard Bartner' AS player,
  2067 AS points,
  2019 AS season)
UNION ALL
(SELECT
  'Devin Booker' AS player,
  1700 AS points,
  2019 AS season)
UNION ALL
(SELECT
  'Paul George' AS player,
  1033 AS points,
  2020 AS season)
UNION ALL
(SELECT
  'Kemba Walker' AS player,
  1145 AS points,
  2020 AS season)
 UNION ALL
(SELECT
  'Adam Gilchrist' AS player,
  1145 AS points,
  2020 AS season);
  
 SELECT * FROM TOP_SCORERS;
  
 DESCRIBE TABLE TOP_SCORERS;
 
 
 ---YEAR-OVER-YEAR CHANGE for player using first_value & last_value
 ---- Here order by is mandatory and instead of partition by can also use group by--
 
 SELECT DISTINCT (player),
  FIRST_VALUE(POINTS) OVER (PARTITION BY PLAYER ORDER BY SEASON ) AS first_season,
  LAST_VALUE(POINTS) OVER (PARTITION BY PLAYER ORDER BY SEASON ) AS last_season,
  ((last_season - first_season) / first_season) * 100 AS PER_CHANGE 
FROM
  TOP_SCORERS
ORDER BY 1;

 --(100 * ((LAST_VALUE(points) OVER (PARTITION BY player ORDER BY season ASC) - FIRST_VALUE(points) OVER (PARTITION BY player ORDER BY season ASC)) / FIRST_VALUE(points) OVER (PARTITION BY player ORDER BY season ASC))) AS per_change 
 
SELECT DISTINCT
  player,
  FIRST_VALUE(POINTS) OVER (PARTITION BY PLAYER ORDER BY SEASON ) AS first_season,
  LAST_VALUE(POINTS) OVER (PARTITION BY PLAYER ORDER BY SEASON ) AS last_season
FROM TOP_SCORERS
ORDER BY 1;

--We used FIRST_VALUE and LAST_VALUE to find the scores for each player in the 
--earliest and most recent seasons of data. 

-- Then we computed the percent difference using:

-- 100 * ((new value - old value) / old value) per_difference

--- How to get top 3 results for each group? using sub-query 
SELECT
  *
FROM
  (
    SELECT
      season,
      DENSE_RANK() OVER (PARTITION BY season ORDER BY points DESC) AS points_rank,
      player,
      points
    FROM
      TOP_SCORERS
  ) 
WHERE
  (points_rank <= 3);

-- In this example, we used RANK to rank each player by points over each season. 
-- Then we used a subquery to then return only the top 3 ranked players for each season.

-- How to find a running total?


select
  season,
  player,
  points,
  --SUM( <expr1> ) OVER ( [ PARTITION BY <expr2> ] [ ORDER BY <expr3> [ ASC | DESC ] [ <window_frame> ] ] )
  SUM(top_scorers.points) OVER (PARTITION BY player ORDER BY season ASC) AS running_total_points
FROM
  TOP_SCORERS
ORDER BY PLAYER ASC, SEASON ASC;

--To find the running total simply use SUM with an OVER clause where you specify your groupings (PARTITION BY), 
-- and the order in which to add them (ORDER BY).

Select * from "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."CUSTOMER"

---------Using row_number without partition
select C_NAME, C_ACCTBAL,
row_number() over (order by C_ACCTBAL DESC ) AS row_number
FROM "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."CUSTOMER"

------using row_number with partition 

select * from "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."PART"

------ using row_number and subquery to find expensive items with top manufacturers as per retail price
select *from(
select 
  row_number () over (partition by P_MFGR order by P_RETAILPRICE DESC) AS row_num,
  P_NAME,P_MFGR,P_RETAILPRICE
  FROM
  "SNOWFLAKE_SAMPLE_DATA"."TPCH_SF1"."PART"
)
WHERE row_num = 1

----------------------------Time travel ----------------------------------------------------
USE DATABASE DEMO_DATABASE;

create or replace table aj_time_travel_table 
(
        orderkey number(38,0),
        custkey number(38,0),
        orderstatus varchar(1),
        totalprice number(12,2),
        orderdate date,
        orderpriority varchar(15),
        clerk varchar(15),
        shippriority number(38,0),
        comment varchar(79)
 )
    data_retention_time_in_days = 1;
    
show tables like 'aj_time_travel_table';

describe table aj_time_travel_table;

--command to set data_retention_time_in_days to given value
alter table aj_time_travel_table 
set data_retention_time_in_days=55;

CREATE or replace DATABASE TIMETRAVEL;

use database timetravel;

CREATE or replace table AJ_CONSUMER_COMPLAINTS

(    DATE_RECEIVED STRING,
     PRODUCT_NAME VARCHAR2(50),
     SUB_PRODUCT VARCHAR2(100),
     ISSUE VARCHAR2(100),
     SUB_ISSUE VARCHAR2(100),
     CONSUMER_COMPLAINT_NARRATIVE string,
     Company_Public_Response STRING,
     Company VARCHAR(100),
     State_Name CHAR(4),
     Zip_Code string,
     Tags VARCHAR(40),
     Consumer_Consent_Provided CHAR(25),
     Submitted_via STRING,
     Date_Sent_to_Company STRING,
     Company_Response_to_Consumer VARCHAR(40),
     Timely_Response CHAR(4),
     CONSUMER_DISPUTED CHAR(4),
     COMPLAINT_ID NUMBER(12,0) NOT NULL PRIMARY KEY
);

DESCRIBE TABLE AJ_CONSUMER_COMPLAINTS;

select * from AJ_CONSUMER_COMPLAINTS;

-- get the current timestammp
SELECT CURRENT_TIMESTAMP; -- 2022-11-28 18:05:27.882 +0000

-- set timezone to UTC
ALTER SESSION SET TIMEZONE = 'UTC';

SELECT DISTINCT SUB_ISSUE FROM AJ_CONSUMER_COMPLAINTS;

-- update all age as zero
update AJ_CONSUMER_COMPLAINTS set sub_issue = NULL;

SELECT * FROM AJ_CONSUMER_COMPLAINTS;

-- time travel to a time based on the timestamp
select distinct sub_issue from AJ_CONSUMER_COMPLAINTS before(timestamp => '2022-11-28 18:05:27.882 +0000' ::timestamp);
select * from AJ_CONSUMER_COMPLAINTS before(timestamp => '2022-11-28 18:05:27.882 +0000' ::timestamp);

-- time travel to 5 minutes ago 
select * from AJ_CONSUMER_COMPLAINTS AT(offset => -60*5);

-- note down the query id of this query as we will use it in the time travel query as well
update AJ_CONSUMER_COMPLAINTS set TAGS = NULL;
--01a89dc3-3200-9a0b-0002-0dfe00088222

-- time travel to the time before the query id specified
select * from AJ_CONSUMER_COMPLAINTS before(statement => '01a89dc3-3200-9a0b-0002-0dfe00088222');

------------------JOINS IN SNOWFLAKE --------------------------------------------

USE DATABASE DEMO_DATABASE;

CREATE or replace TABLE cows_one (cnumber_1 int, cbreed varchar(20));

INSERT INTO cows_one VALUES (1,'Holstein');
INSERT INTO cows_one VALUES (2,'Guernsey');
INSERT INTO cows_one VALUES (3,'Angus');

SELECT * FROM cows_one;

CREATE OR REPLACE TABLE cows_two (cnumber_2 int, breeds varchar(20));

INSERT INTO cows_two VALUES (2,'Jersey');
INSERT INTO cows_two VALUES (3,'Brown Swiss');
INSERT INTO cows_two VALUES (4,'Ayrshire');

SELECT * FROM cows_two;

--An inner join, also known as a simple join, returns rows from joined tables 
---that have matching rows. 
--It does not include rows from either table that have no matching rows in the other.

SELECT x.cnumber_1,x.cbreed,y.BREEDS FROM cows_one as x
INNER JOIN cows_two as y ON x.cnumber_1 = y.cnumber_2;

--An inner join, also known as a simple join, returns rows from joined tables 
---that have matching rows. 
--It does not include rows from either table that have no matching rows in the other.

SELECT x.cnumber_1,x.cbreed,y.BREEDS FROM cows_one as x
INNER JOIN cows_two as y ON x.cnumber_1 = y.cnumber_2;

--A left outer join selects all the rows from the table on the left (cows_one in the sample), and displays the matching rows from the table on the right (cows_two).
--It displays an empty row for the table on the right if the table has no matching row for the table on the left.

/* In all cases, the order of evaluation is as follows:

              -- Evaluate all filters in the ON clause.
              -- Add in rows from the outer table (in this case, the left table in the left outer join) that do not match the filters.
              --- Apply the where clause to the results of the outer join. */

              

SELECT * FROM cows_one as x
LEFT OUTER JOIN cows_two y ON x.cnumber_1 = y.cnumber_2

--A right join selects all the rows from the table on the right (cows_two in our sample), and displays the matching rows from the table on the left (cows_one). 
-- It displays an empty row for the table on the left if the table has no matching value for the table on the right.

SELECT * FROM cows_one as x
RIGHT OUTER JOIN cows_two as y ON x.cnumber_1 = y.cnumber_2;

---A full outer join returns all joined rows from both tables, plus one row for each unmatched left row (extended with nulls on the right), 
--plus one row for each unmatched right row (extended with nulls on the left).


SELECT * FROM cows_one as x 
FULL OUTER JOIN cows_two as y ON x.cnumber_1 = y.cnumber_2;

-------------- using joins with where clause to filter data-----------------
SELECT * FROM cows_one as c
LEFT OUTER JOIN cows_two as c1 ON c.cnumber_1 = c1.cnumber_2 AND c.cnumber_1 < 3;

SELECT * FROM cows_one as c
LEFT OUTER JOIN c1 ON c.cnumber_1 = c1.cnumber_2 WHERE c.cnumber_1 < 3;

SELECT * FROM cows_one 
LEFT OUTER JOIN cows_two ON cows_one.cnumber = 
cows_two.cnumber AND cows_two.cnumber < 3;

SELECT * FROM cows_one 
LEFT OUTER JOIN cows_two ON cows_one.cnumber = cows_two.cnumber WHERE cows_two.cnumber < 3;


SELECT * FROM cows_one INNER JOIN cows_two USING (cnumber);

/* Conditions ON, USING, and NATURAL

You can use the join conditions ON, USING, and NATURAL to specify join criteria.

The ON clause is the most flexible. 
It can handle all join criteria, and, in certain cases, non-join criteria.
The USING and NATURAL clauses provide convenient ways to specify joins 
when the join columns have the same name.

Cross join : You cannot use an ON, USING, or NATURAL condition with a cross join.

------------------------------------------Inner join--------------------------------------------------
The following examples show inner joins. ON join_condition */
SELECT * FROM cows_one INNER JOIN cows_two 
ON cows_one.cnumber = cows_two.cnumber;

-- The following statement is equivalent:
SELECT * FROM cows_one, cows_two WHERE cows_one.cnumber = cows_two.cnumber;

-- USING join_column_list
SELECT * FROM cows_one INNER JOIN cows_two USING (cnumber_1);

--- NATURAL
SELECT * FROM cows_one NATURAL INNER JOIN cows_two;


----------------------------------------------Left outer join-----------------------------------------------------
-- The following examples show left outer joins.ON join_condition
   SELECT * FROM cows_one LEFT JOIN cows_two ON cows_one.cnumber = cows_two.cnumber;
   

-- USING join_column_list
SELECT * FROM cows_one LEFT JOIN cows_two USING (cnumber_1,cnumber_2);


-- NATURAL
SELECT * FROM cows_one NATURAL LEFT JOIN cows_two;


-----------------------------------------Right outer join---------------------------------------------
--The following examples show right outer joins. ON join_condition
SELECT * FROM cows_one RIGHT JOIN cows_two ON cows_one.cnumber = cows_two.cnumber;


--USING join_column_list
SELECT * FROM cows_one RIGHT JOIN cows_two USING (cnumber);

--NATURAL
SELECT * FROM cows_one NATURAL RIGHT JOIN cows_two;

--------------------------------------Full outer join-----------------------------------------------------------------
--The following examples show full outer joins.ON join_condition
SELECT * FROM cows_one FULL OUTER JOIN cows_two ON cows_one.cnumber = cows_two.cnumber;

--USING join_column_list
SELECT * FROM cows_one FULL OUTER JOIN cows_two USING (cnumber);

--NATURAL
SELECT * FROM cows_one NATURAL FULL OUTER JOIN cows_two;

------------ using left outer join to create master table--------------------------------
USE DATABASE DEMO_DATABASE;

CREATE OR REPLACE TABLE AJ_COMPLAIN
(
  ID	INT,
 ComplainDate VARCHAR(10),
 CompletionDate	VARCHAR(10),
 CustomerID	INT,
 BrokerID	INT,
 ProductID	INT,
 ComplainPriorityID	INT,
 ComplainTypeID	INT,
 ComplainSourceID	INT,
 ComplainCategoryID	INT,
 ComplainStatusID	INT,
 AdministratorID	STRING,
 ClientSatisfaction	VARCHAR(20),
 ExpectedReimbursement INT
);
---------------------------------------------------------------------------------------------------------


CREATE OR REPLACE TABLE AJ_CUSTOMER
(
CustomerID	INT,
LastName VARCHAR(60),
FirstName VARCHAR(60),
BirthDate VARCHAR(20) ,
Gender VARCHAR(20),
ParticipantType	VARCHAR(20),
RegionID	INT,
MaritalStatus VARCHAR(15));
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_BROKER
(
  BrokerID	INT,
  BrokerCode VARCHAR(70),
  BrokerFullName	VARCHAR(60),
  DistributionNetwork	VARCHAR(60),
  DistributionChannel	VARCHAR(60),
  CommissionScheme VARCHAR(50)

);
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_CATAGORIES
(
ID	INT,
Description_Categories VARCHAR2(200),
Active INT
);
---------------------------------------------------------------------------------------------------------

CREATE OR REPLACE TABLE AJ_PRIORITIES
(
ID	INT,
Description_Priorities VARCHAR(10)
);
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_PRODUCT
(
ProductID	INT,
ProductCategory	VARCHAR(60),
ProductSubCategory	VARCHAR(60),
Product VARCHAR(30)
);
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_REGION
(
  id INT,
  name	VARCHAR(50) ,
  county	VARCHAR(100),
  state_code	CHAR(5),
  state	VARCHAR (60),
  type	VARCHAR(50),
  latitude	NUMBER(11,4),
  longitude	NUMBER(11,4),
  area_code	INT,
  population	INT,
  Households	INT,
  median_income	INT,
  land_area	INT,
  water_area	INT,
  time_zone VARCHAR(70)
);
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_SOURCES
(
ID	INT,
Description_Source VARCHAR(20)
);
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_STATE_REGION
(
  State_Code VARCHAR(20),	
  State	 VARCHAR(20),
  Region VARCHAR(20)
);
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_STATUSES
(
  ID	INT,
  Description_Status VARCHAR(40));
---------------------------------------------------------------------------------------------------------
CREATE OR REPLACE TABLE AJ_TYPE1
(
  ID INT	,
  Description_Type VARCHAR(20)
);
-------------------------------------------------------------------------------------------------------
SELECT * FROM AJ_COMPLAIN;
SELECT * FROM AJ_CUSTOMER;
SELECT * FROM AJ_BROKER;
SELECT * FROM AJ_CATAGORIES;
SELECT * FROM AJ_PRIORITIES;
SELECT * FROM AJ_PRODUCT;
SELECT * FROM AJ_REGION;
SELECT * FROM AJ_SOURCES;
SELECT * FROM AJ_STATE_REGION;
SELECT * FROM AJ_STATUSES;
SELECT * FROM AJ_TYPE;
SELECT * FROM AJ_CUST_MASTER;

---------------- Craeting Tables by joining multiple tables----------------------------------
CREATE OR REPLACE TABLE AJ_CUST_MASTER AS
SELECT COM.ID,COM.ComplainDate,COM.CompletionDate,CUS.LastName,
CUS.FirstName,CUS.Gender,BR.BrokerFullName,BR.CommissionScheme,
CAT.Description_Categories,SR.Region,ST.Description_Status,REG.state,PR.Product,
PRI.Description_Priorities,SUR.Description_Source,TY.Description_Type
FROM AJ_COMPLAIN COM 
LEFT OUTER JOIN AJ_CUSTOMER CUS ON COM.CustomerID = CUS.CustomerID
LEFT OUTER JOIN AJ_REGION REG ON CUS.RegionID = REG.id
LEFT OUTER JOIN AJ_STATE_REGION SR ON REG.state_code = SR.State_Code
LEFT OUTER JOIN AJ_BROKER BR ON COM.BrokerID = BR.BrokerID
LEFT OUTER JOIN AJ_CATAGORIES CAT ON COM.ComplainCategoryID = CAT.ID
LEFT OUTER JOIN AJ_PRIORITIES PRI ON COM.ComplainPriorityID = PRI.ID
LEFT OUTER JOIN AJ_PRODUCT PR ON COM.ProductID = PR.ProductID
LEFT OUTER JOIN AJ_SOURCES SUR ON COM.ComplainSourceID = SUR.ID
LEFT OUTER JOIN AJ_STATUSES ST ON COM.ComplainStatusID = ST.ID
LEFT OUTER JOIN AJ_TYPE1 TY ON COM.ComplainTypeID = TY.ID
;

GRANT INSERT ON TABLE PUBLIC.AJ_TYPE TO ACCOUNTADMIN;

CREATE OR REPLACE TABLE AJ_CUST_MASTER AS
SELECT COM.ID,COM.ComplainDate,COM.CompletionDate,CUS.LastName,
CUS.FirstName,CUS.Gender,BR.BrokerFullName,BR.CommissionScheme,
CAT.Description_Categories,SR.Region,ST.Description_Status,REG.state,PR.Product,
PRI.Description_Priorities,SUR.Description_Source,
FROM AJ_COMPLAIN COM 
LEFT OUTER JOIN AJ_CUSTOMER CUS ON COM.CustomerID = CUS.CustomerID
LEFT OUTER JOIN AJ_REGION REG ON CUS.RegionID = REG.id
LEFT OUTER JOIN AJ_STATE_REGION SR ON REG.state_code = SR.State_Code
LEFT OUTER JOIN AJ_BROKER BR ON COM.BrokerID = BR.BrokerID
LEFT OUTER JOIN AJ_CATAGORIES CAT ON COM.ComplainCategoryID = CAT.ID
LEFT OUTER JOIN AJ_PRIORITIES PRI ON COM.ComplainPriorityID = PRI.ID
LEFT OUTER JOIN AJ_PRODUCT PR ON COM.ProductID = PR.ProductID
LEFT OUTER JOIN AJ_SOURCES SUR ON COM.ComplainSourceID = SUR.ID
LEFT OUTER JOIN AJ_STATUSES ST ON COM.ComplainStatusID = ST.ID
;

--------------Self-Joins within same tables----------------------
create or replace table FQ_Employee_Raw(
Employee_Id INT,
Name Varchar(20),
Salary Number(8,2))

insert into FQ_Employee_Raw
values (100,'Jennifer',4400),
(100,'Jennifer',4400),
(101,'Michael',13000),
(102,'Pat',600),
(102,'Pat',600),
(103,'Den',11000)

select * from FQ_EMPLOYEE_RAW

CREATE OR Replace table agents(
ID Number(2,0),
First_Name varchar(25),
Last_Name varchar(30),
Years_Experience Number(5,0))

insert into agents values
(1,'KATE','WHITE',5),
(2,'MELISSA','BROWN',2),
(3,'ALEXANDER','MCGREGOR',3),
(4,'SOFIA','SCOTT',3),
(5,'STEVEN','BLACK',1),
(6,'MARIA','SCOTT',1)

SELECT * FROM AGENTS

CREATE or replace TABLE CUSTOMERS(
id int not null primary key,
first_name varchar(20),
last_name varchar(20),
email varchar(60)unique
)

insert into customers values
(11,'Xaviera','Lovez','xaviera11111@gmail.com'),
(12,'Gabriel','Cumberly','gabriel11111@gmail.com'),
(13,'Elizabeth','Stevens','elizabeth11111@gmail.com'),
(14,'Oprah','Winfrey','prah11111@gmail.com'),
(15,'Ivan','Lee','ivan11111@gmail.com')

select * from customers

create or replace table sales(
id int,
house_id int,
c_date date,
agent_first_name varchar(15),
agent_last_name varchar(15),
customer_id int,
price int)

insert into sales values
(101,1012,'2121-11-03','Kate','White',14,1200000),
(102,2134,'2021-12-03','Sophia','Scott',12,950000),
(103,1015,'201-12-10','Maria','Scott',13,800000),
(104,2013,'2021-12-12','Alexand','Mcgregor',15,1350000),
(105,1910,'2022-01-10','Alexand','Slack',11,1500000)

select * from sales

---- using cross join
select a1.first_name as agent_first_name,
a1.last_name as agent_last_name,
a1.Years_Experience as agent1_experience,
a2.first_name as agent2_first_name,
a2.last_name as agent2_last_name,
a2.Years_Experience as agent2_experience,
from agents a1
inner join agents a2
on a1.id < a2.id
where a1.Years_Experience >= 3 AND a2.Years_Experience <=1
order by a1.id

create table student(
student_id int,
name varchar(20),
course_id int,
duration int
)

insert into student values
(1,'adam',1,3),
(2,'peter',2,4),
(1,'adam',2,4),
(3,'brian',3,2),
(2,'shane',3,5)

select * from student

--using cross join for comparision within same tables---
select s1.student_id,s1.name
from student s1 
inner join student s2
on s1.student_id=s2.student_id
and s1.course_id <> s2.course_id
order by 1,2

create or replace table Persons(
PersonID int not null primary key,
LastName varchar(255) not null,
FirstName varchar(255),
ReportsTo INT,
Title varchar(255),
Salary decimal
)

insert into Persons values
(1,'Jha','Anand',8,'Data Analyst',1200000),
(8,'M','Sangeetha',10,'Manager',4500000),
(2,'Chaturvedi','Ishan',8,'Data Scientist',1800000),
(10,'Shekhar','Srinu',123,'Tech Lead',2300000),
(4,'Meshram','Vineet',10,'Consultant',1200000),
(123,'Goel','Neha',134,'Manager',40000000),
(20,'Kumar','Satish',18,'Data Engineer',8000000),
(18,'Gupta','Ankita',10,'Business Architect',1100000),
(7,'yadav','Abhishek',10,'Data Analyst',10000000),
(27,'Bandekar','Kalpana',32,'CEO',50000000)

SELECT * FROM PERSONS

-----list of employees who reports to same manager using cross join----
select distinct p1.personid emp_id,
concat(p1.FirstName,' ',p1.LastName) as empfullname ,p2.ReportsTo as manager_id
from persons p1,persons p2
where p1.personid <> p2.personid
and p1.reportsto = p2.reportsto
order by 1,2,3

------ list of all reportee/manager and the number of employee---
select distinct p2.ReportsTo as manager_id,
concat(p1.FirstName,' ',p1.LastName) AS manager_name,
COUNT(DISTINCT p1.PersonID) AS Total_EMP_REPORTING
FROM Persons AS p1, Persons p2
where p1.PersonID <> p2.PersonID
and p1.ReportsTo = p2.ReportsTo
group by 1
order by 1

---list of all the employees and their associated manager---
select concat(b.LastName,', ',b.FirstName) AS 'Direct Reporting', 
concat(a.FirstName,' ',a.LastName) AS Manager
from Persons b
INNER JOIN persons a ON a.PersonID = b.ReportsTo
order by 2

-----Stored Procedures------------------------
drop database snowflake_stored_procedure;

CREATE DATABASE snowflake_stored_procedure;

USE snowflake_stored_procedure;

----Here first return is what datatype to return as output declare is used for datatype for defined query and again return as output--
CREATE OR REPLACE PROCEDURE area_calc_proc()
  RETURNS VARCHAR
  LANGUAGE SQL
  AS
  $$
    DECLARE
      radius_of_circle FLOAT;
      area_of_circle FLOAT;
    BEGIN
      radius_of_circle := 3;
      area_of_circle := pi() * radius_of_circle * radius_of_circle;
      RETURN area_of_circle;
    END;
  $$
  ;
  
CALL  area_calc_proc();

CREATE OR REPLACE PROCEDURE myprocedure_param(inp_radius number(8,3))
  RETURNS VARCHAR
  LANGUAGE SQL
  AS
  $$
    DECLARE
      message VARCHAR;
      radius_of_circle FLOAT;
      area_of_circle FLOAT;
    BEGIN
      radius_of_circle := inp_radius ;
      area_of_circle := 3.14 * radius_of_circle * radius_of_circle;
      message := 'Area of circle with ' || inp_radius || ' is ' || area_of_circle;
      RETURN message;
    END;
  $$
  ;
  
CALL  myprocedure_param(8.76);

SHOW PROCEDURES; 

create or replace procedure myproc(from_table string, to_table string, count int)
  returns string
  language python
  runtime_version = '3.8'
  packages = ('snowflake-snowpark-python')
  handler = 'run'
as
$$
def run(session, from_table, to_table, count):
  session.table(from_table).limit(count).write.save_as_table(to_table)
  return "SUCCESS"
$$;

CALL myproc('table_a', 'table_b', 5);


create table  bank_details(
age int,
job varchar(30),
marital varchar(30),
education varchar(30),
`default` varchar(30),
balance int , 
housing varchar(30),
loan varchar(30) , 
contact varchar(30),
`day` int,
`month` varchar(30) , 
duration int , 
campaign int,
pdays int , 
previous int , 
poutcome varchar(30) , 
y varchar(30));

insert into bank_details values
(44,'technician','single','secondary','no',29,'yes','no','unknown',5,'may',151,1,-1,0,'unknown','no'),
(33,'entrepreneur','married','secondary','no',2,'yes','yes','unknown',5,'may',76,1,-1,0,'unknown','no'),
(47,'blue-collar','married','unknown','no',1506,'yes','no','unknown',5,'may',92,1,-1,0,'unknown','no'),
(33,'unknown','single','unknown','no',1,'no','no','unknown',5,'may',198,1,-1,0,'unknown','no'),
(35,'management','married','tertiary','no',231,'yes','no','unknown',5,'may',139,1,-1,0,'unknown','no'),
(28,'management','single','tertiary','no',447,'yes','yes','unknown',5,'may',217,1,-1,0,'unknown','no'),
(42,'entrepreneur','divorced','tertiary','yes',2,'yes','no','unknown',5,'may',380,1,-1,0,'unknown','no'),
(58,'retired','married','primary','no',121,'yes','no','unknown',5,'may',50,1,-1,0,'unknown','no'),
(43,'technician','single','secondary','no',593,'yes','no','unknown',5,'may',55,1,-1,0,'unknown','no'),
(41,'admin.','divorced','secondary','no',270,'yes','no','unknown',5,'may',222,1,-1,0,'unknown','no'),
(29,'admin.','single','secondary','no',390,'yes','no','unknown',5,'may',137,1,-1,0,'unknown','no'),
(53,'technician','married','secondary','no',6,'yes','no','unknown',5,'may',517,1,-1,0,'unknown','no'),
(58,'technician','married','unknown','no',71,'yes','no','unknown',5,'may',71,1,-1,0,'unknown','no'),
(57,'services','married','secondary','no',162,'yes','no','unknown',5,'may',174,1,-1,0,'unknown','no'),
(51,'retired','married','primary','no',229,'yes','no','unknown',5,'may',353,1,-1,0,'unknown','no'),
(45,'admin.','single','unknown','no',13,'yes','no','unknown',5,'may',98,1,-1,0,'unknown','no'),
(57,'blue-collar','married','primary','no',52,'yes','no','unknown',5,'may',38,1,-1,0,'unknown','no'),
(60,'retired','married','primary','no',60,'yes','no','unknown',5,'may',219,1,-1,0,'unknown','no'),
(33,'services','married','secondary','no',0,'yes','no','unknown',5,'may',54,1,-1,0,'unknown','no'),
(28,'blue-collar','married','secondary','no',723,'yes','yes','unknown',5,'may',262,1,-1,0,'unknown','no'),
(56,'management','married','tertiary','no',779,'yes','no','unknown',5,'may',164,1,-1,0,'unknown','no'),
(32,'blue-collar','single','primary','no',23,'yes','yes','unknown',5,'may',160,1,-1,0,'unknown','no'),
(25,'services','married','secondary','no',50,'yes','no','unknown',5,'may',342,1,-1,0,'unknown','no'),
(40,'retired','married','primary','no',0,'yes','yes','unknown',5,'may',181,1,-1,0,'unknown','no'),
(44,'admin.','married','secondary','no',-372,'yes','no','unknown',5,'may',172,1,-1,0,'unknown','no'),
(39,'management','single','tertiary','no',255,'yes','no','unknown',5,'may',296,1,-1,0,'unknown','no'),
(52,'entrepreneur','married','secondary','no',113,'yes','yes','unknown',5,'may',127,1,-1,0,'unknown','no'),
(46,'management','single','secondary','no',-246,'yes','no','unknown',5,'may',255,2,-1,0,'unknown','no'),
(36,'technician','single','secondary','no',265,'yes','yes','unknown',5,'may',348,1,-1,0,'unknown','no'),
(57,'technician','married','secondary','no',839,'no','yes','unknown',5,'may',225,1,-1,0,'unknown','no'),
(49,'management','married','tertiary','no',378,'yes','no','unknown',5,'may',230,1,-1,0,'unknown','no'),
(60,'admin.','married','secondary','no',39,'yes','yes','unknown',5,'may',208,1,-1,0,'unknown','no'),
(59,'blue-collar','married','secondary','no',0,'yes','no','unknown',5,'may',226,1,-1,0,'unknown','no'),
(51,'management','married','tertiary','no',10635,'yes','no','unknown',5,'may',336,1,-1,0,'unknown','no'),
(57,'technician','divorced','secondary','no',63,'yes','no','unknown',5,'may',242,1,-1,0,'unknown','no'),
(25,'blue-collar','married','secondary','no',-7,'yes','no','unknown',5,'may',365,1,-1,0,'unknown','no'),
(53,'technician','married','secondary','no',-3,'no','no','unknown',5,'may',1666,1,-1,0,'unknown','no'),
(36,'admin.','divorced','secondary','no',506,'yes','no','unknown',5,'may',577,1,-1,0,'unknown','no'),
(37,'admin.','single','secondary','no',0,'yes','no','unknown',5,'may',137,1,-1,0,'unknown','no'),
(44,'services','divorced','secondary','no',2586,'yes','no','unknown',5,'may',160,1,-1,0,'unknown','no'),
(50,'management','married','secondary','no',49,'yes','no','unknown',5,'may',180,2,-1,0,'unknown','no'),
(60,'blue-collar','married','unknown','no',104,'yes','no','unknown',5,'may',22,1,-1,0,'unknown','no'),
(54,'retired','married','secondary','no',529,'yes','no','unknown',5,'may',1492,1,-1,0,'unknown','no'),
(58,'retired','married','unknown','no',96,'yes','no','unknown',5,'may',616,1,-1,0,'unknown','no'),
(36,'admin.','single','primary','no',-171,'yes','no','unknown',5,'may',242,1,-1,0,'unknown','no'),
(58,'self-employed','married','tertiary','no',-364,'yes','no','unknown',5,'may',355,1,-1,0,'unknown','no'),
(44,'technician','married','secondary','no',0,'yes','no','unknown',5,'may',225,2,-1,0,'unknown','no'),
(55,'technician','divorced','secondary','no',0,'no','no','unknown',5,'may',160,1,-1,0,'unknown','no'),
(29,'management','single','tertiary','no',0,'yes','no','unknown',5,'may',363,1,-1,0,'unknown','no'),
(54,'blue-collar','married','secondary','no',1291,'yes','no','unknown',5,'may',266,1,-1,0,'unknown','no'),
(48,'management','divorced','tertiary','no',-244,'yes','no','unknown',5,'may',253,1,-1,0,'unknown','no'),
(32,'management','married','tertiary','no',0,'yes','no','unknown',5,'may',179,1,-1,0,'unknown','no'),
(42,'admin.','single','secondary','no',-76,'yes','no','unknown',5,'may',787,1,-1,0,'unknown','no'),
(24,'technician','single','secondary','no',-103,'yes','yes','unknown',5,'may',145,1,-1,0,'unknown','no'),
(38,'entrepreneur','single','tertiary','no',243,'no','yes','unknown',5,'may',174,1,-1,0,'unknown','no'),
(38,'management','single','tertiary','no',424,'yes','no','unknown',5,'may',104,1,-1,0,'unknown','no'),
(47,'blue-collar','married','unknown','no',306,'yes','no','unknown',5,'may',13,1,-1,0,'unknown','no'),
(40,'blue-collar','single','unknown','no',24,'yes','no','unknown',5,'may',185,1,-1,0,'unknown','no'),
(46,'services','married','primary','no',179,'yes','no','unknown',5,'may',1778,1,-1,0,'unknown','no'),
(32,'admin.','married','tertiary','no',0,'yes','no','unknown',5,'may',138,1,-1,0,'unknown','no'),
(53,'technician','divorced','secondary','no',989,'yes','no','unknown',5,'may',812,1,-1,0,'unknown','no'),
(57,'blue-collar','married','primary','no',249,'yes','no','unknown',5,'may',164,1,-1,0,'unknown','no'),
(33,'services','married','secondary','no',790,'yes','no','unknown',5,'may',391,1,-1,0,'unknown','no'),
(49,'blue-collar','married','unknown','no',154,'yes','no','unknown',5,'may',357,1,-1,0,'unknown','no'),
(51,'management','married','tertiary','no',6530,'yes','no','unknown',5,'may',91,1,-1,0,'unknown','no'),
(60,'retired','married','tertiary','no',100,'no','no','unknown',5,'may',528,1,-1,0,'unknown','no'),
(59,'management','divorced','tertiary','no',59,'yes','no','unknown',5,'may',273,1,-1,0,'unknown','no'),
(55,'technician','married','secondary','no',1205,'yes','no','unknown',5,'may',158,2,-1,0,'unknown','no'),
(35,'blue-collar','single','secondary','no',12223,'yes','yes','unknown',5,'may',177,1,-1,0,'unknown','no'),
(57,'blue-collar','married','secondary','no',5935,'yes','yes','unknown',5,'may',258,1,-1,0,'unknown','no'),
(31,'services','married','secondary','no',25,'yes','yes','unknown',5,'may',172,1,-1,0,'unknown','no'),
(54,'management','married','secondary','no',282,'yes','yes','unknown',5,'may',154,1,-1,0,'unknown','no'),
(55,'blue-collar','married','primary','no',23,'yes','no','unknown',5,'may',291,1,-1,0,'unknown','no'),
(43,'technician','married','secondary','no',1937,'yes','no','unknown',5,'may',181,1,-1,0,'unknown','no'),
(53,'technician','married','secondary','no',384,'yes','no','unknown',5,'may',176,1,-1,0,'unknown','no'),
(44,'blue-collar','married','secondary','no',582,'no','yes','unknown',5,'may',211,1,-1,0,'unknown','no'),
(55,'services','divorced','secondary','no',91,'no','no','unknown',5,'may',349,1,-1,0,'unknown','no'),
(49,'services','divorced','secondary','no',0,'yes','yes','unknown',5,'may',272,1,-1,0,'unknown','no'),
(55,'services','divorced','secondary','yes',1,'yes','no','unknown',5,'may',208,1,-1,0,'unknown','no'),
(45,'admin.','single','secondary','no',206,'yes','no','unknown',5,'may',193,1,-1,0,'unknown','no'),
(47,'services','divorced','secondary','no',164,'no','no','unknown',5,'may',212,1,-1,0,'unknown','no'),
(42,'technician','single','secondary','no',690,'yes','no','unknown',5,'may',20,1,-1,0,'unknown','no'),
(59,'admin.','married','secondary','no',2343,'yes','no','unknown',5,'may',1042,1,-1,0,'unknown','yes'),
(46,'self-employed','married','tertiary','no',137,'yes','yes','unknown',5,'may',246,1,-1,0,'unknown','no'),
(51,'blue-collar','married','primary','no',173,'yes','no','unknown',5,'may',529,2,-1,0,'unknown','no'),
(56,'admin.','married','secondary','no',45,'no','no','unknown',5,'may',1467,1,-1,0,'unknown','yes'),
(41,'technician','married','secondary','no',1270,'yes','no','unknown',5,'may',1389,1,-1,0,'unknown','yes'),
(46,'management','divorced','secondary','no',16,'yes','yes','unknown',5,'may',188,2,-1,0,'unknown','no'),
(57,'retired','married','secondary','no',486,'yes','no','unknown',5,'may',180,2,-1,0,'unknown','no'),
(42,'management','single','secondary','no',50,'no','no','unknown',5,'may',48,1,-1,0,'unknown','no'),
(30,'technician','married','secondary','no',152,'yes','yes','unknown',5,'may',213,2,-1,0,'unknown','no'),
(60,'admin.','married','secondary','no',290,'yes','no','unknown',5,'may',583,1,-1,0,'unknown','no');

select * from bank_details;
select count(*)  from bank_details;

/*
In this modified version of the stored procedure, the res variable is explicitly declared as a RESULTSET data type. 
The RESULTSET data type represents an unbounded set of rows, which is suitable for storing the result of a 
SELECT statement that returns multiple rows.

After the res variable is assigned the result of the SELECT statement, 
it is returned as a table using the RETURN TABLE clause. 
The RETURN TABLE clause converts the RESULTSET data type to a table that can be used as the output of the stored procedure.
*/

--Here in procedure need to type all column names and even declare resultset datatype for it---
CREATE OR REPLACE PROCEDURE GET_ALL_RECORDS_FROM_TABLE()
RETURNS TABLE(age int, job varchar(30), marital varchar(30), education varchar(30), `default` varchar(30), balance int,
housing varchar(30), loan varchar(30), contact varchar(30), `day` int, `month` varchar(30), duration int,
campaign int, pdays int, previous int, poutcome varchar(30), y varchar(30))
LANGUAGE SQL
AS
$$
DECLARE
  res RESULTSET;
BEGIN
  res := (SELECT * FROM bank_details);
  RETURN TABLE(res);
END;
$$;

select distinct job from bank_details;

CALL GET_ALL_RECORDS_FROM_TABLE();

CREATE OR REPLACE PROCEDURE GET_AVG_BALANCE(job_role varchar(30))
RETURNS NUMBER(10,3)
--LANGUAGE SQL
AS
$$
DECLARE
  avg_balance NUMBER(10,3);
BEGIN
  SELECT AVG(balance) INTO avg_balance FROM bank_details WHERE job =: job_role; 
  RETURN avg_balance;
END;
$$;

--WHILE READING INPUT PARAMTERS GIVE =: VAR_NAME

CALL GET_AVG_BALANCE('admin.');

CALL GET_AVG_BALANCE();

-- Calling the stored procedure
CALL SELECT_REC();

-- Calling the stored procedure
CALL AVG_BAL_JOBROLE();

/* This shows a more realistic example that includes a call to the JavaScript API.
A more extensive version of this procedure could allow a user to insert data into a table that the user didn’t
have privileges to insert into directly. 
JavaScript statements could check the input parameters and execute the SQL INSERT only if certain requirements were met.
*/

create or replace procedure stproc1(FLOAT_PARAM1 FLOAT)
    returns string
    language javascript
    strict
    execute as owner
    as
    $$
    var sql_command = 
     "INSERT INTO stproc_test_table1 (num_col1) VALUES (" + FLOAT_PARAM1 + ")";
    try {
        snowflake.execute (
            {sqlText: sql_command}
            );
        return "Succeeded.";   // Return a success/error indicator.
        }
    catch (err)  {
        return "Failed: " + err;   // Return a success/error indicator.
        }
    $$
    ;

CALL stproc1(3.56);

--------------Using stored procedures for automation-----------------
CREATE SEQUENCE demo_video_seq START = 1 INCREMENT = 1;   -- CREATING SEQUENCE AS AUTOINCREMENT DOESNT WORK

CREATE OR REPLACE TABLE demo_video (
    ID INT DEFAULT demo_video_seq.NEXTVAL,
    NAME VARCHAR(40) DEFAULT 'TESTING',
    DATE TIMESTAMP
);

--CREATING TASK FOR AUTOMATION
---- HERE TASK IS CREATED AND DATA WOULD BE INSERTED EVERY 1 MINUTE AS WITHIN DATE COLUMN OF DEMO_VIDEO TABLE

CREATE OR REPLACE TASK INSERT_DATA_1MIN_INTERVAL
WAREHOUSE = COMPUTE_WH
SCHEDULE = '1 MINUTE'
AS 
INSERT INTO DEMO_VIDEO (DATE) VALUES(CURRENT_TIMESTAMP)

SHOW TASKS   -- TO SHOW CREATED TASKS
ALTER TASK INSERT_DATA_1MIN_INTERVAL RESUME --- TO RESUME TASK AS ITS SUSPENDED---
ALTER TASK INSERT_DATA_1MIN_INTERVAL SUSPENDED   -- TO SUSPEND TASK--

SELECT * FROM DEMO_VIDEO

CREATE OR REPLACE PROCEDURE UPDATE_THE_TABLE()
RETURNS TABLE (DATE TIMESTAMP)
LANGUAGE SQL
AS
$$
DECLARE
RES RESULTSET;
BEGIN;
RES := (INSERT INTO DEMOVIDEO (DATE) VALUES(CURRENT_TIMESTAMP));
RETURN TABLE(RES);
END;
$$;

CREATE DATABASE BANK;

USE BANK;


CREATE OR REPLACE TABLE DISTRICT(
District_Code INT PRIMARY KEY	,
District_Name VARCHAR(100)	,
Region VARCHAR(100)	,
No_of_inhabitants	INT,
No_of_municipalities_with_inhabitants_less_499 INT,
No_of_municipalities_with_inhabitants_500_btw_1999	INT,
No_of_municipalities_with_inhabitants_2000_btw_9999	INT,
No_of_municipalities_with_inhabitants_less_10000 INT,	
No_of_cities	INT,
Ratio_of_urban_inhabitants	FLOAT,
Average_salary	INT,
No_of_entrepreneurs_per_1000_inhabitants INT,
No_committed_crime_2017	INT,
No_committed_crime_2018 INT
) ;



CREATE OR REPLACE TABLE ACCOUNT(
account_id INT PRIMARY KEY,
district_id	INT,
frequency	VARCHAR(40),
Date DATE ,
FOREIGN KEY (district_id) references DISTRICT(District_Code) 
);

CREATE OR REPLACE TABLE ORDER_LIST (
order_id	INT PRIMARY KEY,
account_id	INT,
bank_to	VARCHAR(45),
account_to	INT,
amount FLOAT,
FOREIGN KEY (account_id) references ACCOUNT(account_id)
);



CREATE OR REPLACE TABLE LOAN(
loan_id	INT ,
account_id	INT,
Date	DATE,
amount	INT,
duration	INT,
payments	INT,
status VARCHAR(35),
FOREIGN KEY (account_id) references ACCOUNT(account_id)
);



CREATE OR REPLACE TABLE TRANSACTIONS(
trans_id INT,	
account_id	INT,
Date	DATE,
Type	VARCHAR(30),
operation	VARCHAR(40),
amount	INT,
balance	FLOAT,
Purpose	VARCHAR(40),
bank	VARCHAR(45),
account_partner_id INT,
FOREIGN KEY (account_id) references ACCOUNT(account_id));


CREATE OR REPLACE TABLE CLIENT(
client_id	INT PRIMARY KEY,
Sex	CHAR(10),
Birth_date	DATE,
district_id INT,
FOREIGN KEY (district_id) references DISTRICT(District_Code) 
);


CREATE OR REPLACE TABLE DISPOSITION(
disp_id	INT PRIMARY KEY,
client_id INT,
account_id	INT,
type CHAR(15),
FOREIGN KEY (account_id) references ACCOUNT(account_id),
FOREIGN KEY (client_id) references CLIENT(client_id)
);


CREATE OR REPLACE TABLE CARD(
card_id	INT PRIMARY KEY,
disp_id	INT,
type CHAR(10)	,
issued DATE,
FOREIGN KEY (disp_id) references DISPOSITION(disp_id)
);

---------------------------------------------------------------------------------------------

CREATE OR REPLACE STORAGE integration s3_int
TYPE = EXTERNAL_STAGE
STORAGE_PROVIDER = S3
ENABLED = TRUE
STORAGE_AWS_ROLE_ARN ='arn:aws:iam::441615131317:role/bankrole'
STORAGE_ALLOWED_LOCATIONS =('s3://czechbankdata/');
DESC integration s3_int;


CREATE OR REPLACE STAGE BANK
URL ='s3://czechbankdata'
--credentials=(aws_key_id='AKIAXQKR3H3PSG72XFMK'aws_secret_key='eKL6a6FjlQHic4s8Ne712Aelzg2ou4j6tNsVvFq5')
file_format=CSV
storage_integration =s3_int;

LIST @BANK;

SHOW STAGES;

--CREATE SNOWPIPE THAT RECOGNISES CSV THAT ARE INGESTED FROM EXTERNAL STAGE AND COPIES THE DATA INTO PATIENTS TABLE
--The AUTO_INGEST=true parameter specifies to read event notifications sent from an S3 bucket to an SQS queue when new data is ready to load.


CREATE OR REPLACE PIPE BANK_SNOWPIPE AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."DISTRICT"
FROM '@BANK/District/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE2 AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."ACCOUNT"
FROM '@BANK/Account/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE3 AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."TRANSACTIONS"
FROM '@BANK/Trnx/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE4 AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."DISPOSITION"
FROM '@BANK/disp/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE5 AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."CARD"
FROM '@BANK/Card/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE6 AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."ORDER_LIST"
FROM '@BANK/Order/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE7 AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."LOAN"
FROM '@BANK/Loan/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE8 AUTO_INGEST = TRUE AS
COPY INTO "BANK"."PUBLIC"."CLIENT"
FROM '@BANK/Client/'
FILE_FORMAT = CSV;

SHOW PIPES;

SELECT count(*) FROM DISTRICT;
SELECT count(*) FROM ACCOUNT;
SELECT count(*) FROM TRANSACTIONS;
SELECT count(*) FROM DISPOSITION;
SELECT count(*) FROM CARD;
SELECT count(*) FROM ORDER_LIST;
SELECT count(*) FROM LOAN;
SELECT count(*) FROM CLIENT;

ALTER PIPE BANK_SNOWPIPE refresh;

ALTER PIPE BANK_SNOWPIPE2 refresh;

ALTER PIPE BANK_SNOWPIPE3 refresh;

ALTER PIPE BANK_SNOWPIPE4 refresh;

ALTER PIPE BANK_SNOWPIPE5 refresh;

ALTER PIPE BANK_SNOWPIPE6 refresh;

ALTER PIPE BANK_SNOWPIPE7 refresh;

ALTER PIPE BANK_SNOWPIPE8 refresh;
-----------------------------------------------------------------------------------------------------------------------------------------------
SELECT * FROM DISTRICT;
SELECT * FROM ACCOUNT;
SELECT * FROM TRANSACTIONS;
SELECT * FROM DISPOSITION;
SELECT * FROM CARD;
SELECT * FROM ORDER_LIST;
SELECT * FROM LOAN;
SELECT * FROM CLIENT;

----------------------------------------------------------STORE PROCEDURE-------------------------------------------------------------------------
CREATE OR REPLACE PROCEDURE CREAT_OR_REPLACE_ACC_LATEST()
RETURNS STRING
LANGUAGE SQL
AS
$$
  CREATE OR REPLACE TABLE ACC_LATEST_TXNS_WITH_BALANCE 
AS(
SELECT LTD.*,TXN.BALANCE
FROM TRANSACTIONS AS TXN
INNER JOIN 
(
   SELECT ACCOUNT_ID,YEAR(DATE) AS TXN_YEAR,
   MONTH(DATE) AS TXN_MONTH,
   MAX(DATE) AS LATEST_TXN_DATE
   FROM TRANSACTIONS
   GROUP BY 1,2,3
   ORDER BY 1,2,3

) AS LTD ON TXN.ACCOUNT_ID = LTD.ACCOUNT_ID AND TXN.DATE = LTD.LATEST_TXN_DATE
WHERE TXN.TYPE = 'Credit' -- this is the assumptions am having : month end txn data is credit
ORDER BY TXN.ACCOUNT_ID,LTD.TXN_YEAR,LTD.TXN_MONTH);
$$;

SHOW PROCEDURES;


CREATE OR REPLACE PROCEDURE CREATE_OR_REPLACE_BANKINGKPI()
RETURNS STRING
LANGUAGE SQL
AS
$$
  CREATE OR REPLACE TABLE BANKING_KPI AS(
SELECT  ALWB.TXN_YEAR , ALWB.TXN_MONTH,T.BANK,A.ACCOUNT_TYPE,

COUNT(DISTINCT ALWB.ACCOUNT_ID) AS TOT_ACCOUNT, 
COUNT(DISTINCT T.TRANS_ID) AS TOT_TXNS,
COUNT(CASE WHEN T.TYPE = 'Credit' THEN 1 END) AS DEPOSIT_COUNT ,
COUNT(CASE WHEN T.TYPE = 'Withdrawal' THEN 1 END) AS WITHDRAWAL_COUNT,

SUM(ALWB.BALANCE) AS TOT_BALANCE,

ROUND((DEPOSIT_COUNT / TOT_TXNS) * 100,2)  AS DEPOSIT_PERC ,
ROUND((WITHDRAWAL_COUNT / TOT_TXNS) * 100,2) AS WITHDRAWAL_PERC ,
NVL(TOT_BALANCE / TOT_ACCOUNT,0) AS AVG_BALANCE,

ROUND(TOT_TXNS/TOT_ACCOUNT,0) AS TPA

FROM TRANSACTIONS AS T
INNER JOIN  ACC_LATEST_TXNS_WITH_BALANCE AS ALWB ON T.ACCOUNT_ID = ALWB.ACCOUNT_ID
LEFT OUTER JOIN  ACCOUNT AS A ON T.ACCOUNT_ID = A.ACCOUNT_ID
GROUP BY 1,2,3,4
ORDER BY 1,2,3,4);
$$;  

CALL CREAT_OR_REPLACE_ACC_LATEST();
CALL CREATE_OR_REPLACE_BANKINGKPI();  
  
  

CREATE OR REPLACE TASK  ACC_LATEST_TXNS_WITH_BALANCE
WAREHOUSE = COMPUTE_WH
SCHEDULE =  '1 MINUTE'
AS CALL CREAT_OR_REPLACE_ACC_LATEST();
  
CREATE OR REPLACE TASK  BANKING_KPI
WAREHOUSE = COMPUTE_WH
SCHEDULE =  '2 MINUTE'
AS CALL CREATE_OR_REPLACE_BANKINGKPI();  
  
SHOW TASKS;  
  
ALTER TASK ACC_LATEST_TXNS_WITH_BALANCE  RESUME;
ALTER TASK ACC_LATEST_TXNS_WITH_BALANCE SUSPEND;  
ALTER TASK  BANKING_KPI RESUME;
ALTER TASK BANKING_KPI SUSPEND;    

  
DROP TASK IF EXISTS ACC_LATEST_TXNS_WITH_BALANCE;
DROP TASK IF EXISTS  BANKING_KPI; 
  
DROP TABLE  ACC_LATEST_TXNS_WITH_BALANCE;
DROP TABLE  BANKING_KPI;  
  
SELECT * FROM ACC_LATEST_TXNS_WITH_BALANCE;
SELECT * FROM BANKING_KPI; 

-----------------------------Continuous Data Ingestion -------------------------------------
CREATE DATABASE RETAILS;
USE RETAILS;
use schema PUBLIC;

CREATE OR REPLACE TABLE demographic_RAW
(AGE_DESC	CHAR(20),
MARITAL_STATUS_CODE	CHAR(5),
INCOME_DESC	VARCHAR(40),
HOMEOWNER_DESC	VARCHAR(40),
HH_COMP_DESC	VARCHAR(50),
HOUSEHOLD_SIZE_DESC	VARCHAR(50),
KID_CATEGORY_DESC	VARCHAR(40),
household_key INT PRIMARY KEY
);

CREATE OR REPLACE TABLE CAMPAIGN_DESC_RAW
(DESCRIPTION CHAR(10),	
CAMPAIGN	INT ,
START_DAY	INT,
END_DAY INT,
PRIMARY KEY (DESCRIPTION),
UNIQUE (CAMPAIGN));

CREATE OR REPLACE TABLE CAMPAIGN_RAW
(DESCRIPTION	CHAR(10) ,
household_key	INT,
CAMPAIGN INT,
FOREIGN KEY (DESCRIPTION) references CAMPAIGN_DESC_RAW(DESCRIPTION) ,
FOREIGN KEY (CAMPAIGN) references CAMPAIGN_DESC_RAW(CAMPAIGN),
FOREIGN KEY (household_key) references demographic_RAW(household_key)
);

CREATE OR REPLACE TABLE PRODUCT_RAW
(PRODUCT_ID	INT PRIMARY KEY,
MANUFACTURER 	INT,
DEPARTMENT	VARCHAR(50),
BRAND	VARCHAR(30),
COMMODITY_DESC	VARCHAR(65),
SUB_COMMODITY_DESC VARCHAR(65)	,
CURR_SIZE_OF_PRODUCT VARCHAR(15)
);

CREATE OR REPLACE TABLE COUPON_RAW
(COUPON_UPC	INT,
PRODUCT_ID	INT,
CAMPAIGN INT,
FOREIGN KEY (PRODUCT_ID) references PRODUCT_RAW(PRODUCT_ID),
FOREIGN KEY (CAMPAIGN) references CAMPAIGN_DESC_RAW(CAMPAIGN)
);

CREATE OR REPLACE TABLE COUPON_REDEMPT_RAW
(household_key	INT,
DAY	INT,
COUPON_UPC	INT,
CAMPAIGN INT,
FOREIGN KEY (household_key) references demographic_RAW(household_key),
FOREIGN KEY (CAMPAIGN) references CAMPAIGN_DESC_RAW(CAMPAIGN)
);

CREATE OR REPLACE TABLE TRANSACTION_RAW 
(household_key	INT,
BASKET_ID	INT,
DAY	INT,
PRODUCT_ID	INT,
QUANTITY	INT,
SALES_VALUE	FLOAT,
STORE_ID	INT,
RETAIL_DISC	FLOAT,
TRANS_TIME	INT,
WEEK_NO	INT,
COUPON_DISC	INT,
COUPON_MATCH_DISC INT,
FOREIGN KEY (PRODUCT_ID) references PRODUCT_RAW(PRODUCT_ID),
FOREIGN KEY (household_key) references demographic_RAW(household_key)
);

------------------creating storage interagration-------------------------
----------------------------------------------------AWS (S3) INTEGRATION------------------------------------------------------------------------
CREATE OR REPLACE STORAGE integration s3_int
TYPE = EXTERNAL_STAGE
STORAGE_PROVIDER = S3
ENABLED = TRUE
STORAGE_AWS_ROLE_ARN ='arn:aws:iam::619382079688:role/Retail_role'   ----here arn comes from role created-------
STORAGE_ALLOWED_LOCATIONS =('s3://retailbucket2/');                     ---- location is bucket created------


DESC integration s3_int;    --- this will describe the bucket-----


create or replace file format retail_csv    --- file format needed for stage
    type = 'csv' 
    compression = 'none' 
    field_delimiter = ','
    field_optionally_enclosed_by = 'none'
    skip_header = 1 ;

CREATE OR REPLACE STAGE RETAIL                                 --- stage needed to store data temperorily-----
URL ='s3://retailbucket2'                                      --- this is bucket created----------
file_format = retail_csv
storage_integration = s3_int;

SHOW STAGES;
LIST @RETAIL

--CREATE SNOWPIPE THAT RECOGNISES CSV THAT ARE INGESTED FROM EXTERNAL STAGE AND COPIES THE DATA INTO EXISTING TABLE

--The AUTO_INGEST=true parameter specifies to read 
--- event notifications sent from an S3 bucket to an SQS queue when new data is ready to load.


CREATE OR REPLACE PIPE RETAIL_SNOWPIPE_DEMOGRAPHIC AUTO_INGEST = TRUE AS
COPY INTO "RETAILS"."PUBLIC"."DEMOGRAPHIC_RAW" --yourdatabase -- your schema ---your table
FROM '@RETAIL/DEMOGRAPHIC/' --s3 bucket subfolde4r name
FILE_FORMAT = retail_csv; --YOUR CSV FILE FORMAT NAME

CREATE OR REPLACE PIPE RETAIL_SNOWPIPE_CAMPAIGN_DESC AUTO_INGEST = TRUE AS
COPY INTO "RETAILS"."PUBLIC"."CAMPAIGN_DESC_RAW"
FROM '@RETAIL/CAMPAIGN_DESC/' 
FILE_FORMAT = retail_csv;

CREATE OR REPLACE PIPE RETAIL_SNOWPIPE_CAMPAIGN AUTO_INGEST = TRUE AS
COPY INTO "RETAILS"."PUBLIC"."CAMPAIGN_RAW"
FROM '@RETAIL/CAMPAIGN/' 
FILE_FORMAT = retail_csv;

CREATE OR REPLACE PIPE RETAIL_SNOWPIPE_PRODUCT AUTO_INGEST = TRUE AS
COPY INTO "RETAILS"."PUBLIC"."PRODUCT_RAW"
FROM '@RETAIL/PRODUCT/' 
FILE_FORMAT = retail_csv;


CREATE OR REPLACE PIPE RETAIL_SNOWPIPE_COUPON AUTO_INGEST = TRUE AS
COPY INTO "RETAILS"."PUBLIC"."COUPON_RAW"
FROM '@RETAIL/COUPON/' 
FILE_FORMAT = retail_csv;

CREATE OR REPLACE PIPE RETAIL_SNOWPIPE_COUPON_REDEMPT  AUTO_INGEST = TRUE AS
COPY INTO "RETAILS"."PUBLIC"."COUPON_REDEMPT_RAW"
FROM '@RETAIL/COUPON_REDEMPT/' 
FILE_FORMAT = retail_csv;

CREATE OR REPLACE PIPE RETAIL_SNOWPIPE_TRANSACTION  AUTO_INGEST = TRUE AS
COPY INTO "RETAILS"."PUBLIC"."TRANSACTION_RAW"
FROM '@RETAIL/Transactions/' 
FILE_FORMAT = retail_csv;

SHOW PIPES;

SELECT COUNT(*) FROM demographic_RAW;
SELECT COUNT(*) FROM CAMPAIGN_DESC_RAW;
SELECT COUNT(*) FROM CAMPAIGN_RAW;
SELECT COUNT(*) FROM PRODUCT_RAW;
SELECT COUNT(*) FROM COUPON_RAW;
SELECT COUNT(*) FROM COUPON_REDEMPT_RAW;
SELECT COUNT(*) FROM TRANSACTION_RAW;



----------------------------------------------------------PIPEREFRESH-----------------------------------------------------------------

ALTER PIPE RETAIL_SNOWPIPE_DEMOGRAPHIC refresh;
ALTER PIPE  RETAIL_SNOWPIPE_CAMPAIGN_DESC refresh;
ALTER PIPE  RETAIL_SNOWPIPE_CAMPAIGN refresh;
ALTER PIPE  RETAIL_SNOWPIPE_PRODUCT refresh;
ALTER PIPE  RETAIL_SNOWPIPE_COUPON refresh;
ALTER PIPE  RETAIL_SNOWPIPE_COUPON_REDEMPT refresh;
ALTER PIPE  RETAIL_SNOWPIPE_TRANSACTION refresh;

SELECT * FROM demographic_RAW;
SELECT * FROM CAMPAIGN_DESC_RAW;
SELECT * FROM CAMPAIGN_RAW;
SELECT * FROM PRODUCT_RAW;
SELECT * FROM COUPON_RAW;
SELECT * FROM COUPON_REDEMPT_RAW;
SELECT * FROM TRANSACTION_RAW;

-------------automating stored procedures -------------------------
---- creating database and table-----
create database czechbank
use czechbank

CREATE OR REPLACE TABLE DISTRICT(
District_Code INT PRIMARY KEY	,
District_Name VARCHAR(100)	,
Region VARCHAR(100)	,
No_of_inhabitants	INT,
No_of_municipalities_with_inhabitants_less_499 INT,
No_of_municipalities_with_inhabitants_500_btw_1999	INT,
No_of_municipalities_with_inhabitants_2000_btw_9999	INT,
No_of_municipalities_with_inhabitants_less_10000 INT,	
No_of_cities	INT,
Ratio_of_urban_inhabitants	FLOAT,
Average_salary	INT,
No_of_entrepreneurs_per_1000_inhabitants INT,
No_committed_crime_2017	INT,
No_committed_crime_2018 INT
) ;


CREATE OR REPLACE TABLE ACCOUNT(
account_id INT PRIMARY KEY,
district_id	INT,
frequency	VARCHAR(40),
Date DATE ,
FOREIGN KEY (district_id) references DISTRICT(District_Code) 
);

CREATE OR REPLACE TABLE ORDER_LIST (
order_id	INT PRIMARY KEY,
account_id	INT,
bank_to	VARCHAR(45),
account_to	INT,
amount FLOAT,
FOREIGN KEY (account_id) references ACCOUNT(account_id)
);


CREATE OR REPLACE TABLE LOAN(
loan_id	INT ,
account_id	INT,
Date	DATE,
amount	INT,
duration	INT,
payments	INT,
status VARCHAR(35),
FOREIGN KEY (account_id) references ACCOUNT(account_id)
);


CREATE OR REPLACE TABLE TRANSACTIONS(
trans_id INT,	
account_id	INT,
Date	DATE,
Type	VARCHAR(30),
operation	VARCHAR(40),
amount	INT,
balance	FLOAT,
Purpose	VARCHAR(40),
bank	VARCHAR(45),
account_partner_id INT,
FOREIGN KEY (account_id) references ACCOUNT(account_id));


CREATE OR REPLACE TABLE CLIENT(
client_id	INT PRIMARY KEY,
Sex	CHAR(10),
Birth_date	DATE,
district_id INT,
FOREIGN KEY (district_id) references DISTRICT(District_Code) 
);


CREATE OR REPLACE TABLE DISPOSITION(
disp_id	INT PRIMARY KEY,
client_id INT,
account_id	INT,
type CHAR(15),
FOREIGN KEY (account_id) references ACCOUNT(account_id),
FOREIGN KEY (client_id) references CLIENT(client_id)
);


CREATE OR REPLACE TABLE CARD(
card_id	INT PRIMARY KEY,
disp_id	INT,
type CHAR(10),	
issued DATE,
FOREIGN KEY (disp_id) references DISPOSITION(disp_id)
);

------creating storage integration----------
CREATE OR REPLACE STORAGE INTEGRATION s3_int
TYPE = EXTERNAL_STAGE
STORAGE_PROVIDER = S3
ENABLED = TRUE
STORAGE_AWS_ROLE_ARN = 'arn:aws:iam::619382079688:role/czech_data_role' -- Use the Role ARN from Step 4b
STORAGE_ALLOWED_LOCATIONS = ('s3://czechdatabucket/')

DESC integration s3_int

----------CREATING CSV File Format--------------
CREATE OR REPLACE FILE FORMAT CSV
    TYPE = 'CSV'
    FIELD_OPTIONALLY_ENCLOSED_BY = '"'
    SKIP_HEADER = 1;


-----------creating stage ----------------
CREATE OR REPLACE STAGE CZECH_BANK
URL ='s3://czechdatabucket' -- Use your S3 bucket URL
FILE_FORMAT = CSV
STORAGE_INTEGRATION = s3_int;

CREATE OR REPLACE STAGE CZECH_BANK1
URL ='s3://czechdatabucket/District/' -- Use your S3 bucket URL
FILE_FORMAT = CSV
STORAGE_INTEGRATION = s3_int1;

LIST @CZECH_BANK;

SHOW STAGES;

--CREATE SNOWPIPE THAT RECOGNISES CSV THAT ARE INGESTED FROM EXTERNAL STAGE AND COPIES THE DATA INTO PATIENTS TABLE
--The AUTO_INGEST=true parameter specifies to read event notifications sent from an S3 bucket to an SQS queue when new data is ready to load.


CREATE OR REPLACE PIPE BANK_SNOWPIPE AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."DISTRICT"
FROM '@CZECH_BANK1/DISTRICT/'
FILE_FORMAT = (TYPE = 'CSV');

CREATE OR REPLACE PIPE BANK_SNOWPIPE2 AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."ACCOUNT"
FROM '@CZECH_BANK/Transaction_data/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE3 AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."TRANSACTIONS"
FROM '@CZECH_BANK/Transactions/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE4 AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."DISPOSITION"
FROM '@CZECH_BANK/disp/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE5 AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."CARD"
FROM '@CZECH_BANK/Card/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE6 AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."ORDER_LIST"
FROM '@CZECH_BANK/Order/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE7 AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."LOAN"
FROM '@CZECH_BANK/Loan/'
FILE_FORMAT = CSV;

CREATE OR REPLACE PIPE BANK_SNOWPIPE8 AUTO_INGEST = TRUE AS
COPY INTO "CZECHBANK"."PUBLIC"."CLIENT"
FROM '@CZECH_BANK/Client/'
FILE_FORMAT = CSV;

SHOW PIPES;
select SYSTEM$PIPE_STATUS('BANK_SNOWPIPE3');

SELECT count(*) FROM DISTRICT;
SELECT count(*) FROM ACCOUNT;
SELECT count(*) FROM TRANSACTIONS;
SELECT count(*) FROM DISPOSITION;
SELECT count(*) FROM CARD;
SELECT count(*) FROM ORDER_LIST;
SELECT count(*) FROM LOAN;
SELECT count(*) FROM CLIENT;

ALTER PIPE BANK_SNOWPIPE refresh;

ALTER PIPE BANK_SNOWPIPE2 refresh;

ALTER PIPE BANK_SNOWPIPE3 refresh;

ALTER PIPE BANK_SNOWPIPE4 refresh;

ALTER PIPE BANK_SNOWPIPE5 refresh;

ALTER PIPE BANK_SNOWPIPE6 refresh;

ALTER PIPE BANK_SNOWPIPE7 refresh;

ALTER PIPE BANK_SNOWPIPE8 refresh;
-----------------------------------------------------------------------------------------------------------------------------------------------
SELECT * FROM DISTRICT;
SELECT * FROM ACCOUNT;
SELECT * FROM TRANSACTIONS;
SELECT * FROM DISPOSITION;
SELECT * FROM CARD;
SELECT * FROM ORDER_LIST;
SELECT * FROM LOAN;
SELECT * FROM CLIENT;

----------------------------------------------------------STORE PROCEDURE-------------------------------------------------------------------------
CREATE OR REPLACE PROCEDURE CREAT_OR_REPLACE_ACC_LATEST()
RETURNS STRING
LANGUAGE SQL
AS
$$
  CREATE OR REPLACE TABLE ACC_LATEST_TXNS_WITH_BALANCE 
AS(
SELECT LTD.*,TXN.BALANCE
FROM TRANSACTIONS AS TXN
INNER JOIN 
(
   SELECT ACCOUNT_ID,YEAR(DATE) AS TXN_YEAR,
   MONTH(DATE) AS TXN_MONTH,
   MAX(DATE) AS LATEST_TXN_DATE
   FROM TRANSACTIONS
   GROUP BY 1,2,3
   ORDER BY 1,2,3

) AS LTD ON TXN.ACCOUNT_ID = LTD.ACCOUNT_ID AND TXN.DATE = LTD.LATEST_TXN_DATE
WHERE TXN.TYPE = 'Credit'  -- this is the assumptions am having : month end txn data is credit
ORDER BY TXN.ACCOUNT_ID,LTD.TXN_YEAR,LTD.TXN_MONTH);
$$;

CREATE OR REPLACE PROCEDURE CREATE_OR_REPLACE_BANKINGKPI()
RETURNS STRING
LANGUAGE SQL
AS
$$
  CREATE OR REPLACE TABLE BANKING_KPI AS (
    SELECT ALWB.TXN_YEAR, ALWB.TXN_MONTH, T.BANK,
      COUNT(DISTINCT ALWB.ACCOUNT_ID) AS TOT_ACCOUNT, 
      COUNT(DISTINCT T.TRANS_ID) AS TOT_TXNS,
      COUNT(CASE WHEN T.TYPE = 'Credit' THEN 1 END) AS DEPOSIT_COUNT,
      COUNT(CASE WHEN T.TYPE = 'Withdrawal' THEN 1 END) AS WITHDRAWAL_COUNT,
      SUM(ALWB.BALANCE) AS TOT_BALANCE,
      ROUND((DEPOSIT_COUNT / TOT_TXNS) * 100, 2) AS DEPOSIT_PERC,
      ROUND((WITHDRAWAL_COUNT / TOT_TXNS) * 100, 2) AS WITHDRAWAL_PERC,
      NVL(TOT_BALANCE / TOT_ACCOUNT, 0) AS AVG_BALANCE,
      ROUND(TOT_TXNS / TOT_ACCOUNT, 0) AS TPA
    FROM TRANSACTIONS AS T
    INNER JOIN ACC_LATEST_TXNS_WITH_BALANCE AS ALWB ON T.ACCOUNT_ID = ALWB.ACCOUNT_ID
    GROUP BY 1, 2, 3
    ORDER BY 1, 2, 3
  );
$$;

SHOW PROCEDURES

CALL CREAT_OR_REPLACE_ACC_LATEST();

CALL CREATE_OR_REPLACE_BANKINGKPI();  
  
CREATE OR REPLACE TASK  ACC_LATEST_TXNS_WITH_BALANCE
WAREHOUSE = COMPUTE_WH
SCHEDULE =  '1 MINUTE'
AS CALL CREAT_OR_REPLACE_ACC_LATEST();
  
CREATE OR REPLACE TASK  BANKING_KPI
WAREHOUSE = COMPUTE_WH
SCHEDULE =  '2 MINUTE'
AS CALL CREATE_OR_REPLACE_BANKINGKPI();  
  
SHOW TASKS;  
  
ALTER TASK ACC_LATEST_TXNS_WITH_BALANCE  RESUME;
ALTER TASK ACC_LATEST_TXNS_WITH_BALANCE SUSPEND;  
ALTER TASK  BANKING_KPI RESUME;
ALTER TASK BANKING_KPI SUSPEND;    

  
DROP TASK IF EXISTS ACC_LATEST_TXNS_WITH_BALANCE;
DROP TASK IF EXISTS  BANKING_KPI; 
  
DROP TABLE  ACC_LATEST_TXNS_WITH_BALANCE;
DROP TABLE  BANKING_KPI;  
  
SELECT * FROM ACC_LATEST_TXNS_WITH_BALANCE;
SELECT * FROM BANKING_KPI;  

SHOW TASKS;
SHOW INTEGRATIONS;
DESCRIBE INTEGRATION S3_INT;
