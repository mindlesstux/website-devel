---
id: 201
title: 'Disable Systemd DNS resolver'
date: '2018-01-06T02:21:14-05:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2018/01/06/199-autosave-v1/'
permalink: '/?p=201'
---

I ran into an issue recently where I tracked back that the systemd resolver was trying to be a tad to helpful and causing me pain through DNS. So I set out to kill and keep it disabled across reboots. In some quick googling I found a good answer on askubuntu.com.

Regurgitating what the answer is for my reference later and for anyone to find. (Along with a reference link below)

1. Disable systemd-resolvd service: ```
    sudo systemctl disable systemd-resolved.service
    sudo service systemd-resolved stop
    ```
2. If file exists, add to “\[main\]” section in /etc/NetworkManager/NetworkManager.conf ```
    dns=default
    ```
3. Delete symlink and replace /etc/resolv.conf
4. 
5. 

Restart network-manager

```
sudo service network-manager restart
```