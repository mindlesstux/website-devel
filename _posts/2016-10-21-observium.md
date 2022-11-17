---
id: 31
title: Observium
date: '2016-10-21T02:39:47-04:00'
author: Tux
layout: post
guid: 'https://mindlesstux.com/?p=31'
permalink: /2016/10/21/observium/
switch_like_status:
    - '0'
sharing_disabled:
    - '1'
categories:
    - Observium
---

![](https://observium.mindlesstux.com/images/login-hamster-large.png)

What I do for my job is maintain a monitoring system for all the data centers for work and ensure it is getting good data. One thing I have found is many people tend to emulate work and personal lives together. So a bit over a month and a half ago for home use I went on a venture to figure out how can I monitor my home devices and network like I do for work to help identify problems before they begin. Now what I use for work is [EM7 (by ScienceLogic)](https://www.sciencelogic.com/) would be perfect to use. Only problem is it costs money to have a license for it. I did not want to spend money or hassle the work contacts (to much, I have already prodded them about the idea) to get a license for it. This left me looking to setup something free. So whats free out there? [Nagios](https://www.nagios.org/), [Cacti](http://www.cacti.net), [OpenNMS](https://www.opennms.org/), [LibreNMS](http://www.librenms.org/), [The Dude](http://www.mikrotik.com/thedude), [and more](http://alternativeto.net/software/opennms/). Those mentioned I have heard of or have tried to use, and that is not a complete list but those were the ones that stood out to me.

The problem then became which one to choose? Good question. I did not even know what I wanted to get out of the system which should have been my first question.

I used Nagios before, and it was a pain to keep and add to the config for Nagios. Not saying it should not be used and would have worked for me. I just did not want to deal with the hassle of configuring it again if I could help it. I called this my first choice fall back option.

Like Nagios, Cacti was a bit more of a hassle to install the last time I worked with it than I wanted this time around. Though it produces some nice looking graphs. It lacks notification of something going awry that I wanted. Though I thought if I can’t find something better, Nagios + Cacti would work.

The one last one I used in my past The Dude. It is made by my currently favorite (at time of writing) router hardware and software company, MikroTik. This had an advantage of running on my home router, switch, or spare hardware on my network. Though to make any changes to it requires me to have a windows client installed to make the change. Notifications could be email or via that client so that was fine. It also hits the most points of what I would like to monitor and also makes nice little graphs. I passed on it as I wanted something that would be easy to work with on my phone no matter where I was.

To cut this story short, I then tried OpenNMS and tried to work with LibreNMS, but neither seemed to work for me in some way or another. That is when I found [Observium](http://www.observium.org/). First thing I found is a simple demo install of it, seemed to flow nicely from area to area, monitors the type devices I have installed local and remote. I looked it over and seems that the professional and community versions are not that far apart in feature sets. Including a couple of integrations that while would take a little work to do I felt were worth the effort. The pricing to jump to the professional version does not seem to be that bad either, and I just might after more time make that jump just for the bandwidth billing which I would use in reverse to just simply have a better log of my network usage across devices and keep providers in check with my own monitoring.

So I went about creating a virtual machine at [Vultr](https://www.vultr.com/?ref=6914536-3B) which is turning out to be my new favorite little VM hosting provider over [Linode](https://www.linode.com/) and Digital Ocean. Made myself one of the smallest vms, one cpu, 758mb ram, etc. Installed Ubuntu 16.04 on it. Then proceeded to run the setup instructions that are very well detailed for Observium. I then fairly quickly and almost effortlessly discovered all my home devices and network equipment that was SNMP capable. I also added all my remote servers and the like as well.

<div class="wp-caption aligncenter" style="width: 760px">![Looks like Dacentec (not where I work) needs to work on keeping the datacenter a stable temperature. (Those are not load spikes, as this box is currently at rest till I get time to load it up.)](https://observium.mindlesstux.com/graph.php?type=device_temperature&device=40&to=1494340579&from=1491662179&height=300&width=1152)Looks like [Dacentec](http://dacentec.com/) (not where I work) needs to work on keeping the data center a stable temperature. Those are not load spikes causing a rise in CPU temperature, as this box is currently at rest/no load till I get time to load it up with some game servers.

</div><div class="wp-caption aligncenter" style="width: 760px">![](https://observium.mindlesstux.com/graph.php?type=device_processor&device=40&to=1494340579&from=1491662179&height=300&width=1152)CPU usage for same time period as the CPU temps graph.

</div>Doing a little reading I quickly added [RANCID](http://www.shrubbery.net/rancid/) and [SmokePing](http://oss.oetiker.ch/smokeping/) to the same VM and got that integrated into my instance of Observium as well. Which I sorely needed as I have a habit of making configuration changes on my network devices at home and not document the changes. So when I want to go back to a previous state I cant as I don’t have a easily copy/paste method to do so, or miss something entirely. RANCID solved that. As for the SmokePing integration I wanted that so I can monitor my home Internet connection ping times. Basically right now I have AT&amp;T’s GigaPower service for use but in a little over a month I am going to be moving into a new home and loosing said service. Instead I will be getting TWC (soon to be called Charter) and will be wanting a way to say their connection blows chunks when it does with 100% certainty. A goal I have would also be to monitor the cable modem signal levels if that is exposed to me and graph it over time. Granted from what I can tell thats is going to be an epic script/scrapper/hack to get that into Observium.

So far after a month and a half, I am very much impressed with Observium CE 0.16.1.7533 + RANCID v3 + SmokePing setup that I created for $5 USD / month. It makes that bit of time and money very much worth it. Sure there are features I did not get but all the basics here are covered, alert notifications, detailed graphs, easy gui to use, etc.

I look forward to my first upgrade as the [upgrade process](http://www.observium.org/docs/updating/#community-edition) looks very simple as well.