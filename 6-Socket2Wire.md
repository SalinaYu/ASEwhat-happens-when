# Socket to Wire

_Context: Now we know the destination of our HTTP request from the DNS resolution process. Now we need to make a TCP connection to that destination (in order to send our HTTP request)_

Once the browser receives the IP address of the destination server, it takes that and the given port number from the URL (typically HTTP is port 80 and HTTPS is port 443), and makes a call to the system library function named ``socket`` and requests a TCP socket stream - ``AF_INET/AF_INET6`` and ``SOCK_STREAM``. Here is where we start building the TCP connection. This process starts with a SYN (synchronization) packet.

* This request is first passed to the Transport Layer (_OSI layer 4_)where a TCP segment is crafted. The destination port is added to the header, and a source port is chosen from within the kernel's dynamic port range (ip_local_port_range in Linux).
![TCP header](https://i.stack.imgur.com/bSNbI.jpg)
* This segment is sent to the Network Layer (_OSI layer 3_), which wraps an additional IP header. The IP address of the destination server as well as that of the current machine is inserted to form a packet.
![IP header](https://upload.wikimedia.org/wikipedia/commons/5/54/Ipv4_header.svg)
* The packet next arrives at the Link Layer (_OSI layer 2_). A frame header is added that includes the MAC address of the machine's NIC as well as the MAC address of the gateway (local router). 
![Ethernet header](https://upload.wikimedia.org/wikipedia/commons/thumb/1/13/Ethernet_Type_II_Frame_format.svg/2880px-Ethernet_Type_II_Frame_format.svg.png)
* As before, if the kernel does not know the MAC address of the gateway, it must broadcast an ARP query to find it (_but in this case the ARP entry is cached as we've just looked it up/constantly been using it_). 

_Demonstration Step:_
* Show the established connection (refer to Wireshark for resolved destination IP address)
```bash
$ netstat -an | grep 216.58.192.196
```

[Packet hits the wire](./7-Packet2Wire.md)