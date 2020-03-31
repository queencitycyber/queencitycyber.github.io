It's important to understand different networking technologies and how they relate and are used in capturing traffic that isn't intended for your machine.

Hubs - When a packet hits a networking hub, that packet is sent to every host attached to the hub. This can be useful in some situations, but from a security standpoint, being able to receive packets that weren't intended for your machine doesn't sound very good.

Switches - When a packet hits a networking switch, there is a bit more magic that takes place to send that packet to the correct machine. These are the most popular and are obviously more secure. So in order to sniff traffic that isn't intended for us, we will need to convince other machines on the network to send their packets to us via man-in-the-middle.

By default, your computers NIC \(network interface card\) will ignore all packets that were not addressed to it originally. But what if we want to receive all the packets on the network, even if they weren't supposed to come to us? We can instruct our NIC to do this. This is referred to as** promiscuous mode.**

Summary:

* Hubs are not smart and will send everything to everyone on the network = insecure!
* Switches are smart and will properly route traffic to the intended hosts = more secure than hubs!

If the above information isn't clear, here is a helpful site: https://www.tamos.com/htmlhelp/monitoring/







