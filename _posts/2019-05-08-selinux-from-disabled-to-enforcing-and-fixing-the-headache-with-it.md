---
id: 741
title: 'SELinux &#8211; From Disabled to Enforcing and fixing the headache with it'
date: '2019-05-08T17:24:47-04:00'
author: Tux
layout: post
guid: 'https://mindlesstux.com/?p=741'
permalink: /2019/05/08/selinux-from-disabled-to-enforcing-and-fixing-the-headache-with-it/
Reference_URL:
    - 'https://www.redhat.com/archives/fedora-selinux-list/2008-September/msg00096.html'
php_everywhere_code:
    - 'Just put [php_everywhere] where you want the code to be executed.'
switch_like_status:
    - '0'
sharing_disabled:
    - '1'
categories:
    - 'Centos 7'
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