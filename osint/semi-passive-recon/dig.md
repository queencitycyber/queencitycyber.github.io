**DIG**

DIG \(Domain Information Groper\) is a much more powerful alternative than nslookup. For that reason, we will not cover that tool, but for the majority of cases, the two tools are effectively the same. Since DIG is a bit more robust, we will cover it here. DIG is a network administration and troubleshooting tool. It is used to query DNS name servers for information regarding host addresses, name servers \(NS\), mail servers \(MX\), text annotations \(TXT\), A records \(IP address\), or we can default and have all results returned to us by specific the any parameter after our command.

Such a command would be: `dig uc.edu any`

Above, we see a bunch of output. Lets quickly break it down.

On the left hand side underneath the Answer Section column, we see uc.edu, which is the resource we requested. 

We can see an MX record \(mail server\), an A record \(IP address\), a NS record \(name server\), a TXT record \(annotations\), and SOA records \(Start of authority\) which stores information about the name of the server that gave us this data. 

All of these data points should be investigated further and added to your notes!

