# Web Application Vulnerabilities 

This material will briefly introduce web application technologies, their associated vulnerabilities, and how to identify + exploit them.

# The Mindset:

Remember, you're a researcher/tinkerer/hacker! Think like one!

Ask yourself questions like:

* What does this button/input form/combination of letters + numbers do?
  * Ex: A pizza delivery web site might ask for your address: what happens if I enter in a phone number? 10 phone numbers?
  * Ex: A web application might have a forum/discussion board and asks for your name: what if I enter HTML characters into the name form?

---


As we saw with XSS, SQLi, and Path Traversal vulnerabilities, as very common and ripe place for these to occur is from user-supplied input!

So any place you see things like "**file=/welcome/resources/private/public.txt**", or "**user=charles**", or "**Enter your name:\_\_\_\_\_**", ask yourself:

* What if I request "/welcome/resources/private/bad.txt"? Or what happens if I just browse to "/welcome/resources/private"?
* What if I request "user=; SELECT \* FROM \*"? 
* What if I entered "&lt;script&gt;echo\("Evil Was Here"\); &lt;/script&gt;" when a website asks for my name?



Of course, only test on things you own or have permission to! :\)

---

# Cross Site Scripting (XSS)

Source: https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)

Source: https://www.acunetix.com/websitesecurity/cross-site-scripting/

**Scenario A:** A web application might have a forum/discussion board and asks for your name: what if I enter HTML characters into the name form?

Lots!

### Introduction to Cross-Site Scripting \(XSS\): 

* 2 main types: Reflected and Stored. We will cover reflected.

* XSS is an injection vulnerability that occurs when an application does not properly sanitize \(clean/normalize\) input supplied by a user.

* The user supplied data \(code\) is incorrectly interpretted/handled by the web application and executes inside the browser.
* The malicious code can be anything, but Javascript is often the go to for it's massive web-based presence. Others might inlcude VBScript, Flash, or ActiveX.
* Targets the website/application, not a particular user.

Example HTML code within a web application:

```
print "<html>"
print "<h1>Most recent comment</h1>"
print database.latestComment
print "</html>"
```

**Description:** When a user visits the web page above, the server is sending the HTML to the victims browser. The victims browser interprets the HTML and displays the web page. This web page is presented and the browser executes the `database.lastestComment` and displays the last made comment.

**Attack: **What happens if we make a comment using Javascript instead of normal text?  
A commonly used example: `<script>DoSomethingEvil();</script>`

So when a user visits the web page, instead of the last comment being presented, the evil script is executing inside the browser.

Okay, so an attacker can trick a web application into executing Javascript. So what?

With a reflected XSS, an attacker could:

1. Steal session cookies and impersonate a user.
2. Execute seperate HTTP requests to malicious websites
3. Many, many more malicious things.

**Recap:** XSS occurs when a web site/application accepts input supplied by you \(the user\) \*without\* properly handling the inputted data. Whenever you see a website \(including the URL!\) accepting input from you \(the user\), there's a potential for XSS exploitation.

---

# SQL Injection (SQLi)

Source: https://www.owasp.org/index.php/SQL\_Injection  
Source: https://www.acunetix.com/websitesecurity/sql-injection2/

### Introduction to SQL Injection \(SQLi\)

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

---

# Directory Traversal (Path Traversal)

Source: https://www.owasp.org/index.php/Path_Traversal 
 


### Introduction to Directory or Path Traversal 

* ANOTHER injection vulnerability \(noticing a pattern? :\) \)

* Occurs when an application does not properly sanitize \(clean/normalize\) input supplied by a user.

* Instead of the supplied data being interpretted by a browser \(XSS\), or the data being constructed into a SQL query \(SQLi\), the data is used to construct paths or locations of specific resources we want access to.

* Can be OS or application based. 

Common variable manipulation:

1. "../" &lt;- dot dot slash

**Example using static resource argument:**

1. A user requests an HTML web page titled "boring.html" with the following HTTP command.
   1. http://example.com/getUserProfile.jsp?item=boring.html
2. The web server returns the HTML page. 
3. Instead of requesting "boring.html", how about something juicy?
   1. http://example.com/getUserProfile.jsp?item=../../../../etc/passwd
4. BONUS: What do we know about the system above? This is why our recon is so valuable!

Note: In the above scenario, the vulnerable web application would need to have the proper permissions to read/return the resource.

**Example using file upload functionaility:**

1. http://example.com/index.php?file=http://www.owasp.org/malicioustxt

**Recap: **A directory/path traversal vulnerability occurs when a web site/application accepts input supplied by you \(the user\) \*without\* properly handling the inputted data. 











