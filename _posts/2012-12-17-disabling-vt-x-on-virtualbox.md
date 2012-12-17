---
layout: post
title: "Disabling VT x on VirtualBox"
description: ""
category: 
tags: []
---
{% include JB/setup %}

I do not have VT-x extensions available on my Hackintosh. A default
install of Virtualbox on Mac OS X assumes VT-x availability. THis is
because all of the Mac hardware lineup supports it. In order to disable
VT-x extensions to allow a Virtualbox VM to boot on a hackintosh do:

    VBoxManage modifyvm "VM Name" --hwvirtex off
