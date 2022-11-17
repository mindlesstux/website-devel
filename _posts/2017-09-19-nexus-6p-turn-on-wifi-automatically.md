---
id: 154
title: 'Nexus 6P: Turn on WiFi Automatically'
date: '2017-09-19T13:52:41-04:00'
author: Tux
layout: post
guid: 'https://mindlesstux.com/?p=154'
permalink: /2017/09/19/nexus-6p-turn-on-wifi-automatically/
Reference_URL:
    - 'https://www.xda-developers.com/turn-on-wifi-automatically-nexus5x-nexus6p/'
switch_like_status:
    - '0'
sharing_disabled:
    - '1'
categories:
    - '8.0'
    - Android
    - 'Nexus 6P'
    - 'Not Rooted'
    - Phone
    - 'Tips / Tricks'
---

I use a Nexus 6P as my day to day driver despite my phone having the early shutdown bug with the battery. (Currently working on getting an RMA, come on google I am at 4wks now waiting for outbound shipment.) I stumbled upon something that I just wanted to bookmark for use just in case I ever needed to find this again. Instead of a regular bookmark I figured it would be better if I made a public posting and linked the original artical.

```
adb shell
settings put global wifi_wakeup_available 1
settings put global wifi_wakeup_enabled 1
```