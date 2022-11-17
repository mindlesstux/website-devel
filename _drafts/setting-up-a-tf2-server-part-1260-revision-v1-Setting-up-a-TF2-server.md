---
id: 268
title: 'Setting up a TF2 server'
date: '2018-02-08T19:58:00-05:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2018/02/08/260-revision-v1/'
permalink: '/?p=268'
---

Prepare the system as TF2 servers run as 32-bit

```
<pre class="line-numbers">```bash
cd /home/tf2-server
echo tf2_ds.txt <<EOF
login anonymous
force_install_dir /home/tf2-server/srcds
app_update 232250
quit
EOF
./steamcmd.sh +runscript tf2_ds.txt
```
```

```
<pre class="line-numbers">```bash
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt-get install mailutils util-linux tmux lib32gcc1 libstdc++6 libstdc++6:i386 libcurl4-gnutls-dev:i386
```
```

Always a good idea to run things as a user and not root, so lets add a user and login as it.

```
<pre class="line-numbers">```bash
sudo adduser tf2-server
sudo login -f tf2-server
```
```

Now that we are in the user account lets download the server. First we need to download steamcmd.

```
<pre class="line-numbers">```bash
mkdir steamcmd
cd steamcmd
wget http://media.steampowered.com/installer/steamcmd_linux.tar.gz
tar zxf steamcmd_linux.tar.gz
```
```

Create a steamcmd file and run it.

```
<pre class="line-numbers">```bash
cd /home/tf2-server
echo tf2_ds.txt <<EOF
login anonymous
force_install_dir /home/tf2-server/srcds
app_update 232250
quit
EOF
./steamcmd.sh +runscript tf2_ds.txt
```
```

asdf