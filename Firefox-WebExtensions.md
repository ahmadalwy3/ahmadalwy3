Stable release of uBO/webext has been available on AMO since early September 2017. uBO/webext is compatible with Firefox 52 and above. With Firefox 52 specifically, some features in uBO/webext may be disabled.

- [Read carefully if using uBO/webext](#read-carefully-if-using-ubowebext)
- [Firefox for Android](#firefox-for-android)
- [Future of uBO/legacy](#future-of-ubolegacy)

### Read carefully if using uBO/webext

uBO/webext works best with Firefox 57 and above, and with multi-process enabled.

There are many [reports](http://forums.mozillazine.org/viewtopic.php?p=14764474#p14764474) of people experiencing issues with some web sites, or images not loading, etc. Turns out many of these are a result of using some legacy extensions along uBO/webext. For instance, Reek's AAK in [GreaseMonkey](https://www.reddit.com/r/uBlockOrigin/comments/6xl3em/image_links_suddenly_blocked_by_ublock_origin/) has been [causing](https://www.reddit.com/r/firefox/comments/6x8hbe/ublock_origin_is_a_webextension_in_amo_stable/dmf6j5k/) issues with images not loading.

If you experience such issue, you will have to disable all your legacy extensions and see if this fixes your issue. If so, then you will have to re-enable your legacy extensions one by one to find the one(s) causing the problem.

Those legacy extensions can cause multi-process to be disabled in your browser, and apparently **when multi-process is disabled**, this can cause many cases of [page load failure](https://bugzilla.mozilla.org/show_bug.cgi?id=1348497#c27).

**Update (2018-06-30)**: if you experience above problems in Waterfox then this problem will probably be fixed in next Waterfox release (56.2.2)

Everything is moving to WebExtensions, so it might be just a good time to start giving up on legacy extensions, they are not going to be supported at all in a couple of weeks when Firefox 57 is released. See if there is a beta webext version of any of your legacy extensions. For example, there is [beta webext version of Greasemonkey on AMO](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/versions/beta).

There are also Firefox issues specific to webext extensions which can cause a web page to load improperly:

- [Extension with listener at webRequest.onHeadersReceived breaks navigation (crash/blank page) when the previous page performs sync XHR upon unload](https://bugzilla.mozilla.org/show_bug.cgi?id=1401516)
  - duplicate of [1396395 - Firefox crashes when submitting form](https://bugzilla.mozilla.org/show_bug.cgi?id=1396395) - RESOLVED FIXED in Firefox 58
- [Empty page using uBo / ABP webext (even whitelisting the site)](https://bugzilla.mozilla.org/show_bug.cgi?id=1396226)
  - duplicate of [1379148 - document.write does not synchronously modify a document if an extension has content scripts at document_start](https://bugzilla.mozilla.org/show_bug.cgi?id=1379148) - VERIFIED FIXED in Firefox 57
- [Presence of an Webextension makes the head element missing on (iframe) load](https://bugzilla.mozilla.org/show_bug.cgi?id=1375875)

Another option is to install [uBO 1.13.8](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/versions/?page=1#version-1.13.8) and disable auto-update for it.

Having issues with uBO's cache storage being wiped-out on every restart of the browser? See if <http://forums.mozillazine.org/viewtopic.php?f=9&t=3034189> helps.

**Update (2018-06-30)**: if you still have problems with filter list being out of date on every restart check this [Mozilla bug 944918 - indexedDB broken - UnknownError - Error opening Database](https://bugzilla.mozilla.org/show_bug.cgi?id=944918) In overall your IndexedDB database may be corrupted ([in various ways](https://bugzilla.mozilla.org/show_bug.cgi?id=944918#c30)) and only way to fix this is to find database folder and remove it. One special case of "corruption" may appear when you browse database folders and you file explorer drops hidden files in database directory (for example `.directory` dropped by [Dolphin in KDE](https://bugzilla.mozilla.org/show_bug.cgi?id=944918#c32)) - deleting these unwanted files will fix the problem.

### Firefox for Android

**Firefox for Android 56:** you can access the popup panel using the "uBlock Origin" menu entry. However, the dashboard can't be accessed through `about:addons`. This is fixed in Firefox for Android 57. The workaround is to open uBO's dashboard through uBO's popup panel. Once you access the dashboard, you could create a bookmark out of it to allow direct access in the future.

**Firefox for Android 55:** As per [documentation](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Differences_between_desktop_and_Android), only with Firefox Mobile 55 (beta) you can access uBO's popup panel.

### Differences with uBO/legacy

- `script:contains` filters will stop working
    - uBO's own filter lists have long ceased to rely on this filter syntax to solve reported filtering issues.
- ~~cosmetic filters will no longer use the browser's user styles~~ [Fixed with f32868766340e2fb8ec689f4b5683a413de847b6](https://github.com/gorhill/uBlock/commit/f32868766340e2fb8ec689f4b5683a413de847b6)
- uBO/webext has limited access to behind-the-scene network requests, unlike uBO/legacy which had full access to all behind-the-scene network requests. For example, you won't be able to see (and block) network requests made by other extensions. Related: ["Support moz-extension: urls in MatchPattern"](https://bugzilla.mozilla.org/show_bug.cgi?id=1271354#c14).

### Future of uBO/legacy

For all those Firefox and Firefox-based browsers based on Firefox v52 and less, uBO from <https://addons.mozilla.org/> will cease to work, and they will have to [install manually the `xpi` version](https://github.com/gorhill/uBlock/tree/master/dist#firefox-legacy) from the repo here if you want to keep using the dev version of uBO.

As of writing, there is no plan to cease development of uBO/legacy. Hypothetically, this may change in some future if ever it becomes really non-trivial to keep a working legacy version.

I do expect users of legacy versions of Firefox to test and report any issues with uBO -- I can't afford the time needed to test all those versions.

If you still want to use uBO/legacy, a volunteer created an extension to enable uBO/webext to update automatically: <https://github.com/JustOff/ublock0-updater>.

### Miscellaneous

[Issue #2795](https://github.com/gorhill/uBlock/issues/2795) will be a collection of [bugzilla.mozilla.org](https://bugzilla.mozilla.org/) issues which currently affect the uBO/webext specifically.

Be sure to create backups of your uBO settings, if the transition from uBO/legacy to uBO/webext fails, you can always just restore all your settings from the backup file (see [_Settings_ pane in the dashboard for the backup/restore features](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#backuprestore-section)).

***

[1]: 2018-06-30 updates and solution for "corrupted database" problem thanks to [grahamperrin message](https://discourse.mozilla.org/t/support-ublock-origin/6746/734)