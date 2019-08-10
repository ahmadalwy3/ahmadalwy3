[Back to Wiki home](https://github.com/gorhill/uBlock/wiki)

***

The _"Advanced settings"_ page contains settings which are experimental, or which are of interest to advanced users who want more control over how uBO behaves internally.

These advanced settings can be easily accessed only when the setting [_"I am an advanced user"_](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) in the _Settings_ pane in the dashboard is checked, but will persist and work even when the setting [_"I am an advanced user"_](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) is not checked:

![Click on the _cogs_ icon](https://cloud.githubusercontent.com/assets/585534/20042797/2800dcd4-a44e-11e6-9bc8-a5e0c960262c.png)

The advanced settings available are described below. Be aware that those settings may change or be removed in the future, or more may be added.

If you want to reset a specific setting to its default value, just delete the value, uBO will fill the missing value with the default one.

If you want to reset all settings to their default values, delete everything then press _"Apply changes"_.

***

#### `allowGenericProceduralFilters`

uBO [1.19.3b8](https://github.com/gorhill/uBlock/commit/1caff7429eceabc712b98b25b5c3929f430d6654) and above.

Default: `false`.

If set to `true`, generic [procedural cosmetic filters](./Procedural-cosmetic-filters) will no longer be discarded as invalid.

Whenever this setting is toggled, the user is responsible of forcing a reload of all filter lists so as to allow uBO to process differently any existing generic procedural cosmetic filters.

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
will disable auto-commenting. So one can use `-` or `none` to disable
auto-commenting.

***

#### `autoUpdateAssetFetchPeriod`

Default: `120` seconds.

When the auto-updater kicks in and an asset in need of update is fetched, this is the number of seconds to wait before fetching the next asset which needs to be updated. The delay helps spread the load on CPU and memory as a result of loading/parsing/compiling the filter lists which have been updated.

***

#### `autoUpdateDelayAfterLaunch`

uBO [1.19.3b9](https://github.com/gorhill/uBlock/commit/72d9758faa40a49f00d2a4671c9db2f519471f0d) and above.

Default: `180` secs.

The number of seconds to wait after launch before an auto-update session<sup>[1]</sup> is started.

<sub>[1] "Update session" means that uBO will lookup and update assets deemed out of date, if any.</sub>

***

#### `autoUpdatePeriod`

Default: `7` hours.

The time to wait in hours between each update session. uBO will always start an update session a few minutes after launch when auto-update is enabled. Once that first update session is completed, uBO will wait `autoUpdatePeriod` hours before starting a new update session.

***

#### `blockingProfileColors`

Default: `#666666 #E7552C #F69454 #008DCB`

Introduced in [1.21.7b5](https://github.com/gorhill/uBlock/commit/7ff750eaf6007bdea4e843d3314fc7275b1ce945)

The badge color will hint at the current blocking mode.
There are four colors for the four following blocking
modes:
- JavaScript wholly disabled
- All 3rd parties blocked
- 3rd-party scripts and frames blocked
- None of the above

The default badge color will be used when JavaScript is not
wholly disabled and when there are no rules for `3p`,
`3p-script` or `3p-frame`. 

The value *must* be a sequence of 4 valid CSS color values that match 6 hexadecimal digits
prefixed with`#` -- anything else will be ignored.

***

#### `blockingProfiles`

Default: `11101 11001 00001`

Introduced in [1.21.0](https://github.com/gorhill/uBlock/commit/693687fd74fe9a4645f0c9c1e6dbedb56b5fb5d7)



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

After [1.18.5b4](https://github.com/gorhill/uBlock/commit/0d369cda21bbce23a7376e0f7b2847a3c7a6d3d8) works in Firefox.

If set to `browser.storage.local`, uBO will use WebExtensions storage as a backend to cache storage.

Additionally, should `indexedDB` not be available for whatever reason,
uBO will automatically fallback to `browser.storage.local`.

uBO 1.18.2 and above, Chromium only.

If set to `indexedDB`, uBO will use [IndexedDB](https://developer.mozilla.org/en-US/docs/Glossary/IndexedDB) as a backend to the cache storage, potentially increasing performance and reducing memory usage. See [#328](https://github.com/uBlockOrigin/uBlock-issues/issues/328) for details.
Bad side effects - filter lists will be out of date in Chrome incognito mode - [#399](https://github.com/uBlockOrigin/uBlock-issues/issues/399).

If `unset`, uBO will use whatever backend storage which is optimal for the current platform.

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

Default: `3` minutes.

uBO 1.18.5b1 and above. Used to be `11` minutes until [1.19.7rc1](https://github.com/gorhill/uBlock/commit/3cf71835c4fc9c262d93a645a3af70946539bd19).

Number of minutes after which _selfie_ (optimized, internal representation of filters) is created.

***

#### `strictBlockingBypassDuration`

Default: `120` seconds.

uBO 1.17.3b4 and above.

Controls duration of the [Strict blocking](https://github.com/gorhill/uBlock/wiki/Strict-blocking) "Temporarily" bypass.

***

#### `suspendTabsUntilReady` (experimental)

Default: `unset`, before [1.18.5b8](https://github.com/gorhill/uBlock/commit/87feb47b51202cb8464eab91597b706965a224f3): `false`.

Possible values:

- `unset`: leave it to the platform to pick the optimal
  behavior (default)
- `no`: do no suspend tab loading at launch time
- `yes`: suspend tab loading at launch time

After [1.18.5b8](https://github.com/gorhill/uBlock/commit/87feb47b51202cb8464eab91597b706965a224f3) configurable again in Firefox. 
After uBO [1.17.5rc0](https://github.com/gorhill/uBlock/commit/41548be6be35fe17dbb996e605c4befb09e16911) - Chromium only. Firefox now uses ["persistent startup listeners"](https://bugzilla.mozilla.org/show_bug.cgi?id=1503721) by default.

If enabled, uBO will hard block all network requests when the browser launches until _all_ the filter lists and rules are loaded and ready, at which time uBO will force a reload of the tabs for which there were network requests blocked during the setup phase.

Disclaimer: especially in Chromium based browsers, even with this setting enabled, it's impossible for uBO to guarantee with 100% certainty that everything will be properly blocked when the browser is launched. **This is a by-design browser issue** -- do _not_ open an issue on uBO issue tracker about this.

Related browser issues:
- Chromium: <https://bugs.chromium.org/p/chromium/issues/detail?id=523634>
- Firefox: <https://bugzilla.mozilla.org/show_bug.cgi?id=1378459>, fixed by <https://bugzilla.mozilla.org/show_bug.cgi?id=1447551>.

***

#### `updateAssetBypassBrowserCache`

Default: `false` 

With [v1.21.7b1](https://github.com/gorhill/uBlock/commit/048bfd251c9b8eeafce020b4f894d736044d6a6f) and above.

If set to `true`, uBO will ensure the browser cache is bypassed when fetching a remote resource.

***

#### `userResourcesLocation` 

Default: `unset`.

One or more space-separated URLs which content will be parsed as token-identified resources to be used for [`redirect`](./Static-filter-syntax#redirect) or [scriptlet-injection](./Static-filter-syntax#scriptlet-injection) (`+js(...)`) purpose.

uBO expects valid content such as can be seen in [resources.txt](https://github.com/uBlockOrigin/uAssets/blob/master/filters/resources.txt), anything else will lead to undefined results.

Any duplicate as per token will result in the previous resource being replaced by the latter one. The resource files are loaded in order of URL appearance, and uBO stock resource file is always loaded first.

Additional resources will be updated at the same time the built-in resource file is updated. Purging the cache of 'uBlock filters' will also purge the cache of the built-in resource file -- and hence force a reload of user-specified resources if any.

The setting was introduced in [1.12.0](https://github.com/gorhill/uBlock/releases/tag/1.12.0). Support for multiple URLs was introduced in [1.19.0](https://github.com/gorhill/uBlock/releases/tag/1.19.0).