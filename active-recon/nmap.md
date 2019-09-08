**Nmap**

Nmap \(Network Mapper\) is by far and large the de facto network mapping tool. It was introduced in 1997 and has been in movies such as the Matrix Reloaded, Dredd, Fantastic Four, The Bourne Ultimatum, and many others. Nmap is probably the most robust and expansive tool listed in this entire document, thus covering all topics related to Nmap is practically impossible. Most full length text books don’t teach everything that can be done with Nmap. We will cover the absolute basic techniques.

From their site – “Nmap \("Network Mapper"\) is a free and open source utility for network discovery and security auditing. Many systems and network administrators also find it useful for tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime. It was designed to rapidly scan large networks, but works fine against single hosts. Nmap runs on all major computer operating systems, and official binary packages are available for Linux, Windows, and Mac OS X.

We will cover four basic scanning techniques: Ping scanning; TCP scanning; Version scanning; and OS detection. Make sure you run all commands as root!::.

\*\*Remember: NEVER engage in network scanning and probing techniques unless you have explicit permission by the entity in control of your target. It is very possible you could end up bringing down services,fat-fingering a network address and scanning something entirely different than you though, etc. If you have to ask yourself “Should I be doing this?” The answer is always no. For the purpose of this framework, we will be using a combination of localhost, vulnerable web applications internally hosted, and privately owned domains. Unless you own the target you are scanning, or you have permission in your possession, DO NOT scan the target.\*\*

One exception – Nmap gives us explicit permission to scan a resource of theirs, namely **scanme.nmap.org**. From their site - “You are authorized to scan this machine with Nmap or other port scanners. Try not to hammer on the server too hard. A few scans in a day is fine, but don’t scan 100 times a day or use this site to test your ssh brute-force password cracking tool.” We will absolutely honor this.

_Note:_ A behavior to remember about Nmap is that there are two separate phases in a scan; the discovery phase and the scan phase. Understanding, that by default, if Nmap cannot discover the host, it will not attempt to scan the host. Why is this important? Because sometimes you may know a particular host is up, but Nmap will not scan the host because it believes it is down. That means we have to tell Nmap “We know the host is up, just scan it anyway” This is done with the `–P0` option \(zero, not the letter\). So remember, if Nmap discovers the host, it will scan the host. If it cannot discover the host, it will not scan the host \(unless we include the appropriate options\)

**Ping Scanning**

Often times, we just quickly want to get a quick inventory of our network without doing any port scanning afterwards. This is done with the –sP option. This command simultaneously sends out an ICMP echo request \(ping\), as well as a TCP packet with the ACK flag set sent to port 80. 

**TCP Scanning**

The most basic scan can be accomplished by calling Nmap followed by the target; such as nmap scanme.nmap.org. This does a few things. By default Nmap performs a TCP SYN scan \(-sS\), and scans the top 1000 most common ports \(we can also specify specific ports with the –p option , nmap -p22,23,80 scanme.nmap.org\). The SYN scan is the most common and default scan for a few reasons. It is fast, capable of scanning thousands of ports per second, relatively unobtrusive because it does not fully connect \(often called a half-open scan\), and reliably reports on the status of the port.

**Open:** When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. If we receive a SYN/ACK \(an ACKnowledgement to our SYNchronize\), then the port is reported Open. This means the service being hosted on that particular port probably wants to open a connection with us. Nmap will terminate the connection after this.

**Filtered:** When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. After several seconds, if no response is seen by the target, Nmap will try and reestablish the connection again. If again no response is seen, Nmap will make the port as Filtered. This is usually indicative of the presence of a packet filtering device or a firewall.

**Closed:** When we send a packet with the synchronize bit set in the TCP header \(SYN\), we are pretending to open a real connection. One example that might cause Nmap to conclude the port is closed is if we receive a RST \(Reset\). Per RFC, if your host is using a compliant TCP/IP stack, if a TCP SYN packet is sent to a non-listeing port, a RST is sent back telling us this port is closed. This could also be indicative of some application or protection mechanism immediately blocking the connection attempt and the status is reported as Closed.

**Version Scanning**

Sometimes knowing that a particular service on a port is not enough information to use. Sometimes, we want to know what versions of BIND \(DNS server\) or Apache \(Web server\) versions are on our host. This can be valuable information in determining whether or not vulnerabilities exist. Keep in mind, sometimes security patches are back-ported to earlier versions and administrators will sometimes spoof version numbers to appear patched. Because of this, and just like every other information you receive, it is always best to try and verify these results and never take anything on faith. Nmap’s version detection \(-sV\) is powerful and can do things like: determine application name and version number, not just the protocol; both TCP and UDP services are supported; as well as full support for IPv6 on all major operating systems.



**Operating System Detection**

Nmap also has the ability to determine the operating system the host is running on. This is done by examining the way different operating systems handle different TCP probes. By having a database of known behavior, Nmap can compare the way different hosts respond to different probes and can determine the operating system. In cases where Nmap is not entirely sure, it will give a confidence rating stating how well it believes the host is on a specific operating system. This option also provides information on system uptime and TCP sequence number prediction.



