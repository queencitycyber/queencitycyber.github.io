Source: https://www.owasp.org/index.php/Path\_Traversal  
Source: https://www.owasp.org/index.php/Testing\_Directory\_traversal/file\_include\_\(OTG-AUTHZ-001\)  


Introduction to Directory or Path Traversal 

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





