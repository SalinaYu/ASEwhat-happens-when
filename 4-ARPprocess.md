# ARP process

_Context: Sending an arp request to resolve a DNS server or my local gateway. "Where do I need to send this DNS request to?"_

_OSI Layer(s): 2->3_

[ARP glue](https://3.bp.blogspot.com/-0X__afMPRdE/U8wNRzDGNdI/AAAAAAAAAYA/BPx196yRQvo/s1600/ARP-OSI-Model.jpeg)

In order to send an ARP ([Address Resolution Protocol](https://tools.ietf.org/html/rfc826)) broadcast the network stack library needs the target IP address to look up. It also needs to know the MAC address of the interface it will use to send out the ARP broadcast.

The local ARP cache is first checked for an ARP entry for our target IP. If it is in the cache, the library function returns the result: Target IP = MAC.

If the entry is not in the ARP cache:

* The route table is looked up, to see if the Target IP address is on any of the subnets on the local route table. If it is, the library uses the interface associated with that subnet. If it is not, the library uses the interface that has the subnet of our default gateway.

* The MAC address of the selected network interface is looked up.

* The network library sends a Layer 2 (data link layer of the `OSI model`) ``ARP Request`` destined for the identified MAC ("``Who has`` this IP address?").

_Context: ARPing for the gateway as we assume the Local DNS server is not in the same subnet_

Depending on what type of hardware is between the computer and the router determines the next step. If directly connected the router will answer with an ``ARP Reply``. If connected to a hub then your compute belongs in 1995 but your ARP request will be sent out all the hub ports and the router will respond with an ``ARP reply``. 

Most likely, your computer is connected to a switch. 

* The switch will check its local CAM/MAC table to see which port has the MAC address we are looking for. If the switch has no entry for the MAC address it will rebroadcast the ARP request to all other ports.

* If the switch has an entry in the MAC/CAM table it will send the ARP request to the port that has the MAC address we are looking for.

* Presumably the router is on the same L2 broadcast domain and will respond with an ``ARP Reply``. Your machine will then cache that for some duration of time (20 min for most *nix OSs).

_Demonstration Steps:_
* Show the arp cache
```bash
$ arp -a
```
* Show Wireshark filter for arps to/from the default gateway
``arp.src.proto_ipv4 == 10.10.0.1``

[Next: DNS Resolution](./5-DNSresolution.md)