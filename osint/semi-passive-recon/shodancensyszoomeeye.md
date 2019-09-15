**Shodan**

Shodan is a unique web application search engine. What separates Shodan from traditional search engines is that Shodan specializes in indexing information found in banners. These banners aren’t always the usual banners such as HTTP, but can also fingerprint FTP, SSH, and Telnet banners. Normal search engines crawl data on web pages and then index that data for searching. Shodan does that, except it indexes banners for searching. You can also uncover printers, VOIP services, hidden security cameras, scada systems, and baby monitors. Shodan can reveal information about virtualization technologies as well. Depending on the information Shodan gathers, you might also reveal key technologies and their version numbers, allowing you to determine certain services are vulnerable to exploitation.

Another similar tool is called Censys and works much the same way as Shodan.




Shodan and Censys are very powerful tools and offers a uniqe search syntax that allows us to narrow our searches accordingly. It also has the ability to generate PDF or HTML reports. Creating an account is free and you get access to the API, though you can a one time fee and get unlimited access to the API as well as other features. Some search filters include:

-city: can be used to refine searches to a certain city. Ex. `city:Cincinnati`

-country: same as city, but two letter country codes are used instead. Ex. `country:CH`

-hostname: searches for computers that include the term in their hostname. Ex. `hostname:starbucks`

-os: searches for the specific operating system. Ex. `os:Linux`



Shodan also has Chrome and Firefox plugins. This makes quickly accessing Shodan very easy. Just browse to the website you wish to fingerpring, and select the icon from your toolbar. This is not even scratching the surface as to the powers of Shodan 

Some may bring up the argument that this tool only fasciliates the hacking community, but our job as pen testers, we ultimately report up to management so that they can implement new security fix, this allows network administrators and security administrators to search their own networks and figure out if they have devices connected to the internet with default passwords.

