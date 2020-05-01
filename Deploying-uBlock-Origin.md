I do not know much about that administrator stuff, so I will let a knowledgeable person guide you:
- [Managing Google Chrome with adblocking and security](https://decentsecurity.com/enterprise/#/ublock-for-google-chrome-deployment/) by [SwiftOnSecurity](https://twitter.com/SwiftOnSecurity/status/783348579943317504)
- [Deploy Firefox in the Enterprise with uBlock Origin, HTTPS Everywhere and Privacy Badger using Group Policy](https://www.winsysadminblog.com/2019/03/deploy-firefox-in-the-enterprise-with-ublock-origin-https-everywhere-and-privacy-badger-using-group-policy/) by [John](https://www.winsysadminblog.com/about-me/)
- [How To Deploy AdBlocker for Enterprise](https://www.secjuice.com/how-to-deploy-adblocker-for-smbs/) by [Secjustice](https://twitter.com/secjuice)

### Customizing the settings

Administrators can force specific configurations to deployed uBlock Origin ("uBO"). At launch time, uBO will look for a setting named `adminSettings`, and if it exists, it will parse, extract and overwrite a user's settings with the administrator-assigned ones.

For **Firefox**, refer to Mozilla documentation about ["Native manifests"](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Native_manifests) (sections about ["Managed storage manifests"](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Native_manifests#Managed_storage_manifests) and [its location](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Native_manifests#Manifest_location)). You can also consult [this specific comment](https://github.com/gorhill/uBlock/issues/2986#issuecomment-364035002) in uBO issue tracker.

For **Firefox-legacy**, the `adminSettings` entry must be added to `about:config`, the key name is `extensions.ublock0.adminSettings`, and the value is a plain string -- which must be JSON-parseable.

For **Chrome**, `adminSettings` must be an entry part of the policy for the extension. See <http://www.chromium.org/administrators/configuring-policy-for-extensions>.

This is still a work in progress, there are limitations. For example, it is not possible to merge an admin's settings with the user's ones -- a setting can only be overwritten. Hopefully I will address this limitation eventually, as time permit. (See https://github.com/gorhill/uBlock/issues/832#issuecomment-248138558).

The content of `adminSettings` is pretty straightforward: configure uBO as you wish for your users, then create a backup using the _"Backup to file"_ in the _Settings_ pane. Now open this backup file using a text editor, and remove all entries you do not want to overwrite, while taking care to end up with a valid JSON file (mind trailing commas, etc.). All the entries left are the ones which will be overwritten on the user's side.

An example, I created a backup file after having customized uBO, and removed everything except for the _"Color-blind friendly"_ setting, to force that setting to be set on the user's side. Resulting text file:

    {
      "userSettings": {
        "colorBlindFriendly": true
      }
    }

Now, the value for `adminSettings` must itself be a plain string, and this means we need to encode the above text into a string, using `JSON.stringify`. Here is a small utility to help you deal with this step: <http://raymondhill.net/ublock/adminSetting.html>.


### Modifying the list of stock assets

Content of the "Filter lists" tab can be configured by providing custom version of the [`assets.json`](https://github.com/gorhill/uBlock/blob/16a0ebbfb05c4582ecc68454ba3b45b403164dde/assets/assets.json) file.

URL of the modified `assets.json` file must be added in `assetsBootstrapLocation` key.

Implementation, see: [#2314](https://github.com/gorhill/uBlock/pull/2314)

### Further readings

Here are issues related to the customization of settings for deployed uBO, there might be advises in there which you may find useful:
- https://github.com/gorhill/uBlock/issues/832
- https://github.com/gorhill/uBlock/issues/531
- https://github.com/gorhill/uBlock/issues/2986#issuecomment-333198882