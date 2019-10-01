# A recap on what we've done and where we are

The 5 primary steps in a successful penetration test

What we've done

1. \[x\] Reconnaissance

2. \[x\] Port Scanning

3. \[x\] Vulnerability Scanning

---

Where we are

1. \[ \] Network Traffic Analysis
   1. TCP/UDP/HTTP Basics
   2. Sniffing traffic
      1. Tools and techniques
   3. Crafting packets
      1. Tools and techniques
   4. File Carving
      1. Tools and techniques

---

What we have left

1. \[\] Password Cracking

2. \[ \] Exploitation 

3. \[ \] FW/IDS/IPS Evasion

4. \[ \] Post-Exploitation/Lateral Movement

5. \[ \] Report Writing




Network traffic analysis and sniffing are vital skills to a penetration tester. In this module, we will go over proper definitions, different tools and techniques used for sniffing, how to analyze network traffic and the different common protocols, as well as extracting files from pcaps!

Useful resources:

1. http://proquest.safaribooksonline.com/book/software-engineering-and-development/software-testing/9781457185342/iidot-assessments/ch07\_html



### Introduction to Wireshark

Chances are you've used Wireshark in the past. We will be using Wireshark to sniff and interpret network traffic to and from other local machines within our network.

There are a number of network sniffing/protocol analysis tools that are similar to Wireshark and we will briefly touch on them as well, but given Wiresharks ubiquitous use in the infosec field, we will use that whenever possible.



Wireshark is a GUI application that can sniff, analyze, and decode hundreds of different protocols. For example, Wireshark can decode VoIP \(Voice over IP\) packets, and can reconstruct them and can play back audio of a phone conversation.



It's important to understand different networking technologies and how they relate and are used in capturing traffic that isn't intended for your machine.

Hubs - When a packet hits a networking hub, that packet is sent to every host attached to the hub. This can be useful in some situations, but from a security standpoint, being able to receive packets that weren't intended for your machine doesn't sound very good.

Switches - When a packet hits a networking switch, there is a bit more magic that takes place to send that packet to the correct machine. These are the most popular and are obviously more secure. So in order to sniff traffic that isn't intended for us, we will need to convince other machines on the network to send their packets to us via man-in-the-middle.

By default, your computers NIC \(network interface card\) will ignore all packets that were not addressed to it originally. But what if we want to receive all the packets on the network, even if they weren't supposed to come to us? We can instruct our NIC to do this. This is referred to as** promiscuous mode.**

Summary:

* Hubs are not smart and will send everything to everyone on the network = insecure!
* Switches are smart and will properly route traffic to the intended hosts = more secure than hubs!

If the above information isn't clear, here is a helpful site: https://www.tamos.com/htmlhelp/monitoring/




While both these terms might be used interchangeably, they are not quite the same. Understanding the difference is important.



**Sniffing - **Listening covertly for packets on a network. You're copying and recording packets off the wire. For all practical intents and purposes, sniffing is completely undetectable. 

**Spoofing - **Lying overtly for packets on a network. You are tricking/convincing/fooling other hosts on the network you are someone your're not. 



  
ARP, or Address Resolution Protocol, is a communications protocol.

ARP translates or converts network addresses \(IP address\) to link-layer addresses \(MAC address\).



Wikipedia has a great example of how ARP is used on a local network.![](https://github.com/queencitycyber/queencitycyber.github.io/blob/master/traffic%20analysis/assets/arp.PNG)



Since we will be inside \(virtual\) switched environment, we need a way to get our Kali \(attacking\) machine in between what we want to attack and some other destination, like an FTP or web server. This is called a man in the middle \(MITM\) attack and is a very popular attack, especially during internal penetration tests.



