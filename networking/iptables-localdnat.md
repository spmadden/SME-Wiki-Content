---
title: Localhost DNAT Shenanigans
description: 
published: 1
date: 2025-07-18T23:24:25.545Z
tags: 
editor: markdown
dateCreated: 2025-07-18T23:24:25.545Z
---


```
iptables -t nat -A OUTPUT -p udp -d 127.0.123.6 --dport 123 -j DNAT --to-destination <externalip>:123
iptables -t nat -A OUTPUT -p udp -d 127.0.123.7 --dport 123 -j DNAT --to-destination <externalip>:124
iptables -t nat -A POSTROUTING -j MASQUERADE
sysctl -w net.ipv4.conf.all.route_localnet=1

```