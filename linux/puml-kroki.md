---
title: Plantuml & Kroki containers
description: 
published: 1
date: 2025-11-21T21:26:07.578Z
tags: 
editor: markdown
dateCreated: 2025-11-21T21:26:07.578Z
---


Justfile: 
```just
default: pull remove stop rename create start

pull:
        podman pull docker.io/yuzutech/kroki:latest
        podman pull docker.io/plantuml/plantuml-server:latest

remove:
        -podman rm kroki-old
        -podman rm puml-old

rename:
        podman rename kroki kroki-old
        podman rename puml puml-old

create:
        podman create --name kroki \
                -p 8000:8000 \
                -e TZ="America/New York" \
                -e KROKI_MAX_URI_LENGTH=16384 \
                -e KROKI_COMMAND_TIMEOUT=30s \
                -e KROKI_CONVERT_TIMEOUT=30s \
                docker.io/yuzutech/kroki:latest
        podman generate systemd -n -t 10 kroki > /home/ec2-user/.config/systemd/user/kroki.service
        podman create --name puml \
                -p 8001:8080 \
                plantuml/plantuml-server:latest
        podman generate systemd -n -t 10 puml > /home/ec2-user/.config/systemd/user/puml.service
        systemctl --user daemon-reload
        systemctl --user enable kroki
        systemctl --user enable puml
start:
        systemctl --user start kroki
        systemctl --user start puml

stop:
        -systemctl --user stop kroki
        -podman stop kroki
        -systemctl --user stop puml
        -podman stop puml

restart: stop start

```