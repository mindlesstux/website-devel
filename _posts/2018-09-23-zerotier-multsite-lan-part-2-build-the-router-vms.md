---
id: 410
title: 'Part 2: Build the router VM(s)'
date: '2018-09-23T22:02:19-04:00'
author: Tux
layout: post
guid: 'https://mindlesstux.com/?p=410'
permalink: /2018/09/23/zerotier-multsite-lan-part-2-build-the-router-vms/
php_everywhere_code:
    - 'Just put [php_everywhere] where you want the code to be executed.'
switch_like_status:
    - '0'
sharing_disabled:
    - '1'
categories:
    - ZeroTier
series:
    - 'ZeroTier + Multisite LAN'
---

To bring us into part 2, the next thing is to create the routing VMs.

I simply did a simple CentOS 7 minimal install with one network interface configured. At the router, I created network 10.10.9.0/29 on the same LAN segment. During setup of the VM, I configured the VM to be 10.10.9.2/29 with a gateway of 10.10.9.1/29. I also did the same with IPv6, fd00:10:10:9::2/64 and fd00:10:10:9::1/64 respectively. Now when I get to other sites to deploy, the network will change to be 10.10.9.8/29 &amp; 10.10.9.16/29. The reason I chose to go with a /29 here is simply due to I plan to layer in a “services” into these subnets. This particular set of VMs I plan to layer on a [Pi-Hole](https://pi-hole.net/) and Chrony NTP server.

If you have trouble installing CentOS 7 at a minimal install, then this series is not for you.

Once you have the VM created, the first thing to do is install ZeroTier. Thankfully they make this dead simple.

```
If you want to verify things:
curl -s 'https://pgp.mit.edu/pks/lookup?op=get&search=0x1657198823E52A61' | gpg --import && if z=$(curl -s 'https://install.zerotier.com/' | gpg); then echo "$z" | sudo bash; fi

If you like to live risky:
curl -s https://install.zerotier.com/ | sudo bash
```

Run either as root and it is installed.

Other small things I have found that are needed after install,  
In /etc/sysconfig/network-scripts/ifcfg-eth0, add the following: NM\_CONTROLLED=”no”  
In /etc/sysconfig/network, add the following: NETWORKING=yes  
In /etc/selinux/config, change SELINUX to be permissive, SELINUX=permissive  
Reboot a couple of times, make sure that default gateway and DNS servers show up in their respective places.

At this point, the next thing to do is create the ZeroTier network. Simply log in and go the networks page and create a new network. Once that is done, the next thing is to join the network.

```
zerotier-cli join abcd1234abcd1234
```

Finally, go authorize the new clients and label them in the “My Networks”.