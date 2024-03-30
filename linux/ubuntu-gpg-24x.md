---
title: Ubuntu Install GPG 2.4.x from Debian Experimental Src
description: 
published: 1
date: 2024-03-30T13:07:16.679Z
tags: 
editor: markdown
dateCreated: 2024-03-30T13:07:16.679Z
---

# Ubuntu Install GPG 2.4.x from Debian Experimental Sources


1. Add experimental to sources
```
sudo bash -c "echo 'deb-src http://httpredir.debian.org/debian/ experimental main contrib non-free' > experimental.list"
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0x0E98404D386FA1D9 0x6ED0E7B82643E131
```

2. Update repo sources.
```
sudo apt-get update
```

3. Install the build deps
```
sudo apt-get build-dep gnupg2
```

4. Compile the experimental gnupg2 debian packages
```
sudo apt-get source --compile gnupg2
```

5. Install the packages
```
sudo apt-get install ./*.deb
```