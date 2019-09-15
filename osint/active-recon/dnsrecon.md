**Dnsenum**

This tool is designed to gather as much information as possible about a domain. It is a multithread Python script which can help us extract information such as: A Records, which map hostnames to IP addresses; PTR, Pointer records map IP addresses to hostnames; MX Records, mail exchange identifies the mail servers; NS, nameservers identify other nameservers within the domain; AXFR Queries, A Record zone transfer requests is a mechanism to replicate information specific to one individual DNS server to other DNS severs; think of it as a crude and rudimentary GPO rules for DNS servers.

Usage of this tool is pretty straight forward, with some options to help reach more accurate results.

WARNING: Do not direct this command at any resource you do not own! 

There exists legal precedent in regards unauthorized zone transfers, which was deemed illegal in 2008 by a judge in North Dakota stating nothing short “that requesting a zone transfer from a public DNS server is criminal activity…”


More information on this tool can be found here: https://github.com/darkoperator/dnsrecon

