---
layout: default
title: Namecore binaries
---

[bitcoin](.)

# {{ page.title }}

Here are my namecore binaries:

* Debian 7 (amd64) <https://github.com/ondrejsika/namecore-bin-debian-7>
* Debian 8 (amd64) <https://github.com/ondrejsika/namecore-bin-debian-8>

Builded with __incompatible bdb__.

### Build process

    apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev libdb++-dev libdb4.8-dev libdb4.8++-dev

    git clone https://github.com/namecoin/namecore.git

    cd namecore

    ./autogen.sh
    ./configure --with-incompatible-bdb

    # compile/build with 4 cores
    make -j4

    ln -s `pwd`/src/namecoin-cli /usr/local/bin/
    ln -s `pwd`/src/namecoin-tx /usr/local/bin/
    ln -s `pwd`/src/namecoind /usr/local/bin/

