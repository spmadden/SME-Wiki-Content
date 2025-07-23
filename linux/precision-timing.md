---
title: Precision Timing
description: 
published: 1
date: 2025-07-23T23:55:08.274Z
tags: 
editor: markdown
dateCreated: 2025-07-23T23:55:08.274Z
---


# Standard Linux Configs

* Disable packet coalescing
```bash
# check values with:
ethtool -c eth0

# reduce/minimize values
ethtool -C eth0 rx-usecs 0
ethtool -C eth0 tx-usecs 0
ethtool -C eth0 tx-frames 1
ethtool -C eth0 rx-frames 1
```