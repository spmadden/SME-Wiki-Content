---
title: Precision Timing
description: 
published: 1
date: 2025-08-11T18:52:22.566Z
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

## Scripts
`watchchrony.sh`
```bash
#!/bin/bash

watch -n1 '/usr/local/bin/chronyc -n -m sources sourcestats tracking'
```

`kick_satpulse.service`
```ini
[Unit]
Description=Monitoring service to kick satpulse when it goes off the rails

[Service]
# Block in the 'starting' condition until the exec exits
Type=oneshot
# Kill if the script takes longer than 12h to run
#TimeoutStartSec=12h
ExecStart=/root/kick_satpulse.sh
WorkingDirectory=/root/
StandardOutput=file:/var/log/kick_satpulse.log
StandardError=inherit
```

`kick_satpulse.timer`
```ini
[Unit]
Description=Timer for satpulse monitor

[Timer]
# start 2hr after boot
OnBootSec=0
# only if the service has been quiet for the last 5m
OnUnitInactiveSec=5m
# filename of above service
Unit=kick_satpulse.service

[Install]
WantedBy=multi-user.target
```

`/root/kick_satpulse.sh`
```bash
#!/bin/bash

NUM_FAILS=$(journalctl -n 20 -u satpulse@ttyAMA0.service | grep "failed to emit sample for pulse" | wc -l)
#NUM_FAILS=10
if [[ $NUM_FAILS -gt 10 ]] ; then
        echo "Kicking satpulse because more than 10 fails in last 20 lines"
        journalctl -n 20 -u satpulse@ttyAMA0.service
        systemctl restart satpulse@ttyAMA0.service
fi
```