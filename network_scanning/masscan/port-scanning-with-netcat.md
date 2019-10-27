# Port Scanning with Netcat

Okay so we briefly looked at how we can pass data back and forth between two listening network services. If you think about it, this is essentially what any port scanner is - the port scanning application \(nmap/netcat/masscan/etc\) is sending network packets to one system, and listening for the responses to those connections.

So lets do that with netcat!

The first thing we need is a target with some listening network services. Back to scanme.nmap.org. ![](/assets/netcatscanme.png)

Note: Notice by default netcat does name resolution? We can omit that feature with the -n switch.

So we know port 80 is open. Let's try to scan a range of ports.

