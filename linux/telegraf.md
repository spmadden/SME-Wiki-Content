---
title: Telegraf Snippets
description: 
published: 1
date: 2025-09-01T21:20:18.613Z
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