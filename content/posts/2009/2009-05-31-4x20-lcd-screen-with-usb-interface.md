---
title: 4×20 LCD screen with USB interface.
author: silviu
type: post
date: 2009-05-31T15:50:54+00:00
url: /2009/05/31/4x20-lcd-screen-with-usb-interface/
categories:
  - old
tags:
  - 18f2550
  - lcd
  - microchip
  - pic
  - temp_on
  - usb

---
Attaching an LCD screen to a pc is a pretty easy job. I am working on a jukebox that I wanted to a screen attached to. Although a HD44780 based LCD can be attached to the parallel port with almost no additional parts I wanted a more flexible solution, and I thought about microcontrollers with usb support. I found a thread [here](http://forums.bit-tech.net/showthread.php?t=115461), where all the work is pretty much done. Thank you ch424. All credits for the design and firmware should go to him. I am simply documenting here my build. You can find on the thread mentioned everything you need - firmware, drivers, schematics, programmer configuration. By the way I used the Easy Pic 5 from Mikroelektronika to program my PIC and do some initial testing. The settings for Picflash were similar with the ones ch424 shows for his Winpic.  If you are having trouble programming with Picflash from mikroe drop a comment and I'll try to help you.

## The project

The design is based around a **PIC18F2550** from Microchip. You will also need an LCD screen, one that is up to 20&#215;4 and HD44780 or KS0066U compliant. The design can also accommodate some GPOs, a rotary encoder and a buzzer. I plan to add the rotary encoder soon.

![Just the screen](/blog/images/2009/img_7769_cnv.jpg)

The screen all up and running.

![Soldering the connector for the LCD screen](/blog/images/2009/img_7767_cnv.jpg)

I soldered a female connector to the LCD board so I can connect the screen both to my Easy Pic 5 development board and the USB backpack.

![All done and working](/blog/images/2009/img_7775_cnv.jpg)
![All done and working](/blog/images/2009/img_7777_cnv.jpg)

For now I tested the screen with [Lcdsmartie][1] but later on I plan to use it with lcdproc on linux.

![The custom made board](/blog/images/2009/img_7779_cnv.jpg)
![The board, closer](/blog/images/2009/img_7785_cnv.jpg)

Should the thread or the board disappear just drop a comment and I can mirror the .hex file, the schematic and the pcb layout.

 [1]: http://lcdsmartie.sourceforge.net/
