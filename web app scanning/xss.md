Source: [https://www.owasp.org/index.php/Cross-site\_Scripting\_\(XSS\](https://www.owasp.org/index.php/Cross-site_Scripting_%28XSS\)\)  
Source: [https://www.acunetix.com/websitesecurity/cross-site-scripting/](https://www.acunetix.com/websitesecurity/cross-site-scripting/)

**Scenario A: **A web application might have a forum/discussion board and asks for your name: what if I enter HTML characters into the name form?

Lots!

Introduction to Cross-Site Scripting \(XSS\): 

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

**Recap: **XSS occurs when a web site/application accepts input supplied by you \(the user\) \*without\* properly handling the inputted data. Whenever you see a website \(including the URL!\) accepting input from you \(the user\), there's a potential for XSS exploitation.

