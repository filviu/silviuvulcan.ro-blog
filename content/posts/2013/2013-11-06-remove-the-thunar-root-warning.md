---
title: Remove the Thunar root warning
author: silviu
type: post
date: 2013-11-06T08:36:58+00:00
draft: true
url: /2013/11/06/remove-the-thunar-root-warning/
categories:
  - old
tags:
  - root
  - slackware
  - temp_on
  - Thunar

---

![thunar warnign](/blog/images/2013/thunar-warning.png)  

I never understood a developer's obsession with "their way" but anyways. Thunar is a good light file manager that has one issue, it insists on displaying a warning when being used as root that cannot be turned off. Well I run my personal laptop as root and I don't really care what others think about it and why it might be a bad thing(TM).

In order to remove the damn warning you need to grab everything needed to rebuild the package from:

<http://mirrors.slackware.com/slackware/slackware-current/source/xfce/Thunar/> (32 bit) or <http://mirrors.slackware.com/slackware/slackware64-current/source/xfce/Thunar/> (64 bit)

After that download [this patch][2] to the same folder and replace the slackbuild with [this one][3].

**OR** simply clone [the git repo][4] and build there.

 [1]: http://blog.silviuvulcan.ro/wp-content/uploads/sites/2/2013/11/thunar-warning.png
 [2]: https://github.com/filviu/slackbuilds/raw/master/Thunar/no-root-warning.patch
 [3]: https://github.com/filviu/slackbuilds/raw/master/Thunar/Thunar.SlackBuild
 [4]: https://github.com/filviu/slackbuilds/