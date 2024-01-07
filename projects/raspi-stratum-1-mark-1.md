---
title: Stratum-1 Time Server on a RasPI: Mark 1
description: 
published: 1
date: 2024-01-07T20:57:57.347Z
tags: 
editor: markdown
dateCreated: 2024-01-07T20:57:57.347Z
---

# Stratum-1 Time Server on a RasPI: Mark I

## BOM:
* RasPi Case: [Pilot Gateway Pro LoRa Enclosure Kit for Raspberry Pi 4 - RAK7244](https://www.adafruit.com/product/5057) 
  * ![](https://cdn-shop.adafruit.com/100x75/5057-00.jpg)
* RF Dongle: [SMA to uFL/u.FL/IPX/IPEX RF Adapter Cable](https://www.adafruit.com/product/851)
  * ![](https://cdn-shop.adafruit.com/100x75/851-03.jpg)
* GPS Hat: [Adafruit Ultimate GPS HAT for Raspberry Pi A+/B+/Pi 2/3/Pi 4 - Mini Kit](https://www.adafruit.com/product/2324)
  * ![](https://cdn-shop.adafruit.com/100x75/2324-11.jpg)
* RasPi: [Raspberry Pi 4 Model B - 2 GB RAM](https://www.adafruit.com/product/4292)
  * ![](https://cdn-shop.adafruit.com/100x75/4292-03.jpg)
* Power: [Official Raspberry Pi Power Supply 5.1V 3A with USB C - 1.5 meter long](https://www.adafruit.com/product/4298)
  * ![](https://cdn-shop.adafruit.com/100x75/4298-04.jpg)
* GPS Antenna:
  * Option 1: [GPS Antenna - External Active Antenna - 3-5V 28dB 5 Meter SMA](https://www.adafruit.com/product/960)
    * ![](https://cdn-shop.adafruit.com/100x75/960-04.jpg)
  * Option 2: [MagmaX2 Active Multiband GNSS Magnetic Mount Antenna - AA.200](https://www.sparkfun.com/products/17108)
    * ![](https://cdn.sparkfun.com/r/92-92/assets/parts/1/6/0/7/0/17108-AA.200_____MagmaX2_Active_Multiband_GNSS_Magnetic_Mount_Antenna-01A.jpg)
    
    
## Software Setup:

1. Flash the latest Raspbian OS image (64 bit).
2. Tweak the Base OS Settings:
   1. Disable the Serial Kernel Console by editing `/boot/cmdline.txt` and removing the `console=XYZ` lines, where XYZ is a serial interface (it could be any of `serial0`, `ttyS0` (note the `S`), or `ttyAMA0`)
      * [Doc](https://www.raspberrypi.com/documentation/computers/configuration.html#command-line-options)
      * Alt: Use the `raspi-config` tool: [Disabling the Linux Serial Console](https://www.raspberrypi.com/documentation/computers/configuration.html#disabling-the-linux-serial-console)
   2. Enable the PPS (Pulse Per Second) driver by editing `/boot/config.txt` and adding `dtoverlay=pps-gpio,gpiopin=4` (Pin 4 is the GPS Hat PPS Pin, adjust if different pin)
      * [Doc](https://learn.adafruit.com/adafruit-ultimate-gps-hat-for-raspberry-pi/pinouts#pps-pin-1054766)
3. Reboot
4. Configure GPSd:
   1. Install using apt.
   2. Edit `/etc/default/gpsd` command line to add option `-n` and devices `/dev/ttyS0` `/dev/pps0`
   3. Restart GPSd & verify you're seeing data with `cgps` or `gpsmon`
5. Configure Chrony:
   1. Install using apt.
   2. Edit `/etc/chrony/chrony.conf` and add:
```
refclock SHM 0 poll 4 minsamples 16 refid GPS noselect
refclock PPS /dev/pps0 poll 4 minsamples 16 trust precision 1e-9 refid PPS lock GPS
```

Explanation:
* GPS Line:
  * `refclock SHM 0` uses the NTPd shared-memory segment 0 (provided by GPSd) to source date & time info
  * `poll 4` averages 2^4 (16) seconds worth of data to smooth out jitter (down from default of 2^6/64s)
  * `minsamples 16` keeps the last 16 samples worth of data in memory (up from default of 6)
  * `refid GPS noselect` names this source `GPS` and prohibits chrony from selecting it as the "best source" (9800 baud gives a ~0.2s to ~0.4s delay)
* PPS Line:
  * `refclock PPS /dev/pps0` - self-explantatory, it's a PPS at location `/dev/pps0`
  * `trust` - ensures that chrony doesn't mark this as a "lying sonofabitch" (false-ticker)
  * `precision 1e-9` - This clock has "nanosecond precision" (it doesn't, but otherwise it will assume system-clock precision with a bunch of other errors involved)
  * `refid PPS lock GPS` - names this source `PPS` and since it doesn't provide date & time info, "locks" it to the source named `GPS`'s date & time info
[chrony.conf](https://chrony-project.org/doc/4.4/chrony.conf.html)