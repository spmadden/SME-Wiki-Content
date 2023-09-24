---
title: Samba / Active Directory ID Matching Configuration
description: 
published: 1
date: 2023-09-24T20:44:02.661Z
tags: 
editor: markdown
dateCreated: 2023-09-24T20:44:02.661Z
---

```
[global]
        server string = {your server name - like 'saturn'}
        netbios name = {your server name - like 'saturn'}
        map to guest = Bad User
        security = ads
        #domain logons = yes

        workgroup = {your workgroup - like 'WORKGROUP'}
        kerberos method = secrets and keytab
        dedicated keytab file = /etc/krb5.keytab
        realm = {your dns realm - like 'CONTOSO.COM'
        password server = {your AD Controller - like 'AD.CONTOSO.COM'}
        idmap config * : backend = tdb
        idmap config * : range = 3000-9999
        idmap config {WORKGROUP} : backend = sss
        idmap config {WORKGROUP} : range = 200000-2147483647
        winbind use default domain = yes
        winbind enum users = yes
        winbind enum groups = yes
        template shell = /bin/bash
        template homedir  = /home/%U

        printing = cups
        printcap name = cups
        load printers = yes
        cups options = raw

        access based share enum = yes
        hide unreadable = yes
#       client min protocol = SMB3

        create mask = 0660
        directory mask = 0770
        writable = yes
        log level = 3

        veto files = /._*/.DS_Store/
        delete veto files = yes

```