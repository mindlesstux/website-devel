---
id: 211
title: 'Install Dell OpenManage on Ubuntu 16.04 (and up?)'
date: '2018-01-09T05:34:56-05:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2018/01/09/209-autosave-v1/'
permalink: '/?p=211'
---

So with this new server I am setting up I wanted to install the Dell OpenManage software but got a headache from doing so. Just about everything I was finding was pointing me to CentOS based info and I am using an Ubuntu based system. Hence my headache. After hours of googling I finally found the page I did and it helped me get Dell OpenManage installed. Of course I had to mangle their instructions some but it was not to bad. Below is what I used and a link to the page that was helpful.

```
<pre class="line-numbers">```bash
sudo echo 'deb http://linux.dell.com/repo/community/ubuntu trusty openmanage' | sudo tee -a /etc/apt/sources.list.d/linux.dell.com.sources.list
gpg --keyserver hkp://pool.sks-keyservers.net:80 --recv-key 1285491434D8786F ; gpg -a --export 1285491434D8786F | sudo apt-key add -
sudo apt-get update
sudo apt install srvadmin-base srvadmin-storageservices srvadmin-idrac7
# sudo apt install srvadmin-webserver
# sudo service dsm_om_connsvc start && sudo update-rc.d dsm_om_connsvc defaults
```
```

```
sudo echo 'deb http://linux.dell.com/repo/community/ubuntu trusty openmanage' | sudo tee -a /etc/apt/sources.list.d/linux.dell.com.sources.list
gpg --keyserver hkp://pool.sks-keyservers.net:80 --recv-key 1285491434D8786F ; gpg -a --export 1285491434D8786F | sudo apt-key add -
sudo apt-get update
sudo apt install srvadmin-base srvadmin-storageservices srvadmin-idrac7
# sudo apt install srvadmin-webserver
# sudo service dsm_om_connsvc start && sudo update-rc.d dsm_om_connsvc defaults
```

Also I wanted this to set the hostname of the system in the iDrac 7 that the system has. If it is being stuborn the following will fix it.

```
ssh root@<ip>
/admin1-> racadm set System.ServerOS.Hostname <newhostname>
/admin1-> exit
```