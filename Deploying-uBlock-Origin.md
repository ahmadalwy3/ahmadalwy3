I do not know much about that administrator stuff, so I will let a knowledgeable person guide you:
- [Managing Google Chrome with adblocking and security](https://decentsecurity.com/enterprise/#/ublock-for-google-chrome-deployment/) by [SwiftOnSecurity](https://twitter.com/SwiftOnSecurity/status/783348579943317504)
- [Deploying uBlock Origin for Firefox with CCK2 and Group Policy](https://decentsecurity.com/enterprise/#/ublock-for-firefox-deployment/) by [SwiftOnSecurity](https://twitter.com/SwiftOnSecurity/status/783348579943317504)

### Customizing the settings

Administrators can force specific configurations to deployed uBlock Origin ("uBO"). At launch time, uBO will look for a setting named `adminSettings`, and if it exists, it will parse, extract and overwrite a user's settings with the administrator-assigned ones.

For Firefox, the `adminSettings` entry must be added to `about:config`, the key name is `extensions.ublock0.adminSettings`, and the value is a plain string -- which must be JSON-parseable.

For Chrome, `adminSettings` must be an entry part of the policy for the extensions. See <http://www.chromium.org/administrators/configuring-policy-for-extensions>.

This is still a work in progress, there are limitations. For example, it is not possible to merge an admin's settings with the user's ones -- a setting can only be overwritten. Hopefully I will address this limitation eventually, as time permit. (See https://github.com/gorhill/uBlock/issues/832#issuecomment-248138558).

The content of `adminSettings` is pretty straightforward: configure uBO as you wish for your users, then create a backup using the _"Backup to file"_ in the _Settings_ pane. Now open this backup file using a text editor, and remove all entries you do not want to overwrite, while taking care to end up with a valid JSON file (mind trailing commas, etc.). All the entries left are the ones which will be overwritten on the user's side.

An example, I created a backup file after having customized uBO, and removed everything except for the _"Color-blind friendly"_ setting, to force that setting to be set on the user's side. Resulting text file:

    {
      "userSettings": {
        "colorBlindFriendly": true
      }
    }

Now, the value for `adminSettings` must itself be a plain string, and this means we need to encode the above text into a string, using `JSON.stringify`. Here is a small utility to help you deal with this step: <http://raymondhill.net/ublock/adminSetting.html>.

### Further readings

Here are issues related to the customization of settings for deployed uBO, there might be advises in there which you may find useful:
- https://github.com/gorhill/uBlock/issues/832
- https://github.com/gorhill/uBlock/issues/531