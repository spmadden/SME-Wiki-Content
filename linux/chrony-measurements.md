---
title: Precision Time Measurement Config for Chrony
description: 
published: 1
date: 2025-09-11T15:52:44.511Z
tags: 
editor: markdown
dateCreated: 2025-09-11T15:52:44.511Z
---

# Header


 SPM's recommended measurement config for chrony v4.7

 Notes & Recommendations:
1. Don't use any of the 'pool' addresses as the underlying clock can 'switch' at any time, skewing the measurement comparisons.
2. Stay Polite!  Keep the NIST/USNO sources at min/maxpoll 4 = 2^4 seconds = 1 every 16 seconds.

>   NOTE:  Standard ARP timeouts around 30s, so this is an important number to avoid ARP requests
>          adding noise to measurements.
{.is-info}

3. A Chrony->Chrony sync can use `extfield F323` to more rapidly converge.  This is a nonstandard extension, and many NTP implementations like the TP4100 and NIST don't support it (yet).
4. The reference sources are all combined together to create a virtual "clock" that chrony compares against the local RTC and other sources.  Measurement sources are marked 'noselect' so they don't skew/impact the "clean reference virtual clock" created by the reference sources.
5. With high sample rates (minpoll/maxpoll = 0 = 2^0 = 1s interval) the standard sample retention policies actually reduce accuracy because noise is multiplied.  Have chrony keep a longer sample baseline to smooth out high-rate noise with `maxsamples 64`
6. Recommend starting chronyd with the following options (usually /etc/default/chrony):
   `-r -R -m`
   `-r` : reload dump files from past exit
   `-R` : don't immediately step the clock, only slew it, good for restarting the service
   `-m` : lock the process into memory so it's not paged out, eliminates a source of noise.
7. The 'local DNAT Bullshit' can be enabled using the following bash script (run at boot as root).
 ```bash
!/bin/bash
EXTIP=71.174.114.62
iptables -t nat -A OUTPUT -p udp -d 127.0.123.6 --dport 123 -j DNAT --to-destination $EXTIP:123
iptables -t nat -A OUTPUT -p udp -d 127.0.123.7 --dport 123 -j DNAT --to-destination $EXTIP:124
iptables -t nat -A OUTPUT -p udp -d 127.0.123.8 --dport 123 -j DNAT --to-destination $EXTIP:126
iptables -t nat -A OUTPUT -p udp -d 127.0.123.13 --dport 123 -j DNAT --to-destination $EXTIP:125
iptables -t nat -A POSTROUTING -j MASQUERADE
sysctl -w net.ipv4.conf.all.route_localnet=1
```
---
### AIO Config File
```properties
######
#
# SPM's recommended measurement config for chrony v4.7
#
# Notes & Recommendations:
# 1. Don't use any of the 'pool' addresses as the underlying clock can 'switch'
#    at any time, skewing the measurement comparisons.
# 2. Stay Polite!  Keep the NIST/USNO sources at min/maxpoll 4 = 2^4 seconds = 1 every 16 seconds.
#    NOTE:  Standard ARP timeouts around 30s, so this is an important number to avoid ARP requests
#           adding noise to measurements.
# 3. A Chrony->Chrony sync can use 'extfield F323' to more rapidly converge.  This is a nonstandard
#    extension, and many NTP implementations like the TP4100 and NIST don't support it (yet).
# 4. The reference sources are all combined together to create a virtual "clock" that chrony compares
#    against the local RTC and other sources.  Measurement sources are marked 'noselect' so they
#    don't skew/impact the "clean reference virtual clock" created by the reference sources.
# 5. With high sample rates (minpoll/maxpoll = 0 = 2^0 = 1s interval) the standard sample retention
#    policies actually reduce accuracy because noise is multiplied.  Have chrony keep a longer sample
#    baseline to smooth out high-rate nosie with 'maxsamples 64'
# 6. Recommend starting chronyd with the following options (usually /etc/default/chrony):
# 		-r -R -m
#    -r : reload dump files from past exit
#    -R : don't immediately step the clock, only slew it, good for restarting the service
#    -m : lock the process into memory so it's not paged out, eliminates a source of noise.
# 7. The 'local DNAT Bullshit' can be enabled using the following bash script (run at boot as root).
# ```bash
#!/bin/bash
#EXTIP=71.174.114.62
#iptables -t nat -A OUTPUT -p udp -d 127.0.123.6 --dport 123 -j DNAT --to-destination $EXTIP:123
#iptables -t nat -A OUTPUT -p udp -d 127.0.123.7 --dport 123 -j DNAT --to-destination $EXTIP:124
#iptables -t nat -A OUTPUT -p udp -d 127.0.123.8 --dport 123 -j DNAT --to-destination $EXTIP:126
#iptables -t nat -A OUTPUT -p udp -d 127.0.123.13 --dport 123 -j DNAT --to-destination $EXTIP:125
#iptables -t nat -A POSTROUTING -j MASQUERADE
#sysctl -w net.ipv4.conf.all.route_localnet=1
#```
#
#####

### The following are various "pools" that can be used.  NOT RECOMMENDED FOR HIGH-ACCURACY MEASUREMENTS.
#pool ntp.ubuntu.com        iburst maxsources 4
#pool 0.ubuntu.pool.ntp.org iburst maxsources 1
#pool 1.ubuntu.pool.ntp.org iburst maxsources 1
#pool 2.ubuntu.pool.ntp.org iburst maxsources 2
#pool time.aws.com iburst maxsources 5 minpoll 4 maxpoll 6 noselect presend 6 xleave
#pool time.nist.gov iburst maxsources 5 minpoll 4 maxpoll 6 presend 6 noselect

#!!----------------------------------------------------------------------------
#!! The following are various connections to SPM's personal setup.
#!!
#!! RPI4-KRONOS: Raspi4B w/ Adafruit GPS Hat - ~20ns measured accuracy
#!!
#!! Public IP 74.174.114.62
server newrobotorder.com iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!! Public IPv6
#server 2001:470:8b54::6 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!! Local DNAT Routing bullshit to work around chrony's one-IP-per-server limitation 
#!! 127.0.123.6 = 71.174.114.62:123
#server 127.0.123.6 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!! Local internal network address, won't work w/o VPN to SPM's site.
#server 10.169.0.6 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!!
#!! CM5-LEAM4T: Raspi-CM5 w/ Timebeat TimeCardMini Rev B - ~20ns measured accuracy
#!! https://support.timebeat.app/hc/en-gb/articles/8782340549010-Raspberry-Pi-CM4-multi-constellation-GPS-GNSS-module
#!!
#!! Public IPv6
#server 2001:470:8b54::7 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!!  Local DNAT Routing bullshit to work around chrony's one-IP-per-server limitation 
#!! 127.0.123.7 = 71.174.114.62:124
#server 127.0.123.7 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!! Local internal network address, won't work w/o VPN to SPM's site.
#server 10.169.0.7 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!!
#!! CM4-LEAM4T: Raspi-CM4 w/ Timebeat TimeCardMini RevB - ~20ns measured accuracy
#!!
#!! Public IPv6
#server 2001:470:8b54::13 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!!  Local DNAT Routing bullshit to work around chrony's one-IP-per-server limitation 
#!! 127.0.123.13 = 71.174.114.62:125
#server 127.0.123.13 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!! Local internal network address, won't work w/o VPN to SPM's site.
#server 10.169.0.13 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!!
#!! PI5-KRONOS: Raspi5B w/ TimeHatV6 - ~20ns measured accuracy
#!! https://www.tindie.com/products/timeappliances/timehat-i226-nic-with-pps-inout-for-rpi5/
#!!
#!! Public IPv6
#server 2001:470:8b54::8 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!!  Local DNAT Routing bullshit to work around chrony's one-IP-per-server limitation 
#!! 127.0.123.8 = 71.174.114.62:126
#server 127.0.123.8 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64
#
#!! Local internal network address, won't work w/o VPN to SPM's site.
#server 10.169.0.8 iburst minpoll 0 maxpoll 0 xleave extfield F323 maxsamples 64

#!!
#!! Reference Sources to compare against.
#!!
server time-a-g.nist.gov maxpoll 4 minpoll 4 iburst 
server time-b-g.nist.gov maxpoll 4 minpoll 4 iburst 
server time-c-g.nist.gov maxpoll 4 minpoll 4 iburst 
server time-d-g.nist.gov maxpoll 4 minpoll 4 iburst 
server time-e-g.nist.gov maxpoll 4 minpoll 4 iburst 
server time-a-b.nist.gov maxpoll 4 minpoll 4 iburst 
server time-b-b.nist.gov maxpoll 4 minpoll 4 iburst 
server time-c-b.nist.gov maxpoll 4 minpoll 4 iburst 
server time-d-b.nist.gov maxpoll 4 minpoll 4 iburst 
server time-e-b.nist.gov maxpoll 4 minpoll 4 iburst 
server tick.usno.navy.mil maxpoll 4 minpoll 4 iburst 
server tock.usno.navy.mil maxpoll 4 minpoll 4 iburst 
server ntp2.usno.navy.mil maxpoll 4 minpoll 4 iburst 

#!! Log a bunch of relevant statistics for later processing
log tracking statistics selection rtc rawmeasurements tempcomp

#!! Set the expedited forwarding IP headers, sometimes has an impact, sometimes doesn't.
dscp 46

#!! Set up the ability to query chrony using chronyc remotely.
#!! NOTE: Only commands that should have NO command/control ability are permitted ('opencommands')
#!! this is required for some tracking that Nate's done in the past.
bindcmdaddress 0.0.0.0
bindcmdaddress ::
bindcmdaddress /run/chrony/chronyd.sock
cmdallow 10.0.0.0/8
cmdallow 172.16.0.0/12
cmdallow 192.168.0.0/16
cmdallow 127.0.0.0/8
cmdallow ::1/128
opencommands activity clients ntpdata rtcdata smoothing sources sourcestats tracking sourcename selectdata

# allow all external queries
allow all

# Enable HW Timestamping for better accuracy
hwtimestamp *

# This directive specify the file into which chronyd will store the rate
# information.
driftfile /var/lib/chrony/chrony.drift

# Save NTS keys and cookies.
ntsdumpdir /var/lib/chrony

# Log files location.
logdir /var/log/chrony

# Stop bad estimates upsetting machine clock.
maxupdateskew 100.0

# This directive enables kernel synchronisation (every 11 minutes) of the
# real-time clock. Note that it can't be used along with the 'rtcfile' directive.
rtcsync

# Step the system clock instead of slewing it if the adjustment is larger than
# one second, but only in the first three clock updates.
makestep 1 3

# Prefer frequency accuracy over local time accuracy.  Comment this out if on a system with
# a shitty local oscillator (or virtualized and not backed by a PHC). default value 3
corrtimeratio 6

# Get TAI-UTC offset and leap seconds from the system tz database.
# This directive must be commented out when using time sources serving
# leap-smeared time.
leapsectz right/UTC

# on exit, dump the internal state here for quick & easy reloading.
dumpdir /var/run/chrony

```