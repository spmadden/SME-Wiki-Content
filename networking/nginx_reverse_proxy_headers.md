---
title: NGINX Reverse Proxy Headers
description: 
published: 1
date: 2023-10-03T19:53:22.923Z
tags: 
editor: markdown
dateCreated: 2023-10-03T19:53:22.923Z
---

## Server Definition Section

```nginx
map $remote_addr $proxy_forwarded_elem {
    # IPv4 addresses can be sent as-is
    ~^[0-9.]+$          "for=$remote_addr";

    # IPv6 addresses need to be bracketed and quoted
    ~^[0-9A-Fa-f:.]+$   "for=\"[$remote_addr]\"";

    # Unix domain socket names cannot be represented in RFC 7239 syntax
    default             "for=unknown";
}

map $http_forwarded $proxy_add_forwarded {
    # If the incoming Forwarded header is syntactically valid, append to it
    "~^(,[ \\t]*)*([!#$%&'*+.^_`|~0-9A-Za-z-]+=([!#$%&'*+.^_`|~0-9A-Za-z-]+|\"([\\t \\x21\\x23-\\x5B\\x5D-\\x7E\\x80-\\xFF]|\\\\[\\t \\x21-\\x7E\\x80-\\xFF])*\"))?(;([!#$%&'*+.^_`|~0-9A-Za-z-]+=([!#$%&'*+.^_`|~0-9A-Za-z-]+|\"([\\t \\x21\\x23-\\x5B\\x5D-\\x7E\\x80-\\xFF]|\\\\[\\t \\x21-\\x7E\\x80-\\xFF])*\"))?)*([ \\t]*,([ \\t]*([!#$%&'*+.^_`|~0-9A-Za-z-]+=([!#$%&'*+.^_`|~0-9A-Za-z-]+|\"([\\t \\x21\\x23-\\x5B\\x5D-\\x7E\\x80-\\xFF]|\\\\[\\t \\x21-\\x7E\\x80-\\xFF])*\"))?(;([!#$%&'*+.^_`|~0-9A-Za-z-]+=([!#$%&'*+.^_`|~0-9A-Za-z-]+|\"([\\t \\x21\\x23-\\x5B\\x5D-\\x7E\\x80-\\xFF]|\\\\[\\t \\x21-\\x7E\\x80-\\xFF])*\"))?)*)?)*$" "$http_forwarded, $proxy_forwarded_elem";

    # Otherwise, replace it
    default "$proxy_forwarded_elem";
}
```

## In each reverse proxy (location/server/etc):
```nginx
proxy_set_header Host $host:$server_port;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Forwarded-Host $host;
proxy_set_header X-Forwarded-Port $server_port;
proxy_set_header Forwarded $proxy_add_forwarded;
proxy_buffering off;
proxy_http_version 1.1;
```

### Optional: Add Websocket Support:
```nginx
proxy_set_header Connection "upgrade";
proxy_set_header Upgrade $http_upgrade;
proxy_cache_bypass $http_upgrade;
```

## Example: 
```nginx
server {
    server_name {EXTERNAL FQDN};

    location / {
        proxy_pass {FULL_INTERNAL_URL};
        include conf.d/z.commonproxy; # Common entries above
        include conf.d/z.websocket; # Optional Websocket addon above.
    }

    # SSL Termination options
    listen 443 ssl http2; # managed by Certbot
    ssl_certificate /.../fullchain.pem; # managed by Certbot
    ssl_certificate_key /.../privkey.pem; # managed by Certbot
    include /../options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /../ssl-dhparams.pem; # managed by Certbot
}

# Redirect HTTP to HTTPS
server {
    if ($host = {EXTERNAL_FQDN}) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    listen 80;
    server_name {EXTERNAL_FQDN};
    return 404; # managed by Certbot
}

```

Full set of NGINX Docs: https://nginx.org/en/docs/http/ngx_http_proxy_module.html
