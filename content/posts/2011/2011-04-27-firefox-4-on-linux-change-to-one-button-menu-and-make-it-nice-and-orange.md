---
title: Firefox 4 on linux change to one button menu and make it nice and orange
author: silviu
type: post
date: 2011-04-27T05:13:32+00:00
url: /2011/04/27/firefox-4-on-linux-change-to-one-button-menu-and-make-it-nice-and-orange/
categories:
  - old
tags:
  - button
  - firefox
  - menu
  - temp_on

---
![firefox orange button](/blog/images/2011/linux_firefox_orange_button.png) When I upgraded to Firefox 4 on my linux machines I was disappointed to see that the classic menu bar remained. I'm not necesarily a fan of the new ribbon  interfaces but since I don't use the menu often and so prefer to use the space for something useful, like the tabs.

Reducing the menu bar to a button is easy.

**Right click on the menu bar** and uncheck **Menu bar**

At this point the menu is reduced to a button, unfortunately an ugly button. If you want it nice and orange you need to hack your `userChrome.css` file:

```bash
cd ~/.mozilla/firefox/xxxxxxxx.default/chrome
vi userChrome.css
```

Paste the following:

```css
/*
* Edit this file and copy it as userChrome.css into your
* profile-directory/chrome/
*/

/*
* This file can be used to customize the look of Mozilla's user interface
* You should consider using !important on rules which you want to
* override default settings.
*/

/*
* Do not remove the @namespace line - it's required for correct functioning
*/
@namespace url("http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul"); /\* set default namespace to XUL \*/

#appmenu-toolbar-button {
list-style-image: url(data:image/png;base64,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) !important;
margin-left: -3px!important;
margin-top: -5px!important;
padding-right: 2px!important;
padding-bottom: 1px!important;
border:0!important;
-moz-appearance: none!important;
opacity: 0.8;
}

#appmenu-toolbar-button:hover {
opacity: 1!important;
-moz-transition-duration:0.5s!important;
}

#appmenu-toolbar-button > .toolbarbutton-text,
#appmenu-toolbar-button > .toolbarbutton-menu-dropmarker {
display: none !important;
}
```

Save the file and restart firefox.