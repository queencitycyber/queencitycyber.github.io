Source: https://www.owasp.org/index.php/SQL\_Injection  
Source: https://www.acunetix.com/websitesecurity/sql-injection2/

Introduction to SQL Injection \(SQLi\)

* Another injection vulnerability!

* Many types

* Occurs when an application does not properly sanitize \(clean/normalize\) input supplied by a user.

* Instead of the supplied data being interpretted by a browser, the data is constructed into a SQL query and executed.

Common SQL query commands:

1. SELECT
   1. SELECT firstName,lastName FROM tableCity1 WHERE population &gt; "20,000"
2. UPDATE
   1. UPDATE tableCity1 FROM firstName,lastName WHERE id=44
3. INSERT
   1. INSERT firstName,quizGrade INTO finalgradeTable \(100\)

Example SQL query flow

* Web application constructs queries as strings -&gt; sends to backend database -&gt; database runs query -&gt; database fetches data -&gt; returns data to application
* SQLi vulnerabilities most often occurs during the first stage: building the query.
* An attacker will construct a \*valid\* SQL query that the database will interpret, run, and return the data back to the attacker

Obligatory Bobby Tables XKCD reference: https://xkcd.com/327/  
A detailed explanation: https://www.explainxkcd.com/wiki/index.php/Little\_Bobby\_Tables

**Vulnerable SQL query:**

```
database.execute("INSERT INTO students (name) VALUES ('" + name + "');");
```

**Benign SQL query:**

```
INSERT INTO students (name) VALUES ('Jerry');
```

**Description:** The above SQL query is: INSERTing the name variable INTO the "students" table with a VALUE of "Jerry"

With a normal name like Jerry, the SQL query is constructed, sent to the database, executed, and data returned/updated.

What happens with a name like Little Bobby Tables \(\(Robert'\); DROP TABLE students;--'\);\)\) ?

**Malicious SQL query:**

```
INSERT INTO students (name) VALUES ('Robert'); DROP TABLE students;--');
```

**Description:** What is the happening above?



With a SQLi vulnerability, an attacker could

1. UPDATE/INSERT a database that keeps track of student loan history
2. SELECT sensitive health records 
3. DROP entire tables or columns from a database
4. DELETE entire databases

**Recap: **SQLi occurs when a web site/application accepts input supplied by you \(the user\) \*without\* properly handling the inputted data. The inputted data is then transformed into a SQL query, executed by a database, and results returned back to you!

