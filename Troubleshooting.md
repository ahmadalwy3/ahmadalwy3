I am going to collect here common usage issues users may face.

The best way to troubleshoot uBlock is with uBlock: the [logger](./The-logger) will tell you what uBlock is doing when you try to load a web page. Using the logger is the first thing you should try when you are trying to find out why a page does not load/display as expected.

***

#### Firefox: uBlock's popup UI is not displaying

You can fix this by following the following steps:
1.  In the navigation bar (Awesome Bar) enter `about:config`
2.  Click on the `I'll be careful, I promise!` button
3.  Search for `ublock0`
4.  Double click on `extensions.ublock0.forceLegacyToolbarButton` so that the value = `true`
5.  Restart Firefox

***

#### Firefox: Missing icons in uBlock's popup UI

You can fix this by following the following steps:
1.  If you use a Linux system go to Edit - Settings - Content and choose a default font other than "serif". "Liberation" and "Clear" are known to work.
2.  If the icons are still not showing enter `about:config` in the navigation bar and promise to be careful
3.  Search for `fonts`
4.  Check that gfx.downloadable_fonts.enabled is set to 'true' and see whether the icons appear now. 
5.  If it still does not work you might have to set browser.display.use_document_fonts to '1' but that should not be necessary if you followed step 1.

***

#### Links to social networks are blocked

Because you enabled _"Fanboy’s Social Blocking List"_, or one of the filter lists which includes it, like _"Fanboy’s Annoyance List"_ or _"Fanboy+Easylist-Merged Ultimate List"_.

***

#### My antivirus flags uBlock

False positive.

uBlock ships with malware filter lists, and this causes [false positives](https://github.com/gorhill/uBlock/issues/199) in some antiviruses.

***

#### "NETWORK FAILED" error when I try to install uBlock Origin from Chrome store

Unfortunately, your Chrome browser executable has probably been [tampered by malware](https://code.google.com/p/chromium/issues/detail?id=391552#c153):

> At this point we're pretty sure that this error is primarily caused by malware / unwanted software on your machine actively tampering with the contents of the chrome binary and your user profile directory data

You will need to clean up whatever malware tampered with your Chrome browser installation. Starts here:
[Malwarebytes Anti-Malware](https://www.malwarebytes.org/)

***

#### uBlock Origin stopped blocking ads

I've seen this happens on a Chromium-based browser. Upon investigation, even though uBO's icon was on the toolbar, I found that the extension was not actually in memory. I believe this problem coincided with uBO having been updated with a new version from the Chrome store. Forcing a restart of uBO fixed the issue (uncheck then check _Enable_ in the _Extensions_ page).

So it does appear the browser's automated update of an extension can go wrong sometimes. Forcing a restart of the extension fixes the issue.

***

#### uBlock Origin uninstall itself

This has been reported many times. This could be caused a false positive from your anti-virus application.

Specifically, it has been confirmed [Avira Anti-virus has been uninstalling uBlock Origin](https://github.com/gorhill/uBlock/issues/882).

***

#### Unable to open links in new tab

- Are you using the [no-popups switch](./Quick-guide:-popup-user-interface#no-popups)?
- Are you using a Chromium-based browser?

If you answer "yes" to both questions above, this is your problem (from link above):

> **Caveat for Chromium-based browsers:** Due to Chromium API limitations, it's not possible for uBlock to determine for sure whether a new tab being opened is that of a popup, or is the result of a legitimate click on a link by the user. So if the no-popups switch is in use, you won't be able to open a link in a new tab through the context menu.

***
