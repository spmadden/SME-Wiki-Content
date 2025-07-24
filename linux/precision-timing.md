---
title: Precision Timing
description: 
published: 1
date: 2025-07-24T00:44:09.188Z
tags: 
editor: markdown
dateCreated: 2025-07-23T23:55:08.274Z
---


# Standard Linux Configs

### Disable packet coalescing
```bash
# check values with:
ethtool -c eth0

# reduce/minimize values
ethtool -C eth0 rx-usecs 0
ethtool -C eth0 tx-usecs 0
ethtool -C eth0 tx-frames 1
ethtool -C eth0 rx-frames 1
```


### CM4/5 GNSS Reset nonesense to let the NIC normalize
```bash
sleep 5

pinctrl set 29 no    # FAN_TACH/GPIO29 disable
pinctrl set 20 no    # reset GPIO20 to float
pinctrl set 21 op dl # pull GPIO21 down to cause GNSS Reset
sleep 1              # pause
pinctrl set 21 op dh # pull GPIO21 up to release GNSS Reset
pinctrl set 21 no    # reset GPIO21 to float
sleep 5
```
