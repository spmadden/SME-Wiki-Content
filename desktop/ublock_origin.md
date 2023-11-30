---
title: uBlock Origin Settings
description: 
published: 1
date: 2023-11-30T19:45:29.535Z
tags: 
editor: markdown
dateCreated: 2023-11-30T19:44:10.321Z
---

# uBlock Origin Settings

## Stop Autoplay Videos
filter:
```
*##video:remove-attr(autoplay)
```

## Medium Mode
switch to more aggressive blocking (medium mode), "rules"
```
no-large-media: behind-the-scene false
* * 3p-frame block
* * 3p-script block
behind-the-scene * * noop
behind-the-scene * 1p-script noop
behind-the-scene * 3p noop
behind-the-scene * image noop
behind-the-scene * inline-script noop
```