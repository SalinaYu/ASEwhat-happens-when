# DNS Resolution

_Context: We've determined the MAC address for the destination IP address for our DNS request (the gateway which will then route the request to the local DNS server). We need this DNS request resolved to determine the destination IP address for our HTTP/S request._

_OSI Layer(s): 7_

Now that the network library has the MAC and IP address of either our DNS server or the default gateway it can resume the DNS resolution process:

* Port 53 is opened to send a UDP request to a DNS server (if the response size is larger than an allowed UDP datagram, TCP will be used instead).

* If the local DNS server does not have the entry, then a recursive search is requested and that flows up the list of DNS servers until the SOA (Start of Authority) is reached, and if found an answer is returned.

``www.google.com.`` (notice the .dot at the end) is recursed as:

* ``.`` is the [root authority](https://en.wikipedia.org/wiki/Root_name_server)

* ``.com.`` is a [Top Level Domain (TLD)](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

* ``google.com.`` the monolith

* ``www.google.com.`` the entry in the domain we're looking for.

![recursive DNS example](https://i.stack.imgur.com/ORZ2C.gif)

The DNS answer is ultimately returned to the LDNS server (and likely cached for the duration of the ttl) and then the client. 

_Demonstration Steps:_
* Show Wireshark filer for DNS query (from machine to LDSN server)
``dns.qry.name == "www.google.com"``
  * note that the destination IP address is our local DNS server and the destination MAC is our local gateway.
* Use ``dig`` to show recursion which was performed by LDNS server
```bash
dig +trace www.google.com
```

[Next: Socket to Wire](./6-Socket2Wire.md)