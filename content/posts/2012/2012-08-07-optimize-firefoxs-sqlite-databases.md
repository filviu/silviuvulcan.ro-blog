---
title: Optimize Firefox’s sqlite databases
author: silviu
type: post
date: 2012-08-07T11:51:25+00:00
url: /2012/08/07/optimize-firefoxs-sqlite-databases/
categories:
  - old
tags:
  - database
  - firefox
  - mozilla
  - oneliner
  - optimize
  - sqlite
  - temp_on

---

Here's a handy one-liner to tune a bit your Firefox:

```bash
for file in ~/.mozilla/firefox/*/*.sqlite; do sqlite3 $file 'VACUUM;';done
```

What this does ie optimize every sqlite database in your account's profiles. You can even add this line to a script to start on boot or by cron. Worth noting that Firefox should probably not run while you do this.