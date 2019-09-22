By default, Nmap scans the top 1000 ports based on an Internet survey conducted by it's creator. Sometimes, 1000 ports is too much to scan for a variety of reasons. A common and popular switch to reduce 1000 to 100 is **-F**. We will examine and use this option when doing OS detection using Nmap.

Nmap also has the ability to determine the operating system the host is running on. This is done by examining the way different operating systems handle different TCP probes. By having a database of known behavior, Nmap can compare the way different hosts respond to different probes and can determine the operating system. In cases where Nmap is not entirely sure, it will give a confidence rating stating how well it believes the host is on a specific operating system. This option also provides information on system uptime and TCP sequence number prediction.

Why is this important?

Answer this question: What does it mean if a server you’re scanning has been up for 3 years and 6 months? Well, you know most security patches often require reboots and restarts, so if a system has been up for over 3 years, there is a good chance it is missing critical security patches. Why is TCP sequence number prediction important? Well, the sequence number in TCP is one mechanism used to offer reliability in transmission of data. The ISN \(initial sequence number\) is used to start the connection, and this number is a 32-bit integer, which means there are over 4 billion possibilities for this number. If you can sample enough of these numbers \(what Nmap does\), then you can predict the next sequence number, allowing the possibility of hijacking TCP sessions.

Lets take a look at operating system detection. We'll use the -F switch to go from 1000 ports to the top 100 ports with command:`nmap -F –O scanme.nmap.org`

![](/assets/nmapscanmefast.png)In red you can see where Nmap chose to scan only 100 ports instead of the default 100.

Below is the same scan with the default 1000. Notice how much longer the scan takes!

![](/assets/nmapfastosdetect.png)

