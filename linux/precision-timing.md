---
title: Precision Timing
description: 
published: 1
date: 2025-07-24T01:29:43.242Z
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

### CM5 Boot config w/ TB
```ini
[cm5]
dtoverlay=dwc2,dr_mode=host

[all]
arm_freq_min=2300
force_turbo=1
enable_uart=1
dtparam=uart0=on
dtoverlay=uart1
dtoverlay=disable-bt
dtparam=i2c_arm=on
#dtoverlay=i2c_baudrate=400000
dtparam=i2c_vc=off

dtparam=cooling_fan=off
dtparam=pciex1
dtparam=pciex1_gen=2

# Pin 29 wired to FAN_TACH (formerly ETH_SYNC) to pull down and ground errant energy
gpio=29=op,pd,dl
#dtoverlay=pps-gpio,gpiopin=29
# Pin 21 wired to GNSS_RESET, pull and hold low to keep device in reset
gpio=21=op,dl

gpio=20=op,dl
```

### Load I2C-Dev module
```
/etc/modules: 
i2c-dev
i2c-bcm2708
```