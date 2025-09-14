---
title: LDAP Filter Examples
description: 
published: 1
date: 2025-09-14T17:29:54.091Z
tags: 
editor: markdown
dateCreated: 2025-09-14T17:29:54.091Z
---

# LDAP Filter Examples

### All Groups
```ldap
(&(|(objectclass=group)))
```

### All Users
```ldap
(&(|(objectclass=person)))
```

### User member in specified group (`$GROUP_DN`)
```ldap
(&(objectclass=person)(memberOf=$GROUP_DN))
```

### User with specified login name
```ldap
(&(|(objectclass=person))(samaccountname=%uid))
```

