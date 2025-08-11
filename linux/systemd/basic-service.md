---
title: Basic Service
description: 
published: 1
date: 2025-08-11T16:04:04.609Z
tags: 
editor: markdown
dateCreated: 2025-08-11T16:04:04.609Z
---

# Basic one-off service unit file

```ini
[Unit]
Description=Service Title
#After=network.target

[Service]
Type=exec
#User=not-root
#Group=not-root
#WorkingDirectory=/
ExecStart=/full/path/to/bin <and> <any> <args>

[Install]
WantedBy=multi-user.target
```

