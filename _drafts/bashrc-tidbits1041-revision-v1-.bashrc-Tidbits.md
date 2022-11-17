---
id: 1065
title: '.bashrc Tidbits'
date: '2019-10-07T12:24:25-04:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/2019/10/07/1041-revision-v1/'
permalink: '/?p=1065'
---

First bit is useful if you use hastebin. This basically allows for a simple run command and pipe to hastebin. You will need to install the ‘jq’ package on the system.

```
$ cat /proc/meminfo | hastebin
https://hastebin.mindlesstux.com/botepowivo
$
```

Code/Script:

```
haste_url="https://hastebin.mindlesstux.com"
hastebin () {
  result=$(curl -sf --data-binary @${1:--} ${haste_url}/documents) || {
    echo "ERROR: failed to post document" >&2
    exit 1
  }
  key=$(jq -r .key <<< $result)
  echo "${haste_url}/${key}"
}
```