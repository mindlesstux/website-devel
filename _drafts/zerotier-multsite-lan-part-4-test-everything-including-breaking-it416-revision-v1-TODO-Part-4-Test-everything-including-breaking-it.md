---
id: 522
title: 'TODO: Part 4: Test everything including breaking it!'
date: '2018-12-07T21:10:40-05:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2018/12/07/416-revision-v1/'
permalink: '/?p=522'
---

At this point if everything works you should be able to ping between the networks. If that isn’t working then you need to troubleshoot what is breaking down communication wise. This could be anything from the two local routers not sharing routes to the routers not talking over zerotier. The point I am trying to push across is that there is no simple gotchas I can offer troubleshooting steps for.

Once connectivity across the LANs is working, the next good thing you want to do is break it of course. First simple break I would suggest is just reboot the router vms. Ideally if everything is setup right and once they are booted back up and the services start, routing should be restored and everything should work again. Again if things do not work the next thing to do is troubleshoot and solve, as there are to many possibilities to mention. I would even suggest break the routing demons and make sure you can repair them as needed.

At the end of this now you have a working multi-site lan that each site has its own working IP subnet.

Final comment: People have asked me is it possible to bridge LANs? The answer is yes but that is an entirely different process and one I would not recommend.