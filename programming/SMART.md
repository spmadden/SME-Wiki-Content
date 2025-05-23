---
title: Seagate SMART
description: 
published: 1
date: 2025-05-23T18:43:33.632Z
tags: 
editor: markdown
dateCreated: 2025-05-23T18:43:33.632Z
---


From http://forums.seagate.com/t5/Desktop-HDD-Desktop-SSHD/Seagate-s-Seek-Error-Rate-Raw-Read-Error-Rate-and-Hardware-ECC/td-p/122382


Desktop HDD, Desktop SSHD, Barracuda, DiamondMax and other desktop SATA and
IDE drives

fzabkar
Seagate's Seek Error Rate, Raw Read Error Rate, and Hardware ECC Recovered
SMART attributes
[ Edited ] 

09-14-2011 11:44 PM - edited 09-15-2011 01:28 AM 

Seagate's Seek Error Rate, Raw Read Error Rate, and Hardware ECC Recovered
SMART attributes create a lot of anxiety amongst Seagate users. This is
because the raw values are typically very high, and the normalised values
(Current / Worst / Threshold) are usually quite low. Despite this, the numbers
in most cases are perfectly OK.

The anxiety arises because we intuitively expect that the normalised values
should reflect a "health" score, with 100 being the ideal value. Similarly, we
would expect that the raw values should reflect an error count, in which case
a value of 0 would be most desirable. However, Seagate calculates and applies
these attribute values in a counterintuitive way. 

In fact the normalised values of Seagate's Seek Error Rate, Raw Read Error
Rate, and Hardware ECC Recovered attributes are logarithmic, not linear, and
the raw values are sector counts or seek counts, not error counts.

Seagate's SMART documentation is not publicly available. The following
information has not been gleaned from any official source, but is based on my
own testing and observation, and on testing by others. Therefore it may
contain errors. 


## Seek Error Rate

The raw value of each SMART attribute occupies 48 bits. Seagate's Seek Error
Rate attribute consists of two parts -- a 16-bit count of seek errors in the
uppermost 4 nibbles, and a 32-bit count of seeks in the lowermost 8 nibbles. In
order to see these data, we will need a SMART utility that reports all 48 bits,
preferably in hexadecimal. Two such utilities are HD Sentinel and HDDScan.

I believe the relationship between the raw and normalised values of the SER
attribute is given by ... 

 normalised SER = -10 log (lifetime seek errors / lifetime seeks) 

In the above formula, if the drive has recorded no errors, then we would still
need to set the number of errors to 1, otherwise the result would be
indeterminate. 

The following table correlates the normalised SER against the actual error
rate:
```
  90 =  <= 1 error per 1000 million seeks
  80 =  <= 1 error per 100 million
  70 =  <= 1 error per 10 million
  60 =  <= 1 error per million
  50 =   10 errors per million
  40 =  100 errors per million
  30 = 1000 errors per million
  20 =   10 errors per thousand
```
A drive that has not yet recorded 1 million seeks will show 100 and 253 for the
Current and Worst values. I believe this is because the data are not considered
to be statistically significant until the drive has recorded 1 million seeks.
When this target is reached, the values drop to 60 and 60, assuming there have
been no errors. 

By way of example, here are the SMART data for my 13GB Seagate HDD:
http://www.users.on.net/~fzabkar/SmartUDM/13GB.RPT
```
 Attribute                 ID Threshold Value Worst Raw         
 ===============================================================
 Seek Error Rate           7     30       53    38  052E0E3000EC

[Mirror of full content of above URL:

                    SMARTUDM - HDD S.M.A.R.T. Viewer 2.00
                    Copyright (C) 2001-2003,  Sysinfo Lab
                    Copyright (C) 1997, Michael Radchenko
             www.sysinfolab.com   e-mail: support@sysinfolab.com

  HDD 1 Model:          ST313021A                               
  HDD 1 Size:           12419 Mb (12.13 Gb)
  Location:             Primary Master   
  Serial Number:        6CT0C4JE            
  Controller Revision:  3.03    
  Buffer Size:          512.0 kb
  Compatibility:        ATA/ATAPI-5
  PIO Mode Support:     4
  SW DMA Mode Support:  None
  MW DMA Mode Support:  2, Active: None
  UDMA Mode Support:    4 (UltraDMA/66), Active: 2
  Current AAM Value:    None
  S.M.A.R.T.:           [*] enabled
  SMART Self-test:      [ ]
  SMART Error Logging:  [ ]

  T.E.C. prediction monitoring started at: 31-08-07, 19:24:22
  Attribute                 ID Threshold Value Indicator  1/Month   T.E.C.
----------------------------------------------------------------------------
  Raw Read Error Rate       1      0       79  ========     0.0    Unknown     
  Spin Up Time              3      0       98  ==========   0.0    Unknown     
* Start/Stop Count          4     20       96  ==========   0.0    Unknown     
* Reallocated Sector Count  5     36       98  ==========   0.0    Unknown     
* Seek Error Rate           7     30       53  =====        0.0    Unknown     
  Power On Hours Count      9      0      247  ==========   0.0    Unknown     
* Spin Retry Count          10    90      100  ==========   0.0    Unknown     
* Drive Power Cycle Count   12     0       96  ==========   0.0    Unknown     
  Current Pending Sector    197    0      100  ==========   0.0    Unknown     
  Uncorrectable Sector      198    0      100  ==========   0.0    Unknown     
  UltraDMA CRC Error Rate   199    0      200  ==========   0.0    Unknown     
----------------------------------------------------------------------------
NOTE: "*" means life-critical attribute
  T.E.C. not detected.

  Attribute                 ID Threshold Value Worst Raw            Type
----------------------------------------------------------------------------
  Raw Read Error Rate       1      0       79    78  00000753BA8Eh  ER
  Spin Up Time              3      0       98    97  000000000000h  PR
* Start/Stop Count          4     20       96    96  000000001131h  EC
* Reallocated Sector Count  5     36       98    98  000000000077h  EC
* Seek Error Rate           7     30       53    38  052E0E3000ECh  ER
  Power On Hours Count      9      0      247     1  0000000026C7h  EC
* Spin Retry Count          10    90      100   100  000000000000h  EC
* Drive Power Cycle Count   12     0       96    96  00000000135Fh  EC
  Current Pending Sector    197    0      100   100  000000000001h  EC SP
  Uncorrectable Sector      198    0      100   100  000000000000h  EC SP
  UltraDMA CRC Error Rate   199    0      200   200  000000000000h  ER
----------------------------------------------------------------------------
NOTE: "*" means life-critical attribute
Attribute types:
      PR - Performance-related         ER - Error rate
      EC - Events count                SP - Self-preserve

  Reallocated Sectors:      119
  Current Temperature:      Not Supported
  Drive Power Cycle Count:  4959
```

]

The number of lifetime seek errors = 0x052E (uppermost 4 nibbles)

The number of lifetime seeks = 0x0E3000EC (lowermost 8 nibbles)

Using Google's calculator ...

 0x052E = 1326
 0x0E3000EC = 238 026 988

http://www.google.com/search?q=0x052E+in+decimal
http://www.google.com/search?q=0x0E3000EC+in+decimal

Applying the formula ...

 normalised SER = -10 log (0x052E / 0x0E3000EC) 

http://www.google.com/search?q=-10+log+(0x052E+/+0x0E3000EC)

... we get a result of 52.54.

Here is a second example:
http://www.users.on.net/~fzabkar/SmartUDM/120GB.RPT

```
 Attribute                 ID Threshold Value Worst Raw         
 ===============================================================
 Seek Error Rate           7     30       79    60  00000580A6AC

[Mirror of full content of above URL:

                    SMARTUDM - HDD S.M.A.R.T. Viewer 2.00
                    Copyright (C) 2001-2003,  Sysinfo Lab
                    Copyright (C) 1997, Michael Radchenko
             www.sysinfolab.com   e-mail: support@sysinfolab.com

  HDD 1 Model:          ST3120026A                              
  HDD 1 Size:           114473 Mb (111.79 Gb)
  Location:             Primary Master   
  Serial Number:        3JT4R9H9            
  Controller Revision:  8.01    
  Buffer Size:          8192.0 kb
  Compatibility:        ATA/ATAPI-6 revision 27
  PIO Mode Support:     4
  SW DMA Mode Support:  None
  MW DMA Mode Support:  2, Active: None
  UDMA Mode Support:    5 (UltraDMA/100), Active: 5
  Current AAM Value:    00h (80h recommended) - disabled
  S.M.A.R.T.:           [*] enabled
  SMART Self-test:      [*] enabled
  SMART Error Logging:  [*] enabled

  T.E.C. prediction monitoring started at: 01-09-07, 09:11:00
  Attribute                 ID Threshold Value Indicator  1/Month   T.E.C.
----------------------------------------------------------------------------
* Raw Read Error Rate       1      6       64  ======       0.0    Unknown     
* Spin Up Time              3      0       96  ==========   0.0    Unknown     
  Start/Stop Count          4     20      100  ==========   0.0    Unknown     
* Reallocated Sector Count  5     36      100  ==========   0.0    Unknown     
* Seek Error Rate           7     30       79  ========     0.0    Unknown     
  Power On Hours Count      9      0       99  ==========   0.0    Unknown     
* Spin Retry Count          10    97      100  ==========   0.0    Unknown     
  Drive Power Cycle Count   12    20      100  ==========   0.0    Unknown     
  Drive Temperature         194    0       18  ==           0.0    Unknown     
  Hardware ECC recovered    195    0       64  ======       0.0    Unknown     
  Current Pending Sector    197    0      100  ==========   0.0    Unknown     
  Uncorrectable Sector      198    0      100  ==========   0.0    Unknown     
  UltraDMA CRC Error Rate   199    0      200  ==========   0.0    Unknown     
  Write Error Rate          200    0      100  ==========   0.0    Unknown     
  TA Counter Increased      202    0      100  ==========   0.0    Unknown     
----------------------------------------------------------------------------
NOTE: "*" means life-critical attribute
  T.E.C. not detected.

  Attribute                 ID Threshold Value Worst Raw            Type
----------------------------------------------------------------------------
* Raw Read Error Rate       1      6       64    62  00000AFD20E3h  PR ER
* Spin Up Time              3      0       96    96  000000000000h 
  Start/Stop Count          4     20      100   100  000000000152h  EC SP
* Reallocated Sector Count  5     36      100   100  000000000000h  EC SP
* Seek Error Rate           7     30       79    60  00000580A6ACh  PR ER
  Power On Hours Count      9      0       99    99  0000000005DDh  EC SP
* Spin Retry Count          10    97      100   100  000000000000h  EC
  Drive Power Cycle Count   12    20      100   100  000000000362h  EC SP
  Drive Temperature         194    0       18    40  000000000012h  SP
  Hardware ECC recovered    195    0       64    62  00000AFD20E3h  ER EC
  Current Pending Sector    197    0      100   100  000000000000h  EC
  Uncorrectable Sector      198    0      100   100  000000000000h  EC
  UltraDMA CRC Error Rate   199    0      200   200  000000000000h  PR ER EC SP
  Write Error Rate          200    0      100   253  000000000000h 
  TA Counter Increased      202    0      100   253  000000000000h  EC SP
----------------------------------------------------------------------------
NOTE: "*" means life-critical attribute
Attribute types:
      PR - Performance-related         ER - Error rate
      EC - Events count                SP - Self-preserve

  Reallocated Sectors:      0
  Current Temperature:      18 C
  Drive Power Cycle Count:  866
```
]

The above drive is in fact error free. It has recorded 0x0580A6AC seeks (= 92
million) without error.

Applying the formula ...

 normalised SER = -10 log (1 / 0x0580A6AC) 

... we get a result of 79.65

Note that we have used 1 instead of 0 for the error count (because log 0 is
indeterminate).


Raw Read Error Rate and Hardware ECC Recovered

The raw values of the RRER and HER attributes represent a sector count, not an
error count. This figure rolls over to 0 once the count reaches about 250
million. I suspect that the drive records the total number of errors in each
block of 250 million sectors, and then recalculates the normalised values of
each attribute accordingly. This means that RRER and HER would be updated
according to a rolling average rather than on a lifetime basis. I'm almost
certain that the normalised values are also logarithmic, but I'm not sure how
they are calculated. The above figure of 250 million sectors applies to the
7200.11 and DiamondMax 22 models, but may not apply to all.

While writing this article I came upon a Seagate document entitled "Diagnostic
Commands". It doesn't discuss SMART attributes, but it refers to "Error
Recovery Usage Rate" and defines it as ...

Error Recovery Usage Rate = 

-log10 {(Number of sectors in which controller invoked specified error recovery
scheme)/[(Number of sectors transferred) * (512 bytes/sector) * (8 bits/byte)]}

This lends support for my Seek Error Rate formula, and suggests that the RRER
and HER attributes may be similarly calculated.

In fact the document mentions (but does not discuss) 5 different error recovery
schemes:

 HARD = multiple retries invoked and failed
 FIRM = multiple retries invoked 
 SOFT = 5 retries invoked 
 OTF = 1 retry invoked (On The Fly)
 RAW = OTF ECC invoked 

"On The Fly" means that errored data is corrected using the ECC bytes, without
an additional access of the platters.

Based on the abovementioned Error Recovery Usage Rate formula, I now postulate
that the normalised value of the Raw Read Error Rate attribute could be
calculated as follows:

normalised RRER = -10 log (number of errored sectors / total bits transferred)

The total number of bits is ...

(250 million sectors) x (512 bytes/sector) x (8 bits/byte) = 1.024 x 10^12

It seems to me that it makes more sense to use a round figure, say 10^12.

If we now let the number of errors equal 0 (or 1), then we have ...

 max normalised RRER = -10 log (1 / 10^12) = 120

Similarly, if we let the number of errors equal 250 million (ie every sector is
errored), then we have ...

 min normalised RRER = -10 log (1 / 4096) = 36

Therefore, if my hypothesis is correct, we would expect that the threshold
value of the RRER attribute would be 36, and its maximum possible value would
be 120. In fact my Internet research tends to confirm a maximum of 120 for
7200.11 models, but the threshold figure is 34.

FWIW, here are the numbers for my own Seagate drives:

```
 Attribute                 ID Threshold Value Worst Raw
================================================================
 Raw Read Error Rate       1      6      114   100  00000386EBBA  (ST3320620A)
 Raw Read Error Rate       1      6       64    62  00000AFD20E3  (ST3120026A)
 Raw Read Error Rate       1     34       77    66  000007820F8F  (ST340016A)
 Raw Read Error Rate       1      0       79    78  00000753BA8E  (ST313021A)

 Hardware ECC recovered    195    0      100    63  00000C62F66E  (ST3320620A)
 Hardware ECC recovered    195    0       64    62  00000AFD20E3  (ST3120026A)
 Hardware ECC recovered    195    0       77    66  000007820F8F  (ST340016A)
```
http://www.users.on.net/~fzabkar/SmartUDM/320GB.RPT
http://www.users.on.net/~fzabkar/SmartUDM/120GB.RPT
http://www.users.on.net/~fzabkar/SmartUDM/40GB.RPT
http://www.users.on.net/~fzabkar/SmartUDM/13GB.RPT

References:

Here are several Usenet discussions where I have posted the results of my experiments:

Seagate - SMART Raw Read Error Rate test:
http://groups.google.com/group/comp.sys.ibm.pc.hardware.storage/browse_thread/thread/b6eb8aa2476f9ca...

SER, RRER, and HEC discussion:
http://groups.google.com/group/comp.sys.ibm.pc.hardware.storage/browse_thread/thread/54b8ad6d34549e9...

Seek Error Rate discussion:
http://groups.google.com/group/comp.sys.ibm.pc.hardware.storage/browse_thread/thread/87001db5c567fb9...

A report from a Seagate user regarding the RRER attribute:
http://forums.seagate.com/t5/Barracuda-XT-Barracuda-Barracuda/New-Maxtor-STM3500320AS-500GB-S-M-A-R-...

HD Sentinel (DOS / Windows / Linux): 
http://www.hdsentinel.com/ 

HDDScan for Windows: 
http://hddscan.com/ 

Explanation of SMART attributes: 
http://en.wikipedia.org/wiki/S.M.A.R.T.


================================================================================


SkrewDriver
Re: Seagate's Seek Error Rate, Raw Read Error Rate, and Hardware ECC Recovered
SMART attributes
03-25-2013 11:48 AM



It looks like the SMART parameters are either misunderstood, ill-defined or the
disks don't quite know how to count. I am not sure if you still monitor this
thread, but here is an exmaple from adisk out of a Maxtor BlackArmor that
forgot its passowrd and while it is not locked, it's inaccessable to any useful
operation. HDDGuru SMART Parameters:

PHYSICAL PARAMETERS:
LBA mode is supported
LBA-48 mode is supported
Sectors available with LBA commands: 268,435,455
Sectors available with LBA48 commands: 312,581,808
Full device capacity: 160,041,885,696 bytes

SECURITY:
Security features is supported
The device is currently not locked

FEATURES:
SMART is supported
HPA (Host-protected area) is not supported
AAM (Automatic acoustic management) is not supported
Streaming feature set is not supported

QUEUING:
Command Queuing is supported by the device
Maximum Queue Depth: 32

	 
 

SMART data off that same disk:

 

 
Current date and time: 3/25/2013 11:23:43
HDD Low Level Format Tool 4.12; http://hddguru.com
SMART data for [2]  ST9160824AS    3.AXD    [160.04 GB]
``` 
          Attribute                      Current   Worst          Raw       Note
----------------------------------------------------------------------------------------
 1    01  Read error rate                  100      253                 0
 3    03  Spin up time                      99       98                 0
 4    04  Number of spin-up times          100      100               214
 5    05  Reallocated sectors count        100      100                 0
 7    07  Seek error rate                   60       57        8592033936
 9    09  Power-on time                    100      100                59
 10   0A  Spin-up retries                  100      100                 0
 12   0C  Power Cycles                     100      100               244
 187  BB  Reported Uncorrectable           100      100                 0
 189  BD  High Fly Writes                  100      100                 0
 190  BE  Airflow Temperature               65       45         589496355
 192  C0  Power-off retract count          100      100               227
 193  C1  Load/unload cycle count          100      100               981
 194  C2  HDA Temperature                   35       55       90194313251  (35 degrees)
 195  C3  Hardware ECC recovered           118       60         171129616
 197  C5  Current pending sectors          100      100                 0
 198  C6  Offline scan UNC sectors         100      100                 0
 199  C7  Ultra ATA CRC Error Rate         200      200                 0
 200  C8  Write error rate at preamp       100      253                 0
 202  CA  DAM Read Errors                  100      253                 0
```
Regards,

 

SkrewDriver


================================================================================


fzabkar

Re: Seagate's Seek Error Rate, Raw Read Error Rate, and Hardware ECC Recovered
SMART attributes
03-26-2013 02:27 AM

Thanks for the feedback. I do keep an eye out for differences in SMART reports,
but it's difficult to make sense of all of them. That said, my predominant
focus has been on 3.5" drives, so I haven't analysed 2.5" drives to the same
extent.

The first thing you need to know is that the SMART attributes are not
standardised. They vary between manufacturers, and between models from the same
manufacturer, and even between firmware versions of the same model.

The names of the attributes are open to interpretation. The drive doesn't
report these names, only the attribute IDs. That's why different software uses
different names. For example, attribute 202 is referred to as Data Address Mark
Errors in some cases and TA Counter Increased in others. For Seagate drives, I
tend to trust HDDScan. Its author (Artem Rubtsov aka Doomer at HDD Guru) is
employed by Seagate in a data recovery capacity, so he is more likely to get
the names right.

In your SMART report, the Seek Error Rate numbers are consistent with my
analysis. In fact I have never seen any case which is an exception to the
logarithmic relationship in my article. The raw value of 8592033936 (=
0x000200200890) is reporting 2 seek errors in 2.1 million seeks.

As for read errors, your drive has no Current Pending Sectors, no Offline Scan
UNCorrectable Sectors, no Reported Uncorrectable Errors, and no Reallocated
Sectors.

The Hardware ECC Recovered looks both good and bad. That said, I'm not
completely sure how to interpret the numbers. The current value of 118 appears
to be 2 off the maximum of 120, if my interpretation of the Raw Read Error Rate
attribute in my article is correct. However, this would mean that the worst
value of 60 corresponds to 1 million errors in 250 million sectors.

In my article I refer to a Seagate document which mentions 5 different error
recovery schemes, including HARD, FIRM, SOFT, OTF, and RAW. It could be that
the Hardware ECC Recovered and Raw Read Error Rate SMART attributes refer to
different schemes in desktop and laptop drives. This could explain why the
attributes have appeared to switch places. In fact ISTR one case where the Raw
Read Error Rate attribute was referred to as "OTF errors".

One more observation I'd like to make is that there are several instances where
the worst value is 253. This appears counterintuitive since 253 is larger than
100. However, attribute values often begin life at 253 and ultimately settle
down once the drive has recorded sufficient activity for the data to be
statistically significant. You will notice that the Power On Time is still only
59 hours, so perhaps the Read Error Rate data are still not reliable.

But as I said in my article, my information is not completely reliable, and is
not based on official sources.

