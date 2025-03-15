---
title: Yubikey Quickstart
description: 
published: 1
date: 2025-03-15T12:10:15.308Z
tags: 
editor: markdown
dateCreated: 2025-03-15T12:10:15.308Z
---

# Yubikey Quickstart

## Windows
1. Install gnupg or gpg4win
```
winget install --id gnupg.gnupg
```

2. Edit/create `%APPDATA%\.gnupg\gpg-agent.conf`
```
enable-ssh-support
enable-putty-support
enable-win32-openssh-support
use-standard-socket
default-cache-ttl 600
max-cache-ttl 7200
```

3. Install piv-tool, cli, minidriver
```
winget install --id yubico.piv-tool
winget install --id yubico.yubikeymanagercli
winget install --id yubico.yubikeysmartcardminidriver
```

4. [OPT]: Hook cygwin/msys2 in your `~/.bashrc`
```
eval $(/usr/bin/ssh-pageant -r -a "/tmp/.ssh-pageant-$USERNAME")
```

5. [OPT]: Force-setup git
```
[core]
    sshCommand = 'C:\\Windows\\System32\\OpenSSH\\ssh.exe'
[user]
    signingKey = '<INSERT>'
[commit]
	  gpgSign = true
[tag]
    gpgSign = true
[gpg]
    program = 'C:\\Program Files (x86)\\GnuPG\\gpg.exe'
```

6. Reset the agent
```
gpg-connect-agent.exe killagent /bye
gpg-connect-agent.exe /bye
```

7. Verify it worked
```
gpg -K
ssh-add -L
```