**Fierce**

This is a tool that will help us enumerate non-contiguous IP space and hostnames against our target domain. This means that, because it uses DNS, it’s likely to find targets inside and outside of corporate networks that are leaking misconfigured IP addresses and hostnames. This is especially useful when used in conjunction with Nmap. Why? Because this tool may uncover other IP addresses and hostnames that your initial recon may have missed. Once you identify new targets with this tool, you rinse and repeat, uncovering more targets along the way. There are several switches that can be used, however, we will only cover the basics.

Lets start the tool and look at the options with the command `fierce`



Okay, lets use the –dns switch so our command looks like this: `fierce –dns EXAMPLEDOMAIN.TLD`



So the first thing we see the output above is the location of the nameservers for ericonsecurity.com. The next step a zone transfer was attempted; this is okay because we own this target. Remember, zone transfers are used to replicate and transfer the records from one DNS server to other DNS servers. This extraction of information on resources you do not own is a very legal gray area, so don’t point it at things you don’t own! However, if successful \(we failed\), there would be no reason to brute force sub domains if we can get the information straight from the dragons mouth \(or DNS servers mouth in this case\).

Fierce will also search for wildcard DNS entries. Sometimes, domains will include a wildcard entry, which resolves any subdomain regardless if it exists or not. In our case, no entries were found.

Fierce also brute forces and searches for subdomains based on an internal wordlist. This wordlist can be modified or completely replaced with one provided by the user. Often times, a custom wordlist tailored to a specific domain and organization will reveal more results than the default wordlist. This is why it is important to keep good notes on interesting pieces of information; we can use known subdomains, hostnames, usernames, email addresses, contacts, etc in our wordlist, greatly increasing our chances of uncovering more targets!



