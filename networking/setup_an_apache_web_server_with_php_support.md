## Setup an Apache server with PHP support

Prerequisites:

For a bare system:

    sudo apt-get install gcc g++ make

Download [Apache](http://httpd.apache.org/download.cgi), [PHP](http://www.php.net/downloads.php)

For Apache:

    sudo apt-get install  zlib1g-dev libssl-dev libldap2-dev ldap-utils libmysqlclient15-dev 

For PHP:

    sudo apt-get install libxml2-dev libbz2-dev libgmp3-dev libxslt-dev 

Extract Apache and execute the following:

    ./configure --enable-mods-shared=all --enable-authnz-ldap --enable-rewrite --enable-proxy --enable-ssl --with-ldap
    make -j2
    sudo make install

Make sure the apache bin path (defaults to /usr/local/apache2/bin) is on the path.

Extract PHP and execute the following:

    './configure' '--build=x86_64-redhat-linux-gnu' '--host=x86_64-redhat-linux-gnu' '--target=x86_64-redhat-linux-gnu' '--program-prefix=' '--prefix=/usr' '--exec-prefix=/usr' '--bindir=/usr/bin' '--sbindir=/usr/sbin' '--sysconfdir=/etc' '--datadir=/usr/share' '--includedir=/usr/include' '--libdir=/usr/lib64' '--libexecdir=/usr/libexec' '--localstatedir=/var' '--sharedstatedir=/var/lib' '--mandir=/usr/share/man' '--infodir=/usr/share/info' '--cache-file=../config.cache' '--with-libdir=lib64' '--with-config-file-path=/etc' '--with-config-file-scan-dir=/etc/php.d' '--disable-debug' '--with-pic' '--disable-rpath' '--with-bz2' '--with-exec' '--with-freetype' '--with-png' '--with-xpm' '--enable-gd-native-ttf' '--with-t1lib' '--without-gdbm' '--with-gettext' '--with-gmp' '--with-iconv' '--with-jpeg' '--with-openssl' '--with-pcre-regex' '--with-zlib' '--with-layout=GNU' '--enable-exif' '--enable-ftp' '--enable-magic-quotes' '--enable-sockets' '--enable-sysvsem' '--enable-sysvshm' '--enable-sysvmsg' '--with-kerberos' '--enable-ucd-snmp-hack' '--enable-shmop' '--enable-calendar' '--without-mime-magic' '--with-libxml-dir=/usr' '--enable-xml' '--with-system-tzdata' '--without-unixODBC' '--without-pspell' '--disable-wddx' '--disable-posix' '--disable-sysvmsg' '--disable-sysvshm' '--disable-sysvsem' '--with-apxs2' '--with-config-file-path=/etc' '--with-mysql' '--with-mysqli' '--with-ldap' '--with-xsl' --with-pdo-mysql
    make -j2
    sudo make install
