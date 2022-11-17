---
id: 105792
title: 'Routing to a docker network'
date: '2022-02-23T20:47:40-05:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/?p=105792'
permalink: '/?p=105792'
---

\# zeusjr  
\# Create “bridgeDOCKER” with no NIC to it  
\# Disable v4/v6 addressing  
\# Ensure it goes to an up state

\# routervm  
\# Add a new interface to “bridgeDOCKER”  
\# Give it a static v4 address of what will be the gateway for the docker network, I used 10.50.0.1/24  
\# Update FRR to put the address on the interface and add the network to appropriate routing protocols for redistribution.

\# andromeda  
\# Add a new interface to “bridgeDOCKER”  
\# Give it a static v4 address of something not cared about, eg 10.69.69.69/32  
\# docker network create -d macvlan –subnet 10.50.0.0/24 –ip-range 10.50.0.0/24 –gateway 10.50.0.1 -o parent=ens9 public\_network  
\# — ens9 is the interface aligned with “bridgeDOCKER”

\# https://hub.docker.com/r/nicolaka/netshoot