---
layout: post
title: "Installing Vagrant on a Headless Debian Server"
description: ""
category: 
tags: []
---
{% include JB/setup %}

This post was also contributed by: [github.com/jamesdavidson
&rarr;](https://github.com/jamesdavidson).

I have decided to perform most of the computation intensive tasks on our
university server rack. I have a VM provisioned on this rack. Since the
VM is running an old version of Debian build, I want to keep this build
minimal and work on projects on a separate VM running a bleeding edge
Ubuntu Server provisioned by Vagrant. I started looking into ways to run
Vagrant on a headless Debian build, and it looks quite straightforward.


Install Virtualbox
    
    $ sudo apt-get install linux-headers-$(uname -r)
    $ sudo apt-get install virtualbox-ose-dkms
    $ sudo apt-get install virtualbox-ose
    $ sudo service virtualbox start

Setup a Ruby Environment

    $ sudo apt-get install ruby ruby-dev rubygems

Install Vagrant as a Ruby gem

    $ sudo gem install vagrant

