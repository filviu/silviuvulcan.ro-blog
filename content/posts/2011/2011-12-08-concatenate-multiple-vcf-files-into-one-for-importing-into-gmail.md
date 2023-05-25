---
title: 'Concatenate multiple *.vcf files into one for importing into gMail'
author: silviu
type: post
date: 2011-12-08T13:46:50+00:00
url: /2011/12/08/concatenate-multiple-vcf-files-into-one-for-importing-into-gmail/
dsq_thread_id:
  - 497632496
categories:
  - old
tags:
  - android
  - gmail
  - maemo
  - n900
  - temp_on

---
I have a secondary phone that is running Android. My main phone is still a Nokia N900 for which I gave up trying to sync contacts with gmail. Two options basically exist for n900 none of which works for me:

  1. using MFE which works from time to time
  2. use syncevolution which invariably screws my contacts on the n900 (I guess google&#8217;s implementation of syncml or exchange support is dubious at best)

So I devised a third. Since I edit and store all my contacts on the n900 I will export them from time to time **(Contacts->Export->All contacts) ** and import them manually into gmail. **_Note that Gmail doesn&#8217;t support vCard 3.0; you have to export as 2.1_**. Unfortunately the n900 will export each contact into a separate file. Since google doesn&#8217;t offer bulk import support I thought of concatenating all files into one:

**cat *.vcf > all_contacts.vcf**

Good idea, but it doesn&#8217;t work. In another example of fine programming skills clicking import uploads the file and returns with no contact imported and **no error message**. Nice one.

It seems some new lines are missing; and so this will work (in the folder with the vcf files)

[ccNe_bash]  
for i in *.vcf; do cat &#8220;$i&#8221; >> ../all\_contacts.vcf; echo >> ../all\_contacts.vcf; done  
[/ccNe_bash]  
Import worked now ok!

Update:

Here&#8217;s courtesy of Adam A Johnson (in the comments below) how to do the same in Windows.  
[ccNe_dos]  
FOR %f IN (*.vcf) DO TYPE &#8220;%f&#8221; >> all\_contacts.vcf & ECHO. >> all\_contacts.vcf  
[/ccNe_dos]  
&nbsp;