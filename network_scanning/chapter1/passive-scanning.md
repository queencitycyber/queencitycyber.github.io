## Passive Scanning

* Our primary goal here, again, is to keep the number of packets we send to a target system as little as possible. To do efficient analysis, we need to master the art of analyzing responses, not actively probing.

There are several ways to do passive analysis on a target. One of the most common ways is network traffic analysis and a tool that does this will is p0f. We will examine this tool in the next session.

### Basic Introduction to p0f

p0f is a tool used to passively identify operating systems by analyzing certain characteristics on response TCP/IP packets for OS detection and other markers by comparing them to a known database.

Man page:

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/p0fmanpage.png)

Further down the page, there's info on where the database is.

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/p0fdb.png)

Let's use the tool. Start by running the tool with `p0f`![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/p0frunning.png)

p0f works by analyzing traffic sent to our machine. We need to convince or force our target machine to send us data.

Any ideas how?

Analyzing HTTP responses for service detection![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/p0fhttp.png)

Analyzing TCP/IP signature for OS detection

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/p0ftcpip.png)


There's many more tools and advanced techniques used to conduct passive recon, however for this course a basic introduction is all that's needed.