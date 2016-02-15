sti-ruby-extra
==============

Ruby docker images based on [openshift/ruby-XX-centos7](https://github.com/openshift/sti-ruby), with following extra packages:

- ImageMagick
- ImageMagick-devel

Building
--------

Just do it:

    docker build -t getup:sti-php-extra:latest .

There are sample Image Stream and Template files on https://github.com/getupcloud/origin-templates.
