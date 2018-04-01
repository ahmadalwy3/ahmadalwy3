[Back to Wiki home](https://github.com/gorhill/uBlock/wiki)

***

The _"Advanced settings"_ page contains settings which are experimental, or which are of interest to advanced users who want more control over how uBO behaves internally.

These advanced settings can be easily accessed only when the setting [_"I am an advanced user"_](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) in the _Settings_ pane in the dashboard is checked:

![Click on the _cogs_ icon](https://cloud.githubusercontent.com/assets/585534/20042797/2800dcd4-a44e-11e6-9bc8-a5e0c960262c.png)

The advanced settings available are described below. Be aware that those settings may change or be removed in the future, or more may be added.

If you want to reset a specific setting to its defautl value, just delete the value, uBO will fill the missing value with the default one.

If you want to reset all settings to their default values, delete everything then press _"Apply changes"_.

***

#### `assetFetchTimeout`

Default: `30` seconds.

The number of seconds after which uBO throws an error when a remote server fails to respond to a request.

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

#### `ignoreRedirectFilters`

Default: `false`.

If set to `true`, uBO will no longer attempt to redirect blocked network requests to a local, neutered version of a resource. The main purpose of redirect filters is to minimize web page breakage as a result of blocking resources.

***

#### `ignoreScriptInjectFilters`

Default: `false`.

If set to `true`, uBO will no longer lookup and inject scriptlets into web pages. The main purpose of the scriptlets is to defuse anti-blocker mechanisms present on some sites.

***

#### `manualUpdateAssetFetchPeriod`

Default: `2000` milliseconds.

When clicking the _"Update now"_ button in the _"3rd-party filters"_ pane in the dashboard, this is the number of milliseconds to wait before fetching the next asset which needs to be updated. The delay helps spread the load incurred as a result of loading/processing new filter lists, and its purpose is also to be considerate to remote servers by not subjecting them to rapid-fire requests.

***

#### `popupFontSize`

Default: `unset`.

A valid CSS font size value (`14px`) to use for the popup panel. Use if you are unhappy with the default size.

***

#### `streamScriptInjectFilters`

Default: `false`.

The purpose is to tell uBO to use stream filtering to inject scriptlets where possible. If set to `true`, it brings back scriptlet injection through stream filtering as was the default before `1.15.10`. A fix has also been added to resolve [uBlockOrigin/uAssets#1492](https://github.com/uBlockOrigin/uAssets/issues/1492), which was the main reason to disable stream filtering-based scriptlets injection in 1.15.10.

***

#### `suspendTabsUntilReady` (experimental)

Default: `false`.

If set to `true`, uBO will hard block all network requests when the browser launches until _all_ the filter lists and rules are loaded and ready, at which time uBO will force a reload of the tabs for which there were network requests blocked during the setup phase.

Disclaimer: even with this setting enabled (set to `true`), it's impossible for uBO to guarantee with 100% certainty that everything will be properly blocked when the browser is launched. **This is a by-design browser issue** -- do _not_ open an issue on uBO issue tracker about this.

Related issues:
- Chromium: <https://bugs.chromium.org/p/chromium/issues/detail?id=523634>
- Firefox: <https://bugzilla.mozilla.org/show_bug.cgi?id=1378459>

***

#### `userResourcesLocation` 

Default: `unset`.

uBO 1.11.5 and above.

If set to a valid URL, uBO will load the content of the URL and parse it as token-identified resources to be used for `redirect` or `script:inject` purpose. For example, I use this setting with a `file:///`-based URL to test resources before publishing them for [uAssets](https://github.com/uBlockOrigin/uAssets). uBO expects valid content such as can be seen in [resources.txt](https://github.com/uBlockOrigin/uAssets/blob/master/filters/resources.txt), anything else will lead to undefined results.