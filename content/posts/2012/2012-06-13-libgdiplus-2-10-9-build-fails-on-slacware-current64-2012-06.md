---
title: libgdiplus-2.10.9 build fails on slacware current64 (2012-06)
author: silviu
type: post
date: 2012-06-13T06:01:08+00:00
url: /2012/06/13/libgdiplus-2-10-9-build-fails-on-slacware-current64-2012-06/
categories:
  - old
tags:
  - configure
  - libgdiplus
  - make
  - mono
  - slaclware
  - temp_on

---
Installing [mono](http://www.mono-project.com/Main_Page) I needed to install libgdiplus. It failed with the following error:

```bash
/usr/lib64/gcc/x86_64-slackware-linux/4.7.0/../../../../x86_64-slackware-linux/bin/ld: testgdi.o: undefined reference to symbol 'g_free'
/usr/lib64/gcc/x86_64-slackware-linux/4.7.0/../../../../x86_64-slackware-linux/bin/ld: note: 'g_free' is defined in DSO /usr/lib64/libglib-2.0.so.0 so try adding it to the linker command line
/usr/lib64/libglib-2.0.so.0: could not read symbols: Invalid operation
collect2: error: ld returned 1 exit status
make[2]: *** [testgdi] Error 1
make[2]: Leaving directory `/usr/local/src/libgdiplus-2.10.9/tests'
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory `/usr/local/src/libgdiplus-2.10.9'
make: *** [all] Error 2
```

The fix is simple, thanks to a mention in [slacky](https://www.slacky.eu/asche64/pkgreports/) pkg reports:

After running `./configure` edit `tests/Makefile` and at line 130 replace `LIBS = -lpthread -lfontconfig` with `LIBS = -lpthread -lfontconfig -lglib-2.0 -lX11`

Until a patch is made this means we'll have to install it manually.

http://www.mono-project.com/Main_Page