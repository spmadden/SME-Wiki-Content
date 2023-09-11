## Setup an SVN Server using Apache

Prerequisites:

Download [subversion](http://subversion.tigris.org/downloads/subversion-1.6.11.tar.gz)

Run the following:

    sudo apt-get install libsqlite3-dev sqlite3 libneon27-dev libdb4.7-dev libexpat-dev
    ./configure --enable-all-static --with-apxs --with-ssl --with-neon --with-berkeley-db=db.h:/usr/include/:/usr/lib:db-4.7
    make
    sudo make install
