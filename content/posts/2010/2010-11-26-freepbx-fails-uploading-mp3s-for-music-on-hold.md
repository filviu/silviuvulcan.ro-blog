---
title: FreePBX fails uploading mp3’s for music on hold
author: silviu
type: post
date: 2010-11-26T14:41:03+00:00
url: /2010/11/26/freepbx-fails-uploading-mp3s-for-music-on-hold/
categories:
  - old
tags:
  - asterisk
  - freepbx
  - mpg123
  - sox
  - temp_on

---
![logo](/blog/images/2010/logo.png) This is caused by a couple of problems:

1. the `/var/lib/asterisk/moh` is missing (or has the wrong permissions). Be sure it's there and has the right owner (asterix:asterix) and permissions

2. Sox has to be installed. What the error logs miss to inform at the first glance is that you also need `mpg123` otherwise you'll get this:

```bash
Error Processing: "sox failed to convert file and original could not be copied as a fall back" for Johnny Cash - Solitary Man.mp3!
```

##### This is not a fatal error, your Music on Hold may still work.

Have fun.
