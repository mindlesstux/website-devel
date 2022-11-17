---
id: 743
title: 'SELinux &#8211; From Disabled to Enforcing and fixing the headache with it'
date: '2019-05-08T17:25:57-04:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2019/05/08/741-revision-v1/'
permalink: '/?p=743'
---

I ran into an issue re-enabling SELinux on my little fleet of CentOS 7 boxes in my home lab. Basically when I installed them I had disabled SELinux at install and thus enabling SELinux was causing all the systems to freeze up after a reboot.

A little googling/digging around mailing lists. I [stumbled upon a post](https://www.redhat.com/archives/fedora-selinux-list/2008-September/msg00096.html) that gave a perfect answer to fix the problem I was having.

```
# setenforce 0
# yum remove selinux-policy\*
# rm -rf /etc/selinux/targeted /etc/selinux/config
# yum install selinux-policy-targeted
# yum install selinux-policy-devel policycoreutils-gui  *** Only if these were removed byt the yum remove.
# touch /.autorelabel; reboot
```

Basically temporary disable SELinux, remove selinux-policy\*, remove the old targeted dir and config file, and re-install selinux. Followed by the usualy autorelabel and reboot.

The only thing I would add would be to check your network and ifup the interface after setenforce 0.