---
title: How to add a favicon to your WordPress Blog.
author: silviu
type: post
date: 2009-06-09T18:00:51+00:00
url: /2009/06/09/how-to-add-a-favicon-to-your-wordpress-blog/
categories:
  - old
tags:
  - favicon
  - temp_on
  - wordpress

---
This was simple:

  1. I used The Gimp to create a file 16 x 16 pixels and saved it as **favicon.ico**
  2. **Upload it** to the root of your website
  3. Added the following to header.php:

```html
<link rel="shortcut icon" href="favicon.ico">
```

**Fast and easy !**