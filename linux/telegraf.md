---
title: Telegraf Snippets
description: 
published: 1
date: 2025-09-01T21:21:30.086Z
tags: 
editor: markdown
dateCreated: 2025-09-01T21:20:18.613Z
---

# Telegraf Snippets

## MTR to hosts
```
[[inputs.exec]]
  interval = '60s'
  commands=["mtr -C -n 129.6.15.26", "mtr -C -n 2610:20:6f15:15::26"]
  timeout = "40s"
  data_format = "csv"
  csv_skip_rows = 1
  csv_column_names=[ "", "", "status","dest","hop","ip","loss","snt","", "","avg","best","worst","stdev"]
  name_override = "mtr"
  csv_tag_columns = ["dest", "hop", "ip"]
```

## NTP Pool CSV
```
[[inputs.http]]
        urls = ["https://www.ntppool.org/scores/2001:470:8b54::6/log?limit=200&monitor=*"]
        interval = "30m"
        data_format = "csv"
        csv_header_row_count = 1
        name_override = "ntppool"
        csv_tag_columns = ["monitor_id", "monitor_name"]
        tags = {host = "2001:470:8b54::6"}
        csv_timestamp_column = "ts_epoch"
        csv_timestamp_format = "unix"
        csv_skip_values = [""]
        csv_column_types = ["int", "string", "float", "float", "float", "int", "string", "float"]
```