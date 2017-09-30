### Read carefully if using uBO/webext

There are many [reports](http://forums.mozillazine.org/viewtopic.php?p=14764474#p14764474) of people experiencing issues with some web sites, or images not loading, etc. Turns out many of these are a result of using some legacy extensions along uBO/webext. For instance, Reek's AAK in [GreaseMonkey](https://www.reddit.com/r/uBlockOrigin/comments/6xl3em/image_links_suddenly_blocked_by_ublock_origin/) has been [causing](https://www.reddit.com/r/firefox/comments/6x8hbe/ublock_origin_is_a_webextension_in_amo_stable/dmf6j5k/) issues with images not loading.

If you experience such issue, you will have to disable all your legacy extensions and see if this fixes your issue. If so, then you will have to re-enable your legacy extension one by one to find the one(s) causing the problem.

Those legacy extensions can cause multi-process to be disabled in your browser, and apparently **when multi-process is disabled**, this can cause many cases of [page load failure](https://bugzilla.mozilla.org/show_bug.cgi?id=1348497#c27).

Everything is moving to WebExtensions, so it might be just a good time to start giving up on legacy extensions, they are not going to be supported at all in a couple of weeks when Firefox 57 is released.

There are also Firefox issues specific to webext extensions which can cause a web page to load improperly:

- [Extension with listener at webRequest.onHeadersReceived breaks navigation (crash/blank page) when the previous page performs sync XHR upon unload](https://bugzilla.mozilla.org/show_bug.cgi?id=1401516)
- [Empty page using uBo / ABP webext (even whitelisting the site)](https://bugzilla.mozilla.org/show_bug.cgi?id=1396226)
- [Presence of an Webextension makes the head element missing on (iframe) load](https://bugzilla.mozilla.org/show_bug.cgi?id=1375875)

Another option is to install [uBO 1.13.8](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/versions/?page=1#version-1.13.8) and disable auto-update for it.

***

### Tentative schedule

(This needs to be updated -- there might be obsolete information below)

This page may update often until there is a stable release of uBO/webext.

| Tentative schedule | July 19 | Aug. 10 | Aug. 22 | Sep. 19 | Nov. 14 |
| ----- |:-----:|:-----:|:-----:|:-----:|:-----:|
| Firefox stable is...  | Firefox 54 | Firefox 55 |        |         | [Firefox 57](https://blog.mozilla.org/addons/2017/02/16/the-road-to-firefox-57-compatibility-milestones/) |
| AMO dev channel | [uBO/webext<br>hybrid](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/versions/beta?page=1#version-1.13.9b7) | [uBO/webext](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/versions/beta) |       |       |       |
| AMO stable channel |       |       | uBO/webext<br>hybrid | uBO/webext |       |
| Blocking |       | ~~[1367494](https://bugzilla.mozilla.org/show_bug.cgi?id=1367494)~~ |       |
| Non-blocking |       | [1313401](https://bugzilla.mozilla.org/show_bug.cgi?id=1313401)<br>[1303384](https://bugzilla.mozilla.org/show_bug.cgi?id=1303384) |       |

- **uBO/legacy**: compatible with Firefox 24 to Firefox 56
- **uBO/webext-hybrid**: compatible with Firefox 54 to Firefox 56
    - Use to migrate settings from uBO/legacy to uBO/webext
- **uBO/webext**: compatible with Firefox 54 and above

### First install

The first time uBO/webext-hybrid executes, there might be a noticeable delay<sup>[1]</sup>: this is caused by the fact that uBO/webext-hybrid will import all the data from legacy storage, into webext storage. This is done only the first time the uBO/webext-hybrid is executed, after this the import step will be skipped.

If you subsequently remove uBO/webext-hybrid, this will cause the webext storage to be removed by Firefox, and upon re-installing the uBO/webext-hybrid version, the import code will again kick in.

Note that uBO/webext-hybrid will still be labelled as "Legacy" in `about:addons`, because uBO/webext-hybrid is really an [embedded WebExtension](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Embedded_WebExtensions). Once the legacy storage has been imported at first install by the thin legacy wrapper, uBO/webext-hybrid will fully function as a pure webext extension despite the "Legacy" label.

The legacy storage is left untouched by uBO/webext-hybrid, so you can always go back to uBO/legacy (stable release) if you do not want to use the webext-hybrid version in the short term.

<sub>[1] A few seconds on my older than mainstream CPU with default settings/lists. The more filter lists you have enabled, the longer it will take.</sub>

### Firefox for Android

As per [documentation](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Differences_between_desktop_and_Android), only with Firefox Mobile 55 (beta) you can access uBO's popup panel.

~~However it appears there is an issue with installing webext extensions on Firefox for Android 55, the browser thinks the extensions are corrupted -- this does not appear specific to uBO/webext. Consequently, for now it seems it's best to stick to uBO/legacy on Firefox for Android.~~ **Update:** this is fixed: <https://bugzilla.mozilla.org/show_bug.cgi?id=1367494>.

### Differences with uBO/legacy

- `script:contains` filters will stop working
    - uBO's own filter lists have long ceased to rely on this filter syntax to solve reported filtering issues.
- ~~cosmetic filters will no longer use the browser's user styles~~ [Fixed with f32868766340e2fb8ec689f4b5683a413de847b6](https://github.com/gorhill/uBlock/commit/f32868766340e2fb8ec689f4b5683a413de847b6)
- uBO/webext has limited access to behind-the-scene network requests, unlike uBO/legacy which had full access to all behind-the-scene network requests. For example, you won't be able to see (and block) network requests made by other extensions. Related: ["Support moz-extension: urls in MatchPattern"](https://bugzilla.mozilla.org/show_bug.cgi?id=1271354#c14).

### Tentative schedule

As stated above, the current version of uBO/webext-hybrid is _really_ an embedded WebExtension. The pure webext version of uBO, uBO/webext is now available in the [Releases section](https://github.com/gorhill/uBlock/releases), and in the [dev channel on AMO](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/versions/beta).

Stable release of uBO/webext must be available to all users when [Firefox 57 is released](https://blog.mozilla.org/addons/2017/02/16/the-road-to-firefox-57-compatibility-milestones/).

However, before releasing uBO/webext to stable channel on AMO, I must release uBO/webext-hybrid first, a necessary step for a seamless transition to uBO/webext.

These are the dates of coming Firefox stable release versions, as per [RapidRelease/Calendar](https://wiki.mozilla.org/RapidRelease/Calendar):

- Firefox 55: August 8
- Firefox 56: September 26
- Firefox 57: November 14

This is what I plan:

- August 8 + 2 weeks
    - uBO/webext-hybrid published on AMO's stable channel
    - uBO/webext published on AMO's dev channel
- uBO/webext-hybrid publication + 4 weeks = September 19
    - uBO/webext published on AMO's stable channel
    - Could be sooner if uBO/webext-hybrid is being used by most users sooner than expected.

### Future of uBO/legacy

For all those Firefox and Firefox-based browsers based on Firefox v52 and less, the dev channel of uBO will cease to work, and they will have to install manually the `xpi` version from the repo here if you want to keep using the dev version of uBO, or install the [stable version of uBO on AMO](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/).

As of writing, there is no plan to cease development of uBO/legacy. Hypothetically, this may change in some future if ever it becomes really non-trivial to keep a working the legacy version.

I do expect users of legacy versions of Firefox to test and report any issues with uBO -- I can't afford the time needed to test all those versions.

If you still want to use uBO/legacy, a volunteer created an extension to enable uBO/webext to update automatically: <https://github.com/JustOff/ublock0-updater>.

### Miscellaneous

[Issue #2795](https://github.com/gorhill/uBlock/issues/2795) will be a collection of [bugzilla.mozilla.org](https://bugzilla.mozilla.org/) issues which currently affect the uBO/webext specifically.

Be sure to create backups of your uBO settings, if the transition from uBO/legacy to uBO/webext fails, you can always just restore all your settings from the backup file (see [_Settings_ pane in the dashboard for the backup/restore features](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#backuprestore-section)).