# Introduction to Port Scanning with Kali Linux & Metasploit

Cheatsheets you may find helpful.

Common ports - [http://packetlife.net/media/library/23/common\_ports.pdf](http://packetlife.net/media/library/23/common_ports.pdf)

Linux - [http://www.thecrazyprogrammer.com/2016/02/kali-linux-commands-list-cheat-sheet.html](http://www.thecrazyprogrammer.com/2016/02/kali-linux-commands-list-cheat-sheet.html) or   
Another good one - [http://images.linoxide.com/linux-cheat-sheet.pdf](http://images.linoxide.com/linux-cheat-sheet.pdf)

Nmap - [https://www.stationx.net/nmap-cheat-sheet/](https://www.stationx.net/nmap-cheat-sheet/)

# Summary

* [Recap](recap.md)
* [Introduction](README.md)
* [Kali Linux](kali-linux.md)
* [Metasploit](metasploit.md)
  * [Metasploit Architecture ](metasploit/metasploit-architecture.md)
  * [Starting Metasploit ](metasploit/port-scanning-in-metasploit.md)
  * [Basic Port Scanning ](metasploit/basic-port-scanning.md)
* [Tools](chapter1.md)
  * [Passive Scanning](chapter1/active-scanning.md)
    * [p0f](chapter1/active-scanning/nmap.md)
  * [Active Scanning](chapter1/tools.md)
    * [Nmap](chapter1/tools/nmap.md)
      * [OS Detection](chapter1/tools/nmap/os-detection.md)
      * [Service Detection](chapter1/tools/nmap/service-detection.md)
    * [Xprobe2](chapter1/tools/xprobe2.md)
    * [Masscan](chapter1/tools/masscan.md)
      * [Service Detection](chapter1/tools/masscan/service-detection.md)
* [Manual Tools](masscan.md)
  * [Netcat](masscan/netcat.md)
  * [Port Scanning with Netcat](masscan/port-scanning-with-netcat.md)




# A recap on what we've done and where we are

The 5 primary steps in a successful penetration test

What we've done

1. [x] Reconnaissance 
   1. Passive
   2. Semi-Passive
   3. Active

Where we are

1. [ ] Enumeration
   1. Port Scanning
   2. Service Detection

---

What we have left

1. [ ] Exploitation
   1. tbd
2. [ ] Post-Exploitation/Lateral Movement
3. [ ] Report Writing



---

# What Kali Linux is

* "Kali Linux is a Debian-based Linux distribution aimed at advanced Penetration Testing and Security Auditing" - Offensive Security \(maintainers of Kali\). That's it. It's a flavor of Linux, based on Debian, that has hundreds of pre-installed tools.

# What Kali isn't

* Kali is not a
  * "hacking tool"
  * "penetration test"

# Features of Kali Linux

* Over 600 tools pre-installed. This makes it extremely convenient and easy to get things going. 
  * For a full listing of tools, [click here](https://tools.kali.org/tools-listing)
* Free and open source.
  * Git tree can be found [here](http://git.kali.org/gitweb/)
* Highly customization. If we have time during the course, we will explore customizing the kernel. 
  * More information can be found [here](https://docs.kali.org/category/development)
* Metasploit Framework is installed and works out of the box. This is where we will be doing most of our work from.



---

# Introduction to the Metasploit Framework

### What is Metasploit?

* Metasploit is penetration testing software provided by Rapid7. Mostly paid versions that come in several different varieties, namely Metasploit Pro, Metasploit Ultimate, and Metasploit Express. We will not be using these.

### What is Metasploit Framework?

* Metasploit Framework \(msf\) is the free and open source fork of Metasploit provided by Rapid7.
* MSF is a platform that combines several different sets of tools and applications used for vulnerability analysis, exploit development, and security auditing into a modulated platform. 
* It contains the built in architecture and tools to conduct vulnerability assessments and penetration tests, along with numerous other security related tasks.

#### During this course we will mostly be following the Metasploit Unleashed course, a free ethical hacking course provided by Offensive Security.

Full link here - https://www.offensive-security.com/metasploit-unleashed/

### 

### The Metasploit File System

![](https://www.offensive-security.com/wp-content/uploads/2018/05/msfu-lib0-1.png)

# Starting Metasploit 

## Getting msf running

msf = Metasploit Framework

The first thing we need to do to get up and running is start the  PostgreSQL database. This is the database that will store all our current working information and allow us to query the database to find different modules.

To start the database, run `systemctl postgresql start`. It should exit cleanly.


Then we need to create and initialize the database with `msfdb init.`

And finally start the Metasploit console by entering `msfconsole`

Make sure you're connect with `> db_status`


## Basic Port Scanning in MSF

Metasploit is nice because it keeps track of all our information in the database. Then we can query that database to quickly enumerate hosts, listening services, extra info, and even manually add info if we want.

One of the nicest things about being inside the msfconsole is that you can still run just about any other \*nix command.

For example, inside the console, try running an Nmap scan or ping or dig trace on a domain. All these tools  work inside the console.

We can run any Nmap scan we would normally run. But instead we will run it with **db\_nmap** followed by any other arguments we want. The results of this scan will then be stored inside the database where we can the quickly look up the information.

Run a Fast \(top 100 ports, remember?\) Nmap scan against your target. 

Let's run another scan to get some more information. We can scan any number of ports we want with Nmap - Nmap makes it easy to scan the Top X number of ports with the `- -top-ports X`option.

Run a scan against the top 300 ports with service detection.  
Remember, if you want to go faster, skip pinging the host and resolving hostnames :\)

Let's find some other port scanning capabilities using the msfconsole's `search` function


---
---

# Tools

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



