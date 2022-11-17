---
id: 358
date: '2018-06-21T09:57:49-04:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2018/06/21/357-revision-v1/'
permalink: '/?p=358'
---

re-enable SSv3 support on java

Go to Java installation folder.  
Open {JRE\_HOME}\\lib\\security\\java.security -file in text editor.  
Delete or comment out the following line “jdk.tls.disabledAlgorithms=SSLv3”.