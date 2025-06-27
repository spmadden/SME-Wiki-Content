---
title: Yubikey Quickstart
description: 
published: 1
date: 2025-06-27T19:28:14.197Z
tags: 
editor: markdown
dateCreated: 2025-03-15T12:10:15.308Z
---

# Yubikey Quickstart

## Windows
### Setup
1. Install gnupg or gpg4win
    ```powershell
    winget install --id gnupg.gnupg
    ```
   a. Disable the windows builtin ssh agent
   ```powershell
   Get-Service ssh-agent | Set-Service -StartupType Disabled
   Stop-Service ssh-agent
   Get-Service ssh-agent
   ```
   b. [OPT] Enable window's sshd
   ```powershell
   Start-Service sshd
   Set-Service -Name sshd -StartupType 'Automatic'
   ```
   c. [OPT] Configure window's sshd to secure it (admin, obvs)
   ```powershell
   (Get-Content $ENV:PROGRAMDATA\ssh\sshd_config) | ForEach-Object {
     $_.replace("#PasswordAuthentication yes", "PasswordAuthentication no") `
     -replace("#GSSAPIAuthentication no", "GSSAPIAuthentication yes")
     } | Set-Content $ENV:PROGRAMDATA\ssh\sshd_config
   Restart-Service sshd
   ```

2. Edit/create `%APPDATA%\.gnupg\gpg-agent.conf`
```conf
enable-ssh-support
enable-putty-support
enable-win32-openssh-support
default-cache-ttl 600
max-cache-ttl 7200
# The ~/ is critical at the front to get replaced with $HOME, the rest of the paths must be \
extra-socket ~/.gnupg\S.gpg-agent.extra
```

3. Install piv-tool, cli, minidriver
```powershell
winget install --id yubico.piv-tool
winget install --id yubico.yubikeymanagercli
winget install --id yubico.yubikeysmartcardminidriver
```

4. [OPT]: Hook cygwin/msys2 in your `~/.bashrc`
```bash
eval $(/usr/bin/ssh-pageant -r -a "/tmp/.ssh-pageant-$USERNAME")
```

5. [OPT]: Force-setup git
```ini
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
```powershell
gpg-connect-agent.exe killagent /bye
gpg-connect-agent.exe /bye
```

7. Verify it worked
```powershell
gpg -K
ssh-add -L
```

## Push keys to remote windows box
```powershell
# Get the public key file generated previously on your client
$authorizedKeys = (ssh-add -L) -join "||"

# Generate the PowerShell to be run remote that will copy the public key file generated previously on your client to the authorized_keys file on your server
$remotePowershell = "powershell New-Item -Force -ItemType Directory -Path $env:USERPROFILE\.ssh; Add-Content -Force -Path $env:USERPROFILE\.ssh\authorized_keys -Value '$authorizedKeys'"

# Connect to your server and run the PowerShell using the $remotePowerShell variable
ssh username@domain1@contoso.com $remotePowershell
```

## Dump all secure ssh public keys in `authorized_keys` format
```powershell
$keyid = ""
$cardno = ""
(gpg --with-colons -K) | ForEach-Object {
  $parts = $_ -split ":"
  if (($parts[0] -contains "uid") -and $keyid) {
    (gpg --export-ssh-key $keyid) + " cardno:" + $cardno + " 0x" + $keyid + " " + $parts[9]
    $keyid = ""
  }elseif (($parts[0] -contains "sec") -and ($parts[14] -like "D276000124010000000*")) {
  	$keyid = $parts[4]
    $cardno = $parts[14].substring(20,8)
  }
}
```

## Forward GPG agent to remote linux box
```powershell
 ssh -R'/home/sean/.gnupg/S.gpg-agent':'~/.gnupg/S.gpg-agent.extra' sean@10.169.0.27
```

## Some better defaults for `gpg.conf`
```
no-greeting
cert-digest-algo SHA512
compress-level 9
require-cross-certification
keyid-format 0xlong
with-fingerprint
with-keygrip
list-options show-policy-url show-user-notations show-sig-expire
list-options show-uid-validity
```