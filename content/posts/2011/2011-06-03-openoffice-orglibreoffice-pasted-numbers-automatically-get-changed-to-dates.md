---
title: OpenOffice.org / Libreoffice pasted numbers automatically get changed to dates
author: silviu
type: post
date: 2011-06-03T12:12:01+00:00
url: /2011/06/03/openoffice-orglibreoffice-pasted-numbers-automatically-get-changed-to-dates/
categories:
  - old
tags:
  - automatic
  - calc
  - date
  - libreoffice
  - openoffice
  - temp_on

---
![Open Office Calc](/blog/images/2011/openoffice_calc_3D-150x150.png)
I've been pasting some information from some weblogs into Calc (the [LibreOffice](http://www.libreoffice.org/) Excel equivalent) and some version numbers like 1.5.30 got changed to dates. All the documentation pointed me towards changing the cell format to **text**. That only works if you **type** the numbers, not if you paste them. When you paste them the cell format get changed to **number** again. Read more for the solution...

<!--more-->

One sollution would be to paste as unformatted text. Unfortunately this didn't work for me as I couldn't get the data to align (columns kept overflowing).

The solution I found was to set the **Default** style. Press **F11**, right click on **Modify** and change the format on the **Numbers** tab to text.

No matter how many explanations I read about how this behaviour is a Good Thing (TM) I still consider this type of behaviour brain dead and there should be a switch to disable automatic date formatting.

>  Are all entries in the document text entries? If so, try changing the default format to text. Press F11, right click "Default" in the list in the dialog, choose "Modify" and change the format on the Numbers tab. You could save such a document as a template.
