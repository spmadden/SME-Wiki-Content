---
title: Falsehoods Programmers Believe About Networking
description: 
published: 1
date: 2023-12-02T21:59:41.139Z
tags: 
editor: markdown
dateCreated: 2023-12-02T21:56:29.227Z
---

# Falsehoods Programmers Believe About Networking


1. Data on the network cannot be altered.
2. Encrypted data on the network cannot be altered.
3. Data cannot be accidentally corrupted, because TCP has checksums and Ethernet has CRCs
4. If it's inside my perimeter firewall, that means I have total control over it 
5. If it doesn't return an error, then `send()` sent all the data that was asked of it.
6. Packets arrive in the order in which they were sent.
7. Segment boundaries on a TCP stream are meaningful to the application.
8. Segment boundaries on a TCP stream are not meaningful to the application.
9. If you can't ping the target, then it doesn't exist. 
10. If you can ping the target, then it does exist.
11. TCP RSTs come from end-nodes.
12. Bytes must be "swapped" from the network byte-order to the host CPU byte-order.
13. It's an internal web app -- outsiders won't be able to discover where it is 
14. The DHCP address will be the same after a reboot 
15. The DHCP address will remain the same until the next reboot.
16. Well, it'll last a long time between changes
17. Packets/PDUs go up or down the network stack, never sideways. 
18. The IPv4 header is 20 bytes long starting with `0x45` (options are so rare we don't have to worry about them) 
19. The DHCP server and local router are the same 
20. There is no IPv6 on my network 
21. NAT automatically blocks all inbound attacks 
22. We know all the devices attached to our network at any given time 
23. VLANs are just as good as physical segmentation.
24. Ok, VLANs aren't as good, but they are good enough for now.
25. We have good WIPS/monitors, so we don't have rogue access-points anywhere. 
26. No need to add it to the DNS; I'll remember it. 
26. Source address checking is sufficient security.
26. The local network has zero latency and infinite bandwidth.
26. Packets are never duplicated.
26. Duplicated packets are never corrupted.
26. My edge routers won't try to route out RFC1918 address packets.
26. My edge routers won't accept packets with RFC1918 addresses.
26. The RFC1918 addresses I pick for this network will never collide with any other network that it may connect to or VPN to.
26. The MTU is always 1500 octets.
26. The MTU is never more than 1500 octets.
26. Putting raw IPv4 addresses into higher layer content (such as URLs in web pages) is okay.
26. The DNS resolver in the end node will round robin DNS servers.
26. The DNS resolver in the end node will always pick the first DNS server.
26. The DNS resolver in the end node will never repeat a query until it's cache times out.
26. The DNS resolver in the end node will cache queries.
26. TCP connections will have *some* traffic at least every minute/hour/day/week.
26. Packets coming from the local router with a from address of the local net are never valid.
26. Packets coming from "surprising" sources with "surprising" From addresses are never valid.
26. Nothing important is using multicast.
26. I can block ICMP for "security reasons" without breaking anything important.
26. I can block all packet types except ICMP, UDP, and TCP, for "security reasons", without breaking anything important.
26. I can block all ethernet packet types except for IPv4 without breaking anything important.
26. The only address ever used in 127/8 is 127.0.0.1
26. Nobody uses 169.254/16 for anything important.
26. 169.254/16 isn't special.
26. The same device will always get the same 169.254/16 address.
26. I can hardcode a 169.254/16 address into my IP stack or configuration.
26. What is this 169.254/16?
26. Nobody uses dialup PPP anymore.
26. Especially not over an expensive sat link.
26. Ethernet MAC addresses are *always* unique.
26. I can tell if I'm in a VM container by looking at the local interface's MAC address.
26. No manufacturer of Ethernet hardware has ever just made up a prefix without registering with the IEEE.
26. No manufacturer of Ethernet hardware has ever just stolen someone else's prefix.
26. The same goes for manufacturers of cell phone towers. They would NEVER use a duplicated or unregistered tower ID.
26. The network interfaces on an end node will always come up in the same order, with the same names and numbers, with the same MAC addresses, connected to the same networks, every time the node boots up.
26. A network interface always has a unique MAC address.
26. Or at least some sort of globally unique layer 2 address.
26. Or at least some sort of locally unique layer 2 address.
26. Or some sort of address at all? 