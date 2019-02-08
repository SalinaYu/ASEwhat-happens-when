# DNS Resolution

Now that the network library has the IP address of either our DNS server or the default gateway it can resume the DNS resolution process:

* Port 53 is opened to send a UDP request to a DNS server (if the response size is too large, TCP will be used instead).
* If the local/ISP DNS server does not have the entry, then a recursive search is requested and that flows up the list of DNS servers until the SOA (Start of Authority) is reached, and if found an answer is returned.
![recursive DNS example](https://i.stack.imgur.com/ORZ2C.gif)

_DEMO_
* Show Wireshark filer for DNS query
``dns.qry.name == "www.google.com"``

[Socket to Wire](6-Socket2Wire.md)