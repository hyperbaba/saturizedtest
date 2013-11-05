# saturizedtest

This is a test system for saturized.
It has the following services:

mysql
postfix
ngnx
php-fpm
wordpress with some plugins and themes preinstalled

Recepies taken from WP-Chef and vagrant-chef-centos-wordpress and modified for this task.


## Usage

Three easy steps:

One: Install Vagrant 1.3.5.

```
http://downloads.vagrantup.com/tags/v1.3.5
```

Two: Clone this repository.

```
git clone https://github.com/hyperbaba/saturizedtest.git
```


Three: Vagrant up to deploy locally.

```
cd saturizedtest
vagrant up 

#This takes a few minutes

Wordpress site is already installed and configured.
Default username: admin and password: admin

The vagrant provison does not reset the wordpress database.

