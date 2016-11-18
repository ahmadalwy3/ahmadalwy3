[Back to Wiki home](https://github.com/gorhill/uBlock/wiki)

***

The _"Advanced settings"_ page contains settings which are experimental, or which are of interest to advanced users who want more control over how uBO behaves internally.

These advanced settings can be easily accessed only when the setting [_"I am an advanced user"_](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) in the _Settings_ pane in the dashboard is checked:

![Click on the _cogs_ icon](https://cloud.githubusercontent.com/assets/585534/20042797/2800dcd4-a44e-11e6-9bc8-a5e0c960262c.png)

The advanced settings available are described below. Be aware that those settings may change or be removed in the future, or more may be added.

If you want to reset a specific setting to its defautl value, just delete the value, uBO will fill the missing value with the default one.

If you want to reset all settings to their default values, delete everything then press _"Apply changes"_.

***

`ignoreRedirectFilters`: if set to `true`, uBO will no longer attempt to redirect blocked network requests to a local, neutered version of a resource. The main purpose of redirect filters is to minimize web page breakage as a result of blocking resources.

`ignoreScriptInjectFilters`: if set to `true`, uBO will no longer lookup and inject scriplets into web pages. The main purpose of the scriptlets is to defuse anti-blocker mechanisms present on some sites.

`popupFontSize`: a valid CSS font size value to use for the popup panel. Use if you are unhappy with the default size. For reference, the default size is currently `14px`.

`suspendTabsUntilReady` (experimental): if set to `true`, uBO will hard block all network requests when the browser launches until _all_ the filter lists and rules are loaded and ready, at which time uBO will force a reload of the tabs for which there were network requests blocked during the setup phase.