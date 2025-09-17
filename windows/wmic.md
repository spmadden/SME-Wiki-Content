---
title: WMIC
description: 
published: 1
date: 2025-09-17T17:02:05.588Z
tags: 
editor: markdown
dateCreated: 2025-09-17T17:02:05.588Z
---

# Windows snippets

### List Apps
```pwsh
wmic product get name
```

```powershell
## List 32bit installed programs
$regPath = 'HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*'
Get-ItemProperty -Path $regPath |
Select-Object DisplayName, DisplayVersion, Publisher, InstallDate
## List 64bit installed programs
$regPath = 'HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*'
Get-ItemProperty -Path $regPath |
Select-Object DisplayName, DisplayVersion, Publisher, InstallDate
```