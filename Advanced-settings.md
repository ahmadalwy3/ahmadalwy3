[Back to Wiki home](https://github.com/gorhill/uBlock/wiki)

***

The _"Advanced settings"_ page contains settings which are experimental, or which are of interest to advanced users who want more control over how uBO behaves internally.

These advanced settings can be easily accessed only when the setting [_"I am an advanced user"_](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) in the _Settings_ pane in the dashboard is checked, but will persist and work even when the setting [_"I am an advanced user"_](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) is not checked:

![Click on the _cogs_ icon](https://cloud.githubusercontent.com/assets/585534/20042797/2800dcd4-a44e-11e6-9bc8-a5e0c960262c.png)

The advanced settings available are described below. Be aware that those settings may change or be removed in the future, or more may be added.

If you want to reset a specific setting to its defautl value, just delete the value, uBO will fill the missing value with the default one.

If you want to reset all settings to their default values, delete everything then press _"Apply changes"_.

***

#### `assetFetchTimeout`

Default: `30` seconds.

The number of seconds after which uBO throws an error when a remote server fails to respond to a request.

***

#### `autoCommentFilterTemplate`

uBO 1.17.7b2 and above.

Default value is `{{date}} {{origin}}`.

Placeholders are identified by `{{...}}`. There are currently
only three placeholders supported:

- `{{date}}`: will be replaced with current date
- `{{time}}`: will be replaced with current time
- `{{origin}}`: will be replaced with site information on which
  the filter(s) was created

If no placeholder is found in `autoCommentFilterTemplate`, this
will disable auto-commenting. So one can use `-` to disable
auto-commenting.

***

#### `autoUpdateAssetFetchPeriod`

Default: `120` seconds.

When the auto-updater kicks in and an asset in need of update is fetched, this is the number of seconds to wait before fetching the next asset which needs to be updated. The delay helps spread the load on CPU and memory as a result of loading/parsing/compiling the filter lists which have been updated.

***

#### `autoUpdatePeriod`

Default: `7` hours.

The time to wait in hours between each update session<sup>[1]</sup>. uBO will always start an update session a few minutes after launch when auto-update is enabled. Once that first update session is completed, uBO will wait `autoUpdatePeriod` hours before starting a new update session.

<sub>[1] "Update session" means that uBO will lookup and update assets deemed out of date, if any.</sub>

***

#### `cacheControlForFirefox1376932`

Default: `no-cache, no-store, must-revalidate`.

uBO 1.17.0 and above.

Configure how uBO should affect caching for the purpose of dealing with browser bug (see [#229](https://github.com/uBlockOrigin/uBlock-issues/issues/229)).

Possible values:

`no-cache, no-store, must-revalidate`:
- Undesirable side effect: documents themselves for which uBO has to inject CSP directives as a result of filters/ruleset won't be available offline.

`no-cache`:
- Undesirable side effect: One will need to explicitly cache-bypass reload a page each time uBO has to inject CSP directives as a result of filters/ruleset. Note that such cache-bypass reload does not affect only the document itself, but also all secondary resources inside that document.

Related browser issues:
- Firefox: <https://bugzilla.mozilla.org/show_bug.cgi?id=1376932>

***

#### `cacheStorageAPI`

Default: `unset`.

uBO 1.18.2 and above, Chromium only.

If set to `indexedDB`, uBO will use [IndexedDB](https://developer.mozilla.org/en-US/docs/Glossary/IndexedDB) as a backend to the cache storage, potentially increasing performance and reducing memory usage. See [#328](https://github.com/uBlockOrigin/uBlock-issues/issues/328) for details.  If IndexedDB is not available for whatever reasons, uBO will fall back using `browser.local.storage` -- which is expected to always work.

If set to `browser.storage.local` (1.18.5b4+), uBO will use WebExtensions storage as a backend to cache storage.

If `unset`, uBO will use whatever backend storage which is optimal for the current platform.

Bad side effects - filter lists will be out of date in incognito mode - [#399](https://github.com/uBlockOrigin/uBlock-issues/issues/399).

***

#### `cacheStorageCompression`

Default: `true`.

uBO 1.16.21 and above.

If set to true, uBO will lz4-compress data before storing it in its cache storage. The cache storage is used for storing downloaded filter lists, compiled filter lists, selfies. This setting work when IndexedDB is used as the cache storage backend (by default with Firefox/Firefox for Android). See [#141](https://github.com/uBlockOrigin/uBlock-issues/issues/141) for related discussion.

***

#### `consoleLogLevel`

Default: `unset`.

uBO 1.18.5b1 and above

For development purposes only. 

If set to `info`, prints debug messages to the browser console.

***

#### `debugScriptlets`

Default: `false`.

If set to `true`, [`debugger;` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger) will be inserted just before [scriptlet](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#scriptlet-injection) code

***

#### `disableWebAssembly`

Default: `false`.

uBO 1.17.3rc4 and above.

For development purposes only.

If set to `true`, turns off WebAssembly optimizations in uBO code.

***

#### `ignoreRedirectFilters`

Default: `false`.

If set to `true`, uBO will no longer attempt to redirect blocked network requests to a local, neutered version of a resource. The main purpose of redirect filters is to minimize web page breakage as a result of blocking resources.

***

#### `ignoreScriptInjectFilters`

Default: `false`.

If set to `true`, uBO will no longer lookup and inject scriptlets into web pages. The main purpose of the scriptlets is to defuse anti-blocker mechanisms present on some sites.

***

#### `manualUpdateAssetFetchPeriod`

Default: `500` milliseconds.

When clicking the _"Update now"_ button in the _"3rd-party filters"_ pane in the dashboard, this is the number of milliseconds to wait before fetching the next asset which needs to be updated. The delay helps spread the load incurred as a result of loading/processing new filter lists, and its purpose is also to be considerate to remote servers by not subjecting them to rapid-fire requests.

***

#### `popupFontSize`

Default: `unset`.

A valid CSS font size value (`14px`) to use for the popup panel. Use if you are unhappy with the default size.

***

#### `requestJournalProcessPeriod`

Default: `1000` milliseconds.

uBO 1.16.21b2 and above.

Controls the delay before uBO internally process it's network request journal queue. The network request journal queue exists for the purpose of fixing [issue 2053](https://github.com/gorhill/uBlock/issues/2053).

As a benign side effect to the fix, there is a delay in displaying the number of blocked requests on extension icon (see [#155](https://github.com/uBlockOrigin/uBlock-issues/issues/155)).

A lower delay than the default one could bring back the issue it's meant to fix.

***

#### `selfieAfter`

Default: `11` minutes.

uBO 1.18.5b1 and above.

Number of minutes after which _selfie_ (optimized, internal representation of filters) is created.

***

#### `strictBlockingBypassDuration`

Default: `120` seconds.

uBO 1.17.3b4 and above.

Controls duration of the [Strict blocking](https://github.com/gorhill/uBlock/wiki/Strict-blocking) "Temporarily" bypass.

***

#### `suspendTabsUntilReady` (experimental)

Default: `false`.

After uBO [1.17.5rc0](https://github.com/gorhill/uBlock/commit/41548be6be35fe17dbb996e605c4befb09e16911) - Chromium only. Firefox now uses ["persistent startup listeners"](https://bugzilla.mozilla.org/show_bug.cgi?id=1503721) by default.

If set to `true`, uBO will hard block all network requests when the browser launches until _all_ the filter lists and rules are loaded and ready, at which time uBO will force a reload of the tabs for which there were network requests blocked during the setup phase.

Disclaimer: even with this setting enabled (set to `true`), it's impossible for uBO to guarantee with 100% certainty that everything will be properly blocked when the browser is launched. **This is a by-design browser issue** -- do _not_ open an issue on uBO issue tracker about this.

Related browser issues:
- Chromium: <https://bugs.chromium.org/p/chromium/issues/detail?id=523634>
- Firefox: <https://bugzilla.mozilla.org/show_bug.cgi?id=1378459>

***

#### `userResourcesLocation` 

Default: `unset`.

uBO 1.11.5 and above.

If set to a valid URL, uBO will load the content of the URL and parse it as token-identified resources to be used for `redirect` or `script:inject` purpose. For example, I use this setting to test resources before publishing them for [uAssets](https://github.com/uBlockOrigin/uAssets). uBO expects valid content such as can be seen in [resources.txt](https://github.com/uBlockOrigin/uAssets/blob/master/filters/resources.txt), anything else will lead to undefined results.