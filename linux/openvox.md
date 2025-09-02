---
title: Openvox Notes
description: 
published: 1
date: 2025-09-02T00:26:30.173Z
tags: 
editor: markdown
dateCreated: 2025-08-26T03:53:58.368Z
---

# Doc Links
* https://help.puppet.com/core/current/Content/PuppetCore/puppet_language.htm
* https://help.puppet.com/core/current/Content/PuppetCore/the_trifecta.htm
* https://help.puppet.com/core/current/Content/PuppetCore/lang_relationships.htm
* https://help.puppet.com/core/current/Content/PuppetCore/lang_node_definitions.htm

# Quick Setup

## Raspbian

### Install
`debian12` from https://apt.voxpupuli.org/
```bash
curl -LO https://apt.voxpupuli.org/openvox8-release-debian12.deb
dpkg -i openvox8-release-debian12.deb
apt update
apt install openvox-agent
```
## Redhat Variants
https://yum.voxpupuli.org/
### Install
```
curl -LO https://yum.voxpupuli.org/openvox8-release-fedora-36.noarch.rpm
dnf install openvox8-release-fedora-36.noarch.rpm
dnf install openvox-agent
```
## Path & Configure
### Client Connect:
`~/.bashrc`:
```bash
export PATH=/opt/puppetlabs/bin:$PATH
```

Configure server URL and initial register
```bash
#!/bin/bash
puppet config set server <puppetserver.example.com> --section main

puppet ssl bootstrap
```

On server, acknowledge registration
```bash
#!/bin/bash
puppetserver ca list
puppetserver ca sign --certname <name>
```

Back on client, if not polling to pull cert:
```bash
#!/bin/bash
puppet ssl bootstrap
```

## Configure node on server:
`vim /etc/puppetlabs/code/environments/production/manifests/site.pp`:
```puppet
node '<hostname>' {

}
```