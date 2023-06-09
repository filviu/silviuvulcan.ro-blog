---
title: Checking directory sizes from the BASH prompt
author: silviu
type: post
date: 2010-01-18T20:18:16+00:00
url: /2010/01/18/checking-directory-sizes-from-bash-prompt/
categories:
  - old
tags:
  - bash
  - directory
  - folder
  - pipe
  - sort
  - temp_on

---
![bash_script](/blog/images/2010/bash_script.jpg) The command `ls` can be made to show directories and permission but it will not display directory sizes. Then it's time for other commands. For example on my hosting account there is no file manager installed and evidently x and kde is missing too so, to find out directory sizes I can use the **du** command. It will show something like this:

```bash
du -h -max-depth=1
3.2M    ./wp-admin
24M     ./wp-content
5.9M    ./wp-includes
4.0K    ./cgi-bin
44M     .
```

BTW the command above shows a typical WordPress installation. What I used was the switch -h which provides human readable sizes for folders (like Kilo, Giga, Tera, etc.) and I also used the swithc -max-depth to tell du only to go one folder deep otherwise it will also show the sizes of every subfolder from the current one down.

Should you like to have those results sorted it's only a matter of piping the results of `du` into `sort`, like this:

```bash
du -h -max-depth=1 | sort -nr
44M     .
24M     ./wp-content
5.9M    ./wp-includes
4.0K    ./cgi-bin
3.2M    ./wp-admin
```

What `sort` does is - surprise, sort it's input. The switches used are **-n** to tell sort to sort by numerical values and **-r** to reverse the results (from big to small). Of course from here on you can pipe to text files, use even more complicated constructs but this should take care of the base.

If you managed to sort your folders how about sorting my wish list 🙂 don't forget to click a sponsor.