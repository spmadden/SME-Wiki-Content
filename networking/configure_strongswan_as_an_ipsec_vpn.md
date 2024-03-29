## Configuring StrongS/WAN for an IPSec VPN using EAP/MS-CHAPv2

Assumptions:

Server is a Fedora 17 Linode off in the cloud.

Disclaimer: Most of this has been pulled from

-   <http://wiki.strongswan.org/projects/strongswan/wiki/Win7EapMultipleConfig>
-   <http://wiki.strongswan.org/projects/strongswan/wiki/Win7CertReq>
-   <http://wiki.strongswan.org/projects/strongswan/wiki/Win7Certs>

### Download & Compile StrongS/WAN

-   Download from <http://download.strongswan.org/strongswan.tar.bz2>

```{=html}
<!-- -->
```
    wget http://download.strongswan.org/strongswan.tar.bz2

-   Extract and compile - I used the following configure script

```{=html}
<!-- -->
```
    tar -xvf strongswan.tar.bz2
    sudo yum install gmp-devel openssl-devel
    ./configure --enable-eap-identity --enable-eap-mschapv2 --enable-md4 --enable-md5 --enable-openssl --enable-pkcs11 --enable-blowfish --enable-agent --enable-eap-md5 --enable-eap-peap --enable-eap-tls 
    make -j4
    sudo make install

-   make install will install the config files by default in /usr/local/etc
-   Make sure you update your path to include /usr/local/sbin

### Configure StrongS/WAN

#### /usr/local/etc/ipsec.conf

    config setup

    conn %default
          keyexchange=ikev2
          ike=aes256-sha1-modp1024!
          esp=aes256-sha1!
          dpdaction=clear
          dpddelay=300s
          rekey=no

    conn roadwarrior
          left=173.255.229.6
          leftsubnet=0.0.0.0/0
          leftauth=pubkey
          leftfirewall=yes
          leftcert=/etc/openvpn/keys/secure.seanmadden.net.crt
          leftsendcert=always
          right=%any
          rightauth=eap-mschapv2
          rightsendcert=never
          rightsourceip=172.16.0.0/24
          auto=start

Things to change:

-   rightsourceip -> This is the internal pool of VPN IPs that it will pull from
-   leftcert -> This is the certificate of the vpn server. Requirements:
    -   <http://tiebing.blogspot.com/2012/05/windows-7-ikev2-error-13806.html>
    -   ENSURE THAT THE CERTIFICATE AUTHORITY IS INSTALLED AS A "MACHINE CERTIFICATE" FROM <http://wiki.strongswan.org/projects/strongswan/wiki/Win7Certs>
-   left -> This is the public IP address of the vpn gateway.

#### /usr/local/etc/ipsec.secrets

    # /etc/ipsec.secrets - strongSwan IPsec secrets file
    : RSA /etc/openvpn/keys/secure.seanmadden.net.key

    sean : EAP "password!"

Things to change:

-   'sean' -> username for the user
-   'password' -> password for the user in cleartext
-   RSA -> The key file for the certificate specified in ipsec.conf

### IPTABLES!

    iptables -t nat -A POSTROUTING -j SNAT --to-source 173.255.229.6

Things to change:

-   --to-source "x.x.x.x" -> IP address of 'left' in ipsec.conf

### WINDOWS!

<http://wiki.strongswan.org/projects/strongswan/wiki/Win7EapConfig>

## Roadwarrior Linux Clients

    conn secure
          left=%any
          leftcert=orcus.crt
          leftsourceip=%config
          leftid=orcus
          leftfirewall=yes
          right=173.255.229.6
          rightsubnet=0.0.0.0/0
          rightcert=secure.seanmadden.net.crt
          auto=start

## Server Linux Clients

    conn secure
          left=%any
          leftcert=orcus.crt
          leftdns=%config
          leftsourceip=%config
          leftid=orcus
          leftfirewall=yes
          right=173.255.229.6
          rightsubnet=172.16.0.0/16
          rightcert=secure.seanmadden.net.crt
          auto=start
