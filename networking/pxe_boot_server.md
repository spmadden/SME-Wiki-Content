## PXE Boot Server

### Prerequisites

Starting from scratch:

-   Install the latest version of Fedora
    -    For this step, I used a LiveCD onto a VirtualBox machine
-   PXE Boot requires the following packages be installed
    -   tftp-server
    -   xinetd
    -   dhcp
    -   syslinux
-   This is as easy as 'sudo yum install dhcp tftp-server xinetd syslinux'

### DHCP

This is my configuration for dhcp. Change values in here as required. /etc/dhcp/dhcpd.conf :

      ignore client-updates;
      subnet 10.0.0.0 netmask 255.255.255.0 {
           range 10.0.0.5 10.0.0.20; # total 15 addresses allocated
           default-lease-time 86400; #1 day lease time for extended boots
           max-lease-time 86400; # only 1 day lease - no more - no less
           option ip-forwarding off;
           option broadcast-address 10.0.0.255;
           option subnet-mask 255.255.255.0;
           filename "/pxelinux.0";
           option tftp-server-name "10.0.0.1";
      }

Point of note: You must have a 10.0.0.0/24 address assigned to a NIC for the DHCP server to broadcast on.

### TFTP

/etc/xinetd.d/tftp :

    Notably: change 'disable = yes' to 'disable = no'

The following is the tftpd configuration file. Change '/sto/tftpboot' to the directory where you'll be hosting your files. If you're making this directory from scratch, please note this dir must have 0x777 permissions for the tftp daemon to access and host it.

    service tftp {
          disable = no
          socket_type             = dgram
          protocol                = udp
          wait                    = yes
          user                    = root
          server                  = /usr/sbin/in.tftpd
          server_args             = -s /sto/tftpboot -v -v -p
          per_source              = 11
          cps                     = 100 2
          flags                   = IPv4
    }

If you're using the IPTables firewall, you will need to add the following lines to allow DHCP and TFTP traffic directed at the server.

### IPTABLES

/etc/sysconfig/iptables :

    -A INPUT -m state -m tcp --state NEW --dports 67,68 -j ACCEPT
    -A INPUT -m state -m udp --state NEW --dports 67,68 -j ACCEPT
    -A INPUT -m state -m tcp --state NEW --dport 69 -j ACCEPT

### Filesystem

This is how I structured my filesystem. You may move the root tftpboot directory wherever you like, but the substructure must remain the same.

Filesystem structure:

    /tftpboot
    |-- menu.c32
    |-- pxelinux.0
    |-- pxelinux.cfg/
    |   -- default

You will need to copy both pxelinux.0 and menu.c32 from /usr/share/syslinux into this directory for PXE to boot into the menu successfully.

Within /tftpboot/pxelinux.cfg/default , the bare minimum must contain the following lines:

    DEFAULT menu
    PROMPT 0
    MENU TITLE PXEBoot Server.  Use at own risk.
    TIMEOUT 200
    TOTALTIMEOUT 6000
    ONTIMEOUT local
    LABEL local
          MENU LABEL (local)
          MENU DEFAULT
          LOCALBOOT 0
    MENU end

I have found it easier to simply disable SELinux on my PXE server boxes if only to remove needless hassle.

### Additional Tutorials

Follow the following links for instructions on how to add individual boot options.

-   [Memtest over PXEBoot](/networking/pxeboot/Memtest over PXEBoot)
-   [DBan over PXEBoot](/networking/pxeboot/DBan over PXEBoot)
-   [GParted over PXEBoot](/networking/pxeboot/GParted over PXEBoot)
-   [Clonezilla over PXEBoot](/networking/pxeboot/Clonezilla over PXEBoot)
-   [PartedMagic over PXEBoot](/networking/pxeboot/PartedMagic over PXEBoot)
-   [Knoppix over PXEBoot](/networking/pxeboot/Knoppix over PXEBoot)
-   [Fedora 11 Kickstarted Install over PXEBoot](/networking/pxeboot/Fedora 11 Kickstarted Install over PXEBoot)
-   [Fedora 11 LiveOS over PXEBoot](/networking/pxeboot/Fedora 11 LiveOS over PXEBoot)
