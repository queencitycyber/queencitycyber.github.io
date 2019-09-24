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


There's many more tools and advanced techniques used to conduct passive recon, however for this course a basic introduction is all that's needed.

---

## Active Scanning 

### Basic Introduction to Nmap

If you are reading this, you have probably used Nmap before. Nmap \(Network Mapper\) is by far and large the de facto network mapping tool. It was introduced in 1997 and has been in movies such as the Matrix Reloaded, Dredd, Fantastic Four, The Bourne Ultimatum, and many others. Nmap is probably the most robust and expansive tool listed in this entire document, thus covering all topics related to Nmap is practically impossible. Most full length text books don’t teach everything that can be done with Nmap. We will cover the absolute basic techniques.

From their site – “Nmap \(“Network Mapper”\) is a free and open source utility for network discovery and security auditing. Many systems and network administrators also find it useful for tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime. It was designed to rapidly scan large networks, but works fine against single hosts. Nmap runs on all major computer operating systems, and official binary packages are available for Linux, Windows, and Mac OS X.

**Remember: NEVER engage in network scanning and probing techniques unless you have explicit permission by the entity in control of your target. It is very possible you could end up bringing down services, fat-fingering a network address and scanning something entirely different than you though, etc. If you have to ask yourself “Should I be doing this?” The answer is always no. **

**For the purpose of this course, we will be using a combination of localhost, vulnerable web applications internally hosted, and privately owned domains. Unless you own the target you are scanning, or you have permission in your possession, DO NOT scan the target.**

One exception – Nmap gives us explicit permission to scan a resource of theirs, namely **scanme.nmap.org**.

From their site - “You are authorized to scan this machine with Nmap or other port scanners. Try not to hammer on the server too hard. A few scans in a day is fine, but don’t scan 100 times a day or use this site to test your ssh brute-force password cracking tool.” We will absolutely honor this.

Nmap is also very smart. It has several built-in default behaviors that are used to gather as much information as possible. Though sometimes this information is useful and necessary, it can slow down scan times.

The most basic scan can be accomplished by calling Nmap followed by the target; such as nmap scanme.nmap.org. This does a few things.  The SYN scan is the most common and default scan for a few reasons. It is fast, capable of scanning thousands of ports per second, relatively unobtrusive because it does not fully connect \(often called a half-open scan\), and reliably reports on the status of the port.

Let's take a look at a standard, default Nmap scan with no options against **scanme.nmap.org**

Command: `nmap scanme.nmap.org`

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/nmapscanme.png)

**Open: **When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. If we receive a SYN/ACK \(an ACKnowledgement to our SYNchronize\), then the port is reported Open. This means the service being hosted on that particular port probably wants to open a connection with us. Nmap will terminate the connection after this.

**Filtered: **When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. After several seconds, if no response is seen by the target, Nmap will try and reestablish the connection again. If again no response is seen, Nmap will make the port as Filtered. This is usually indicative of the presence of a packet filtering device or a firewall.

**Closed: **When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. One example that might cause Nmap to conclude the port is closed is if we receive a RST \(Reset\). Per RFC, if your host is using a compliant TCP/IP stack, if a TCP SYN packet is sent to a non-listeing port, a RST is sent back telling us this port is closed. This could also be indicative of some application or protection mechanism immediately blocking the connection attempt and the status is reported as Closed.


### OS Detection

By default, Nmap scans the top 1000 ports based on an Internet survey conducted by it's creator. Sometimes, 1000 ports is too much to scan for a variety of reasons. A common and popular switch to reduce 1000 to 100 is **-F**. We will examine and use this option when doing OS detection using Nmap.

Nmap also has the ability to determine the operating system the host is running on. This is done by examining the way different operating systems handle different TCP probes. By having a database of known behavior, Nmap can compare the way different hosts respond to different probes and can determine the operating system. In cases where Nmap is not entirely sure, it will give a confidence rating stating how well it believes the host is on a specific operating system. This option also provides information on system uptime and TCP sequence number prediction.

Why is this important?

Answer this question: What does it mean if a server you’re scanning has been up for 3 years and 6 months? Well, you know most security patches often require reboots and restarts, so if a system has been up for over 3 years, there is a good chance it is missing critical security patches. Why is TCP sequence number prediction important? Well, the sequence number in TCP is one mechanism used to offer reliability in transmission of data. The ISN \(initial sequence number\) is used to start the connection, and this number is a 32-bit integer, which means there are over 4 billion possibilities for this number. If you can sample enough of these numbers \(what Nmap does\), then you can predict the next sequence number, allowing the possibility of hijacking TCP sessions.

Lets take a look at operating system detection. We'll use the -F switch to go from 1000 ports to the top 100 ports with command:`nmap -F –O scanme.nmap.org`

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/nmapscanmefast.png) In red you can see where Nmap chose to scan only 100 ports instead of the default 100.

Below is the same scan with the default 1000. Notice how much longer the scan takes!

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/nmapfastosdetect.png)

### Service Detection

Sometimes knowing that a particular service on a port is not enough information to use. Sometimes, we want to know what versions of BIND \(DNS server\) or Apache \(Web server\) versions are on our host. This can be valuable information in determining whether or not vulnerabilities exist. Keep in mind, sometimes security patches are back-ported to earlier versions and administrators will sometimes spoof version numbers to appear patched. Because of this, and just like every other information you receive, it is always best to try and verify these results and never take anything on faith.

Nmap’s version detection \(-sV\) is powerful and can do things like: determine application name and version number, not just the protocol; both TCP and UDP services are supported; as well as full support for IPv6 on all major operating systems.

Lets take a look at what we can uncover using techniques we have already discussed and break down the output.

Run the command: `nmap -sV scanme.nmap.org`

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/nmapservice.png)

Want to go faster? Don't wait for top 1000 ports, use -F instead and scan top 100 instead!

![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/nmapfastservice.png)

**Remember,** since we are running this as root, default is to use SYN \(half-open\) scan. If we are non-UID 0 \(root\), we don’t have access to raw sockets which means the default scan is then moved to a TCP connect scan \(-sT\). This type of scan is usually less accurate because of the way Nmap handles the scan. This is closer to the behavior of modern web browsers and other network applications.

An entirely different API is used when this scan takes place; rather than reading raw sockets, Nmap will use the Berkley Sockets API, issuing the connect\(\) system call, which is handled by the underlying operating system. Because Nmap does not have as much control over this higher level connection attempt as raw packets, it becomes less efficient.

## Xprobe2

### Basic Introduction to xprobe2

Xprobe2 is another tool used for OS detection, however it is an active tool. It interacts and probes remote systems and compares returned signatures to a known database. It can also scan open ports, but we will use it for OS detection in the next section as we have better, more robust tools like Nmap for scanning open ports

Man page:![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/xprobeman.png)

Examples from man page:![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/xprobeexmaples.png)

## Massscan

### Basic Introduction to Masscan


Masscan is really awesome. The main about Masscan that is different is it's speed. 

From the author - " This is the fastest Internet port scanner. It can scan the entire Internet in under 6 minutes, transmitting 10 million packets per second."  

Masscan is really fast for a couple reasons:

1. Custom TCP/IP network stack
2. Packets are generated and sent asynchronously 



Masscan is also very similiar to Nmap. It even has an --nmap switch to see what Nmap compatibility  switches are available.

Run `masscan --nmap` to view what switches are similar across Nmap and Masscan


Masscan can do service detection. However, it does it in a more roundabout way than Nmap.

Masscan does service detection by banner grabbing.

For exmaple, let's look at service detection using Masscan and Nmap

First, run --nmap to see comparable options to Nmap.![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/network%20scanning/assets/masscanbanner.png)

The switch `--banners`looks like what we want.







