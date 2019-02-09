# DNS Resolution

_Context: We've determined what MAC address to send our DNS request to (the gateway which will then route it to the local DNS server)._

Now that the network library has the IP address of either our DNS server or the default gateway it can resume the DNS resolution process:

* Port 53 is opened to send a UDP request to a DNS server (if the response size is larger than an allowed UDP datagram, TCP will be used instead).

* If the local/ISP DNS server does not have the entry, then a recursive search is requested and that flows up the list of DNS servers until the SOA (Start of Authority) is reached, and if found an answer is returned.

``www.google.com.`` is recursed as:
``.`` is the root authority
``.com`` is a Top Level Domain (TLD)
``google`` the monolith
``www`` the entry in the domain we're looking for.

![recursive DNS example](https://i.stack.imgur.com/ORZ2C.gif)

The DNS answer is ultimately returned to the LDNS server and then the client. 

_Demonstration Steps:_
* Show Wireshark filer for DNS query
``dns.qry.name == "www.google.com"``

[Socket to Wire](./6-Socket2Wire.md)