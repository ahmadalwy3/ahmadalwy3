| Tentative schedule | July 19 | August 22 | October 3 | November 14 |
| ----- |:-----:|:-----:|:-----:|:-----:|
| Firefox stable is...  | Firefox 54 | Firefox 55 | Firefox 56 | [Firefox 57](https://blog.mozilla.org/addons/2017/02/16/the-road-to-firefox-57-compatibility-milestones/) |
| AMO dev channel | [uBO/webext<br>hybrid](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/versions/beta) | uBO/webext |       |       |
| AMO stable channel |       | uBO/webext<br>hybrid | uBO/webext |       |
| Blocking |       | [1367494](https://bugzilla.mozilla.org/show_bug.cgi?id=1367494)<br>[1313401](https://bugzilla.mozilla.org/show_bug.cgi?id=1313401) |       |

This page may update often until there is a stable release of uBO/webext.
 
### First install

The first time uBO/webext-hybrid executes, there might be a noticeable delay (a few seconds): this is caused by the fact that uBO/webext-hybrid will import all the data from legacy storage, into webext storage. This is done only the first time the uBO/webext-hybrid is executed, after this the import step will be skipped.

If you subsequently remove uBO/webext-hybrid, this will cause the webext storage to be removed by Firefox, and upon re-installing the uBO/webext-hybrid version, the import code will again kick in.

Note that uBO/webext-hybrid will still be labelled as "Legacy" in `about:addons`, because uBO/webext-hybrid is really a [webext-hybrid extension](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Embedded_WebExtensions). Once the legacy storage has been imported at first install by the thin legacy wrapper, uBO/webext-hybrid will fully function as a pure webext extension despite the "Legacy" label.

The legacy storage is left untouched by uBO/webext-hybrid, so you can always go back to uBO/legacy (stable release) if you do not want to use the webext-hybrid version in the short term.

### Firefox for Android

As per [documentation](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Differences_between_desktop_and_Android), only with Firefox Mobile 55 (beta) you can access uBO's popup panel.

~~However it appears there is an issue with installing webext extensions on Firefox for Android 55, the browser thinks the extensions are corrupted -- this does not appear specific to uBO/webext. Consequently, for now it seems it's best to stick to uBO/legacy on Firefox for Android.~~ **Update:** this is fixed: <https://bugzilla.mozilla.org/show_bug.cgi?id=1367494>.

### Differences with uBO/legacy

- `script:contains` filters will stop working
    - uBO's own filter lists have long ceased to rely on this filter syntax to solve reported filtering issues.
- ~~cosmetic filters will no longer use the browser's user styles~~ [Fixed with f32868766340e2fb8ec689f4b5683a413de847b6](https://github.com/gorhill/uBlock/commit/f32868766340e2fb8ec689f4b5683a413de847b6)
- uBO/webext has limited access to behind-the-scene network requests, unlike uBO/legacy which had full access to all behind-the-scene network requests. For example, you won't be able to see (and block) network requests made by other extensions. Related: ["Support moz-extension: urls in MatchPattern"](https://bugzilla.mozilla.org/show_bug.cgi?id=1271354#c14).

### Tentative schedule

As stated above, the current version of uBO/webext-hybrid is _really_ a hybrid version. The pure webext version of uBO, uBO/webext is now available in the [Releases section](https://github.com/gorhill/uBlock/releases).

Stable release of uBO/webext must be available to all users when [Firefox 57 is released](https://blog.mozilla.org/addons/2017/02/16/the-road-to-firefox-57-compatibility-milestones/).

Of course for practical reasons, the stable release of uBO/webext should be available on AMO in advance of Firefox 57 release date.

So I am just going to try this: publish stable release of uBO/webext one release cycle ahead of Firefox 57, i.e. publish stable uBO/webext when Firefox 56 is released.

However, before releasing uBO/webext to stable channel on AMO, I must release uBO/webext-hybrid first, a necessary step for a seamless transition to uBO/webext. Again, it feels reasonable to publish uBO/webext-hybrid one release cycle ahead of Firefox 56, i.e. publish stable uBO/webext-hybrid when Firefox 55 is released.

These are the dates of coming Firefox stable release versions, as per [RapidRelease/Calendar](https://wiki.mozilla.org/RapidRelease/Calendar):

- Firefox 55: August 8
- Firefox 56: September 26
- Firefox 57: November 14

Ideally this is what should happen:

- August 8 + 2 weeks
    - uBO/webext-hybrid published on AMO's stable channel
    - uBO/webext published on AMO's dev channel
- September 26 + 2 weeks
    - uBO/webext published on AMO's stable channel

However this is theoretical:
- uBO/webext-hybrid on Firefox for Android is not ready yet: 
    - Firefox for Android 54: no way to access the popup panel or dashboard.
    - Firefox for Android 55 (beta): "The add-on downloaded from addons.cdn.mozilla.net could not be installed because it appears to be corrupt".
    - Firefox for Android 56 (nightly): works.

### Future of uBO/legacy

For all those Firefox and Firefox-based browsers based on Firefox v53 and less, the dev channel of uBO will cease to work, and they will have to install manually the `xpi` version from the repo here if you want to keep using the dev version of uBO, or install the [stable version of uBO on AMO](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/).

As of writing, there is no plan to cease development of uBO/legacy. Hypothetically, this may change in some future if ever it becomes really non-trivial to keep a working the legacy version.

### Miscellaneous

[Issue #2795](https://github.com/gorhill/uBlock/issues/2795) will be a collection of [bugzilla.mozilla.org](https://bugzilla.mozilla.org/) issues which currently affect the uBO/webext specifically.

Be sure to create backups of your uBO settings, if the transition from uBO/legacy to uBO/webext fails, you can always just restore all your settings from the backup file (see [_Settings_ pane in the dashboard for the backup/restore features](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#backuprestore-section)).