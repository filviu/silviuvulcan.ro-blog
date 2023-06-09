---
title: Add php APC and UploadProgress support to CentOS
author: silviu
type: post
date: 2011-08-03T08:25:40+00:00
url: /2011/08/03/add-php-apc-and-uploadprogress-support-to-centos/
categories:
  - old
tags:
  - apc
  - centos
  - php
  - temp_on
  - uploadprogress

---
I was playing today with some file uploading scripts and noticed that they require one of the two in order to be able to display a progress bar.

Those are the steps required to enabled both of them on centos:

```bash
yum install php-pear php-devel httpd-devel pcre-devel
pecl install apc
pecl install uploadprogress
```

Than I created in /etc/php.d/ the following files:

```ini
; provides upload progress, installed using pecl
extension=apc.so
apc.rfc1867=1
```

and

```ini
; provides upload progress, installed using pecl
extension=uploadprogress.so
```

All you need to do now is restart apache!

_Please note that I was using PHP 5.2 from testing at the time_
