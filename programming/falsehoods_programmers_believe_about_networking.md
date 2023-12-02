---
title: Falsehoods Programmers Believe About Networking
description: 
published: 1
date: 2023-12-02T21:56:29.227Z
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
