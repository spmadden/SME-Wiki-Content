---
title: WSL2 Timing Shenanigans
description: 
published: 1
date: 2025-07-22T22:49:50.117Z
tags: 
editor: markdown
dateCreated: 2025-07-22T22:49:50.117Z
---

## 1. Disable Time Integration

```bash
echo 2dd1ce17-079e-403c-b352-a1921ee207ee > /sys/bus/vmbus/drivers/hv_util/unbind
```

## 2. Disable implicit timesync

#### Opt 1: kernel Command line in `~/.wslconfig`
```ini
[wsl2]
kernelCommandLine=hv_utils.timesync_implicit=0
```

#### Opt 2: w/in the VM:
```bash
echo N > /sys/module/hv_utils/parameters/timesync_implicit
```

## 3. Setup chrony:

