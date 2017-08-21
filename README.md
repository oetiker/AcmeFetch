AcmeFetch
=========

[![Build Status](https://travis-ci.org/oetiker/AcmeFetch.svg?branch=master)](https://travis-ci.org/oetiker/AcmeFetch)

Version: #VERSION#

Date: #DATE#

AcmeFetch is a thin wrapper arount he ACME::Protocol library to fetch and maintain
ssl certificates using the the services of Let's Encrypt!

Setup
-----

To build AcmeFetch you require the perl, openssl and gcc packages on your
system.

On RedHat you get them with:

    yum install perl-core openssl-devel gcc unzip

On Ubuntu / Debian with:

    apt-get install perl libssl-dev gcc unzip make

Get a copy of AcmeFetch from https://github.com/oetiker/AcmeFetch/releases
and unpack it into your scratch directory and cd there.

    ./configure --prefix=$HOME/opt/acmefetch
    make

Configure will check if all requirements are met and give
hints on how to fix the situation if something is missing.

Any missing perl modules will be built and installed into the prefix
directory. Your system perl will NOT be affected by this.

To install the application, just run

    make install

Configuration
-------------

Take a look at the etc/acmefetch.cfg.dist file for inspiration.

Documentation
-------------

First make sure you understand how letsencrypt certificates work
by reading https://letsencrypt.org/howitworks/technology/

Then read the acmefetch documentation in the doc directory and finally take
some inspiration from the sample configuration file provided.

Enjoy!

Tobias Oetiker <tobi@oetiker.ch>
