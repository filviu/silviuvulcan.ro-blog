---
title: Whitelist a host when using denyhosts
author: silviu
type: post
date: 2010-03-26T16:55:02+00:00
url: /2010/03/26/whitelist-a-host-when-using-denyhosts/
dsq_thread_id:
  - 326525521
categories:
  - old
tags:
  - temp_on

---
[<img decoding="async" loading="lazy" class="aligncenter size-full wp-image-758" title="denyhosts" src="http://blog.silviuvulcan.ro/wp-content/uploads/sites/2/2010/03/denyhosts.jpg" alt="" width="347" height="73" />][1]I&#8217;m using this excellent tool on my hosting server called <a href="http://denyhosts.sourceforge.net/" target="_blank" rel="noopener">denyhosts</a>. It basically scans trough auth.log for repeated failed attempts to login in order to block brute force attackers. It can also get a list of offending ip-s from other usesrs of DenyHosts who configured their instalation to share attacker ip&#8217;s. All nice and well until you mistype your password one to many times. Or 127.0.0.1 gets added to the list like it happened today for me. So, you need to add a few ip&#8217;s to a whitelist.

It&#8217;s easy. Create a file called **allowed-hosts** in **/var/lib/denyhosts** or whatever you set your work dir for. Inside this file you can list ip&#8217;s that should be whitelisted.

 [1]: http://blog.silviuvulcan.ro/wp-content/uploads/sites/2/2010/03/denyhosts.jpg