# Basic Introduction to Nmap

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

![](/assets/nmapscanme.png)

**Open: **When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. If we receive a SYN/ACK \(an ACKnowledgement to our SYNchronize\), then the port is reported Open. This means the service being hosted on that particular port probably wants to open a connection with us. Nmap will terminate the connection after this.

**Filtered: **When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. After several seconds, if no response is seen by the target, Nmap will try and reestablish the connection again. If again no response is seen, Nmap will make the port as Filtered. This is usually indicative of the presence of a packet filtering device or a firewall.

**Closed: **When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. One example that might cause Nmap to conclude the port is closed is if we receive a RST \(Reset\). Per RFC, if your host is using a compliant TCP/IP stack, if a TCP SYN packet is sent to a non-listeing port, a RST is sent back telling us this port is closed. This could also be indicative of some application or protection mechanism immediately blocking the connection attempt and the status is reported as Closed.

