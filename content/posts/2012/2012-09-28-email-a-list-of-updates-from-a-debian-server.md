---
title: Email a list of updates from a Debian server.
author: silviu
type: post
date: 2012-09-28T12:49:40+00:00
url: /2012/09/28/email-a-list-of-updates-from-a-debian-server/
categories:
  - old
tags:
  - debian
  - email
  - temp_on
  - updates

---
![Debian logo](/blog/images/2012/Debian1.png)

Do you run remote servers? Me too.

It's a good ideea to keep them up to date. On the other hand I don't like automatic updates, something might break when you least want or expect it. So I prefer to be notified of updates and choose myself the moment when to apply them. Following is a nice script that sends an email of available updates on a Debian system.

```bash
#!/bin/bash

EMAIL=youremail@example.com

# Only download updates.
# Nothing is installed.
apt-get -dqq update
apt-get -dyqq upgrade

upgrades=$(apt-get -s upgrade | grep ^Inst)
if [ "$upgrades" ] ; then
echo "$upgrades" | mail -s "Updates for $(hostname) on $(date +%Y-%m-%d)" $EMAIL
fi
```

Set the above script to run from cron as often as you'd like to get these notifications.
