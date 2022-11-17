---
id: 239
title: 'Shitty Idea: Change webserver storage up'
date: '2018-01-28T13:10:49-05:00'
author: Tux
layout: post
guid: 'https://mindlesstux.com/?p=239'
permalink: /2018/01/28/shitty-idea-change-webserver-storage-up/
switch_like_status:
    - '0'
sharing_disabled:
    - '1'
categories:
    - 'Shitty Ideas'
---

Most likely will never public but here is a shitty idea I just had for hosting my website.

- Two systems, A &amp; B 
    - A side (self hosted side) 
        - 2x 10gb? partition on standard storage
        - 10gb? /dev/ram0
        - Use mdadm to raid 1 1 standard storage and the /dev/ram0 
            - Setup DRBD on top of that RAID1 
                - Setup PV/VG/LV on top of the DRBD
        - Setup DRBD (#2) on second standard storage async from B side
    - B side (Vultr + block storage) 
        - 10gb? partition on standard storage
        - 2x 10gb? partition on block storage
        - Use mdadm to raid 1 those two together 
            - Setup DRBD on top of that RAID1, Async from Side A
        - Setup DRBD (#2) on second block storage 
            - Setup PV/VG/LV on that
- Configure webservices on both sides to use mount points off of the LVMs 
    - 3 nginx services 
        - Possibly symlink out of webroots?
    - 1 MariaDB, 
        - Boot from only active side (A mostly)
- Write scripts to break DRBD on B side to allow for 
    - LV snapshots of file system -&gt; tarballs 
        - 1 per week, up to a month
    - Daily? backups of mysql via mysqldump 
        - Keep 14 days worth?
    - All tarballs go to second DRBD

On top of all that, Vultr will snapshot the VM (not block store) every week.