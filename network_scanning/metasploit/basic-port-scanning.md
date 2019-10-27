# Basic Port Scanning in MSF

Metasploit is nice because it keeps track of all our information in the database. Then we can query that database to quickly enumerate hosts, listening services, extra info, and even manually add info if we want.

One of the nicest things about being inside the msfconsole is that you can still run just about any other \*nix command.

For example, inside the console, try running an Nmap scan or ping or dig trace on a domain. All these tools  work inside the console.

We can run any Nmap scan we would normally run. But instead we will run it with **db\_nmap** followed by any other arguments we want. The results of this scan will then be stored inside the database where we can the quickly look up the information.

Run a Fast \(top 100 ports, remember?\) Nmap scan against your target. ![](/assets/db_nmap Fastscan.png)

Let's run another scan to get some more information. We can scan any number of ports we want with Nmap - Nmap makes it easy to scan the Top X number of ports with the `- -top-ports X`option.

Run a scan against the top 300 ports with service detection.  
Remember, if you want to go faster, skip pinging the host and resolving hostnames :\)

Let's find some other port scanning capabilities using the msfconsole's `search` function

