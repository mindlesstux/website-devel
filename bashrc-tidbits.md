---
id: 1041
title: '.bashrc Tidbits'
date: '2019-09-13T15:31:52-04:00'
author: Tux
layout: page
guid: 'https://mindlesstux.com/?page_id=1041'
php_everywhere_code:
    - 'Just put [php_everywhere] where you want the code to be executed.'
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