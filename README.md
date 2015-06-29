bosun
=====

The bosun container can be used to spin up an instance of
[Bosun](http://bosun.org/).

Quick Start
-----------

To quickly spin up an instance of Bosun, simply specify a port forwarding
rule and run the container:

    $ docker run \
        -p 4242:4242 \
        jleight/bosun

Usage
-----

Bosun relies on OpenTSDB to store its data. Bosun assumes that OpenTSDB will be
provided via a linked container named "db". If you want to use a different
OpenTSDB instance, you will need to modify the `bosun.conf` file located in the
exposed `/var/opt/bosun` volume in this container.

A Bosun data container can be created by using the following command:

    $ docker create \
        --name bosun-data \
        jleight/bosun

An OpenTSDB container can be started by using the following command:

    $ docker run \
        --name bosun-opentsdb \
        jleight/opentsdb

A Bosun container can then be started by running:

    $ docker run \
        --name bosun \
        --volumes-from bosun-data \
        --link bosun-opentsdb:db \
        -p 8070:8070 \
        jleight/opentsdb
