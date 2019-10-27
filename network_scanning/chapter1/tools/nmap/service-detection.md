Sometimes knowing that a particular service on a port is not enough information to use. Sometimes, we want to know what versions of BIND \(DNS server\) or Apache \(Web server\) versions are on our host. This can be valuable information in determining whether or not vulnerabilities exist. Keep in mind, sometimes security patches are back-ported to earlier versions and administrators will sometimes spoof version numbers to appear patched. Because of this, and just like every other information you receive, it is always best to try and verify these results and never take anything on faith.

Nmap’s version detection \(-sV\) is powerful and can do things like: determine application name and version number, not just the protocol; both TCP and UDP services are supported; as well as full support for IPv6 on all major operating systems.

Lets take a look at what we can uncover using techniques we have already discussed and break down the output.

Run the command: `nmap -sV scanme.nmap.org`

![](/assets/nmapservice.png)

Want to go faster? Don't wait for top 1000 ports, use -F instead and scan top 100 instead!

![](/assets/nmapfastservice.png)

**Remember,** since we are running this as root, default is to use SYN \(half-open\) scan. If we are non-UID 0 \(root\), we don’t have access to raw sockets which means the default scan is then moved to a TCP connect scan \(-sT\). This type of scan is usually less accurate because of the way Nmap handles the scan. This is closer to the behavior of modern web browsers and other network applications.

An entirely different API is used when this scan takes place; rather than reading raw sockets, Nmap will use the Berkley Sockets API, issuing the connect\(\) system call, which is handled by the underlying operating system. Because Nmap does not have as much control over this higher level connection attempt as raw packets, it becomes less efficient.

