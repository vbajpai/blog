---
layout: post
title: "Fun with Raspberry PI"
description: ""
category: 
tags: []
---
{% include JB/setup %}

### Expand the SD Partition
<hr/>

check the current partition status:

    # df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/root       1.7G  706M  883M  45% /
    devtmpfs         51M     0   51M   0% /dev
    tmpfs           105M     0  105M   0% /dev/shm
    tmpfs           105M  244K  105M   1% /run
    tmpfs           105M     0  105M   0% /sys/fs/cgroup
    tmpfs           105M     0  105M   0% /tmp
    /dev/mmcblk0p1   90M   24M   67M  27% /boot

`ssh` into the raspbery pi and run `fdisk`:

    # fdisk /dev/mmcblk0

delete the second partition, and then create a new partition and use the
default sizes prompted. At the end, save, exit and reboot. Resize the
newly created partition after reboot:

    # shutdown -r now
    # resize2fs /dev/mmcblk0p2

check the new partition status:

    # df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/root       7.3G  707M  6.3G  10% /
    devtmpfs         51M     0   51M   0% /dev
    tmpfs           105M     0  105M   0% /dev/shm
    tmpfs           105M  244K  105M   1% /run
    tmpfs           105M     0  105M   0% /sys/fs/cgroup
    tmpfs           105M     0  105M   0% /tmp
    /dev/mmcblk0p1   90M   24M   67M  27% /boot

The new partition expands to the length of the available space on the
card.

#### Update Packages
<hr/>

Let's change the `root` password, before even bringing it online

    # passwd

Let's synchronize the repository feed and upgrade the packages

    # pacman -Syu

It's good to have the bleeding edge packages.

#### Create a new user
<hr/>

install `zsh` shell:

    # pacman -S zsh

create a new user:

    # useradd -m -g users -s /bin/zsh vbajpai

set the password for the new user:
    
    # passwd

install `sudo`

    # pacman -S sudo

allow users of group `wheel` to run as root with `sudo`

    # visudo
    %wheel    ALL=(ALL) ALL

add your user to group `wheel`

    # gpasswd -a vbajpai wheel
    # groups vbajpai
    wheel users

logout now, we will use our new user to login back.

#### Secure ssh access
<hr/>

push your public ssh key in `$HOME/.ssh/authorized_keys`

    [remote] $ ssh-copy-id <pi>

this will take precedence over password-based logins over `ssh`.

#### Synchronize Time
<hr/>

check your timezone status:

    $ timedatectl status

see available timezones:

    $ timedatectl list-timezones

change to a different timezone:

    $ sudo timedatectl set-timezone Europe/Berlin

raspberrypi does not have a hardware RTC. The stock archlinux-arm
provides `openntp`, which is not currently maintained for linux. let's
install `ntp` instead to synchronize the time over the network:

    $ sudo pacman -S ntp

enable the service on reboot:

    $ sudo systemctl start ntpd
    $ sudo systemctl enable ntpd

it takes around 4-5 minutes for the time to get updated.

#### Change the `hostname`
<hr/>

change the `hostname` to pi

    $ hostnamectl set-hostname pi

list the available locales:

    $ locale -a

see the current locale:

    $ locale
    
The available locales can be changes in `/etc/locale.gen`. 

#### Install development tools
<hr/>

install some essentials:

    $ sudo pacman -S git
    $ sudo pacman -S vim
    $ sudo pacman -S tree
    $ sudo pacman -S tmux
    $ sudo pacman -S curl
    $ sudo pacman -S gcc

This is my personal list. Your mileage may vary.

#### Setup Python Environment
<hr/>

install python2:

    $ sudo pacman -S python2

install distribute:

    $ sudo pacman -S python2-distribute
    $ sudo pacman -S python2-pip

archlinux has defaulted to `python3` by default, edit your `zshrc` to
use `python2` by default

    $ alias python=python2
    $ alias pip=pip2
    $ ln -s /usr/bin/python2 /usr/bin/python

install `virtualenv` and `virtualenvwrapper`

    $ sudo pip2 install virtualenv
    $ sudo pip install virtualenvwrapper

#### Setup Ruby Environment
<hr/>

install `rvm`

    $ curl -L get.rvm.io | bash -s stable

logout and log back in

check if `rvm` is installed correctly:
    
    $ type rvm | head -n1
    rvm is a shell function

install any dependencies:

    $ rvm requirements
    $ sudo pacman -S libxml2 libxslt
    $ sudo pacman -S autoconf automake make libtool bison

list known rubies:

    $ rvm list known

install `ruby` 2.0.0

    $ rvm install 2.0.0
    $ rvm use 2.0.0


