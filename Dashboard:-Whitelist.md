- Back to [Wiki home](https://github.com/gorhill/uBlock/wiki)
- Back to [Dashboard](https://github.com/gorhill/uBlock/wiki/Dashboard)

***

The _Whitelist_ pane lists all the _whitelist directives_. The purpose of a whitelist directive is to tell on which page uBlock Origin ("uBO") should disable itself completely. When uBO is disabled on a page, there will be no filtering applied to that page.

When uBO is disabled for a site, its toolbar icon will be grayed, and the large blue "power" button in the popup panel is dimmed.

When you visit a web page, uBO will try to match the URL of the page in the address bar against the existing whitelist directives. When there is a match, uBO will be disabled for that page.

The easiest way to create a whitelist directive is by toggling the large "power" button in uBO's popup panel -- this will cause a site-wide whitelist directive for the current site to be automatically created and added to the _Whitelist_ pane.

The _Whitelist_ pane allows you to review or edit the exisiting whitelist directives, or to manually add new ones.

**Important:** there are predefined whitelist directives when you first install uBO. You should not remove these predefined whitelist directives, unless you know _exactly_ the consequences of doing so. Removing the predefined whitelist directives without understanding the consequences could cause your browser to malfunction. This is especially true for the `behind-the-scene` whitelist directive.

Further details about the supported syntax for whitelist directives can be found at ["How to whitelist a web site"](https://github.com/gorhill/uBlock/wiki/How-to-whitelist-a-web-site).