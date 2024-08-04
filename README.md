# Bank Database Management with SQL
# Description

This project demonstrates various SQL queries performed on a bank database, showcasing essential database management skills. The queries cover a range of functionalities, from data retrieval and sorting to complex joins and aggregations. This project is ideal for those looking to deepen their understanding of SQL and database interactions within the banking sector.

**Database Structure**

The bank database consists of the following tables:

**Customer Table:**

custid: Customer ID

fname: First Name

mname: Middle Name

lname: Last Name

city: City

mobileno: Mobile Number

occupation: Occupation

dob: Date of Birth

**Account Table:**

acnumber: Account Number

custid: Customer ID (Foreign Key)

aod: Account Open Date

astatus: Account Status

**Branch Table:**

bid: Branch ID

bcity: Branch City

**Loan Table:**

loanid: Loan ID

custid: Customer ID (Foreign Key)

bid: Branch ID (Foreign Key)

loan_amount: Loan Amount

**SQL Queries for Bank Database**

This document provides detailed descriptions of various SQL queries executed on a bank database. Each query is designed to perform specific operations, from data retrieval and sorting to complex joins and aggregations.

**Queries Description**

**1. Ordering Customers by Year of Birth and First Name**

SELECT custid, fname, mname, dob

FROM customer

ORDER BY EXTRACT(YEAR FROM dob), fname ASC;

**2. Concatenating Middle Name or Last Name**

This query selects customer details and concatenates the middle name or the last name, depending on the availability of the middle name.

SELECT custid, fname, IF(mname IS NOT NULL, mname, lname) AS cust_name

FROM customer;

**3. Joining Account and Customer Tables**

This query joins the account and customer tables to retrieve account numbers along with the respective customer details and account open date.

SELECT account.acnumber, customer.custid, customer.fname, customer.lname, account.aod

FROM account

INNER JOIN customer ON account.custid = customer.custid;

**4. Counting Customers in a Specific City**

This query counts the number of customers residing in Delhi.

SELECT (SELECT COUNT(city) FROM customer WHERE city = 'Delhi') AS Cust_Count;

**5. Selecting Accounts Opened After a Certain Date**

This query retrieves customer and account details for accounts opened after the 15th day of any month.

SELECT account.custid, customer.fname, account.acnumber

FROM account, customer

WHERE account.custid = customer.custid AND DAY(aod) > 15;

**6. Distinct Customer Details Based on Occupation**

This query retrieves distinct customer details for customers whose occupation is not business, service, or student.

SELECT DISTINCT customer.fname, customer.city, account.acnumber

FROM account, customer

WHERE account.custid = customer.custid AND NOT(occupation='business' OR occupation='service' OR occupation='student');

**7. Counting Branches by City**

This query counts the number of branches in each city.

SELECT bcity, COUNT(*) AS Count_Branch

FROM branch

GROUP BY bcity;

**8. Active Accounts Details**

This query retrieves account details for accounts that are active.

SELECT account.acnumber, customer.fname, customer.lname

FROM account, customer

WHERE account.custid = customer.custid AND astatus = 'Active';

**9. Loan Information with Customer and Branch Details**

This query retrieves loan details along with the respective customer and branch information.

SELECT customer.custid, customer.fname, branch.bid, loan.loan_amount

FROM ((loan INNER JOIN customer ON loan.custid = customer.custid)

INNER JOIN branch ON loan.bid = branch.bid);

**10. Terminated Accounts Details**

This query retrieves details of accounts that have been terminated.

SELECT account.acnumber, customer.custid, customer.fname, customer.lname, account.astatus

FROM account, customer

WHERE customer.custid = account.custid AND astatus = 'Terminated';

These queries cover a wide range of database operations and are useful for managing and analyzing data within a banking context. They can be executed in any SQL client that supports MySQL.
