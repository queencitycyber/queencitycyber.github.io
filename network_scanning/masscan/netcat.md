# Brief Introduction to Netcat

* A cheetsheet you might find helpful [https://www.sans.org/security-resources/sec560/netcat\_cheat\_sheet\_v1.pdf](https://www.sans.org/security-resources/sec560/netcat_cheat_sheet_v1.pdf)
* This may also be useful [https://coderwall.com/p/pd78eg/using-nc-netcat-as-a-port-scanner-in-linux](https://coderwall.com/p/pd78eg/using-nc-netcat-as-a-port-scanner-in-linux)
* [http://www.pythonforbeginners.com/modules-in-python/how-to-use-simplehttpserver/](http://www.pythonforbeginners.com/modules-in-python/how-to-use-simplehttpserver/)

From the manpage:

![](/assets/ncman.png)

Netcat, or simply nc, is a simple yet powerful tool that is used to send data back and forth between two ports.

For purposes here, we will be using netcat to conduct port scans, but it can send any kind of data across networks. For example, netcat can be used as a web server, a backup tool, and monitoring tool, and compression/decompression tool, file watcher, etc.

In essence, any service that sends data between one process on a computer to another process somewhere else, local or remote, netcat can probably mimick that behavior. We will be conducting port scans using netcat.

Before port scanning though, let's take a brief look at netcat and how it works.  
Start by entering `nc -h` on the command line to bring up the help.![](/assets/nchelp.png)

So we first need to listen on a port. Pick any port. Now connect to that port.

![](/assets/nclisten.png)

Note: In the vast majority of cases, the -v option will stand for verbosity. It's often helpful to run tools with this switch so you can view any error messages or other information that may be a part of the tools default output.

Now in another terminal \(control + shift + t\), use netcat to connect to that port. Send some data and go back to your listening session :\)

