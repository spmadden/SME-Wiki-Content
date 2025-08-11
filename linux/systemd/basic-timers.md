---
title: Systemd Timers with Cancel Timeout
description: 
published: 1
date: 2025-08-11T16:31:19.597Z
tags: 
editor: markdown
dateCreated: 2025-08-11T16:31:19.597Z
---

# Service File
`/etc/systemd/system/mirror.service` or
`~/.config/systemd/user/mirror.service`
```ini
[Unit]
Description=Basic Mirroring Service

[Service]
# Block in the 'starting' condition until the exec exits
Type=oneshot
# Kill if the script takes longer than 12h to run
TimeoutStartSec=12h
ExecStart=/backuptank/mirror/update.sh
WorkingDirectory=/backuptank/mirror/
StandardOutput=file:/var/log/mirror.log
StandardError=inherit
```

# Timer File
`/etc/systemd/system/mirror.timer` or
`~/.config/systemd/user/mirror.timer`
```ini
[Unit]
Description=Timer for Mirror Service

[Timer]
# start 2hr after boot
OnBootSec=2h
# only if the service has been quiet for the last 24hr
OnUnitInactiveSec=24h
# filename of above service
Unit=mirror.service

[Install]
WantedBy=multi-user.target
```

## Cron equivalents
* Every minute: `OnCalendar=*-*-* *:*:00`
* Every 5 minutes: `OnCalendar=*-*-* *:*/5:00`
* Every 10 minutes: `OnCalendar=*-*-* *:*/10:00`
* Every hour: `OnCalendar=*-*-* *:00:00`
* Every day at midnight: `OnCalendar=*-*-* 00:00:00`