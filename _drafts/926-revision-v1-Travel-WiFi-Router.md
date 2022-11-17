---
id: 3142
title: 'Travel WiFi Router'
date: '2020-02-22T17:32:17-05:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2020/02/22/926-revision-v1/'
permalink: '/?p=3142'
---

Recently there were a few posts on Reddit asking about travel routers, particularly one that got me going was the following:

- [https://www.reddit.com/r/mikrotik/comments/f0fmqc/map\_lite\_travel\_router/](https://www.reddit.com/r/mikrotik/comments/f0fmqc/map_lite_travel_router/)

Following that I found an interesting blog posting about building a travel router and setting up a VPN to encrypt all traffic:

- <https://danrl.com/blog/2016/travel-wifi/>

After reading that I found that I really should describe how I use a [MikroTik RB962](https://www.amazon.com/MikroTik-RouterBoard-Triple-802-11ac-RB962UiGS-5HacT2HnT-US/dp/B01BMMK4HI/) (also known as [hAP ac](https://mikrotik.com/product/RB962UiGS-5HacT2HnT)) for my travel router purposes. I chose this to be my travel router for many reasons beyond the scope of this but the basics that make it attractive in general:

- 1x 2.4ghz radio
- 1x 5.0ghz radio
- 5x Ethernet ports 
    - 1x One PoE in
    - 1x One PoE out
- 1 SFP port
- 1 USB port

Now, why do those things mean something? Well lemme start off with it makes it an incredibly adaptable platform to work with for something of this nature.

- If I want ports on the WAN side I can.
- If I want to use my phone as an LTE modem for it, I can via USB-A-&gt;USB-C cable.
- The biggest reason is I can establish an EoIP tunnel or I can bring along a RaspberryPi and create a router on a stick and use either a [wireguard](https://www.wireguard.com/) or [zerotier](https://www.zerotier.com/) tunnel back to my server in the [datacenter](https://dacentec.com/). I can then fire up a routing daemon and get access to “WAN/MAN” network for all my devices while I travel.
- Even better I can use ethernet, wifi, or USB for WAN connectivity and my devices in the “LAN” won’t care.

To use this in a very basic travel router format (no VPN setup) here are rough instructions to do so.

1. Boot the device and run “Quick Set” in winbox 
    1. Choose “Home AP Dual”
    2. Set the wireless to be your preferred settings, mine are: 
        1. Network Name: SSID-Travel
        2. Frequency: 1st channel for the frequency range
        3. Band: 2GHz-only-N &amp;&amp; 5GHz-N/AC
        4. Wifi Password: “Did you really think I would give this?”
        5. Skip the “Guest Wireless Network”, your traveling, you are the guest!
    3. Internet: Eth1
    4. Address Acquisition: Automatic, aka DHCP
    5. Local Network 
        1. IP Address: 172.16.30.254
        2. Netmask: 255.255.255.0/24
        3. Bridge All LAN Ports, yes
        4. DHCP Server Range, 172.16.30.1-172.16.30.50
        5. NAT, yes
    6. Apply it and reboot the device and make sure the configuration works
2. Create a bridge named something like “bridgeWAN” 
    1. Attach ether1 to it
3. Create a second bridge named something like “bridgeLAN” 
    1. Attach all the remaining ports/interfaces to it
4. Move the LAN IP to the “bridgeLAN”
5. Move the DHCP client to the “bridgeWAN”
6. Adjust any firewall &amp; nat rules that are assigned to interfaces to be updated to respective bridges.

At this point you should now have a device that is capable of using ether1 for WAN connectivity. This does not solve the problem of those hotels that do not offer ethernet though! To do that you will want to figure out which frequency you get the clearest/strongest signal on. Once you have that, move the wlan interface for that frequency to the bridgeWAN.