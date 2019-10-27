# Basic Introduction to p0f

p0f is a tool used to passively identify operating systems by analyzing certain characteristics on response TCP/IP packets for OS detection and other markers by comparing them to a known database.

Man page:

![](/assets/p0fmanpage.png)

Further down the page, there's info on where the database is.

![](/assets/p0fdb.png)

Let's use the tool. Start by running the tool with `p0f`![](/assets/p0frunning.png)

p0f works by analyzing traffic sent to our machine. We need to convince or force our target machine to send us data.

Any ideas how?

Analyzing HTTP responses for service detection![](/assets/p0fhttp.png)

Analyzing TCP/IP signature for OS detection

![](/assets/p0ftcpip.png)

