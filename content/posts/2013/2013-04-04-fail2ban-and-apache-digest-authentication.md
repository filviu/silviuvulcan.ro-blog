---
title: fail2ban and apache digest authentication
author: silviu
type: post
date: 2013-04-04T10:11:45+00:00
url: /2013/04/04/fail2ban-and-apache-digest-authentication/
dsq_thread_id:
  - 1186042468
categories:
  - old
tags:
  - apache
  - authentication
  - digest
  - temp_on

---
Although I don&#8217;t consider fail2ban something to rely on for security is just another piece of the puzzle when securing a server. When configuring fail2ban for a debian server I noticed that the defaults rules are missing failures if DIGEST is used for authentication instead of basic.

I added the following to **/etc/fail2ban/filter.d/apache-auth.conf**:

[cce lang=&#8221;INI&#8221;]  
\[[]client <HOST>[]\] (Digest: )?user .* (authentication failure|not found|password mismatch)  
[/cce]

Restart fail2ban and try entering a wrong user/password while checking the fail2ban log. It should catch the try. (Be sure you don&#8217;t lock yourself out 🙂 )