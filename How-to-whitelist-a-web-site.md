I've read a couple of feedbacks of people who wish it was possible to whitelist a web site, i.e. to disable uBlock on a specific web site.

The feature is already available: it is the big power button.  It serves to whitelist the current web site, and its state will be remembered next time you visit the web site.

![uBlock's popup](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1.png)

### Detailed syntax

All whitelist directives are matched against the URL address of web pages.

As of version uBlock 0.8.2.0, the whitelist directive syntax is split into three classes:
- Plain
- Complex
- Comment

Plain syntax is when using only hostname label(s), which means only the hostname portion of a URL will be taken into account.  With plain syntax, the matching is performed by comparing the right-most portion of the page hostname with the whitelist directive.  Wildcards are not allowed when using plain syntax.

Complex syntax occurs if and only if at least one `/` appears in a whitelist directive.  Optionally, the wildcard `*` can be used with complex directives for more flexibility.

A comment is a line prefixed with `#`.  Comments are ignored by uBlock.

If no `/` appears in a whitelist directive, and if the directive contains characters which are not allowed for a plain hostname, then the whitelist directive will be commented out and ignored by uBlock.  This allows you to fix your directive.

#### Plain hostname

- `example.com`: whitelist all pages from `example.com` or above (i.e. `example.com`, `www.example.com`).
- `www.example.org`: whitelist all pages from `www.example.org` or above (i.e. `www.example.org`, `forums.www.example.org`, but not `example.org`).
- `org`: whitelist all pages from TLD `org` (i.e. `example.org`, `wikipedia.org`).

#### Single web page

- `http://www.twitch.tv/letofski`: whitelist only this one page, i.e. when the URL in the address bar **matches exactly** `http://www.twitch.tv/letofski`.

#### Section of a web site

 - `http://www.twitch.tv/letofski*`: whitelist this one page, and everything underneath, i.e. when the URL in the address bar **starts exactly** with `http://www.twitch.tv/letofski`.

#### Specific pattern

- `*reddit.com/r/privacy/*`

Wildcards can be used at any position. However, when a wildcard is used within the hostname portion of a directive, it cannot be at the end of the hostname, and also must be at the boundary of a hostname label.

#### Regular expression (1.9.17+)

- `/^https?://192\.168\.0\.\d+//`
- `/^https://[0-9a-z-]+//`

When you are facing a case where no other directive syntax work, you may use a regular expression ("regex") as a last resort solution. When a whitelist directive starts and ends with a forward slash (`/`), uBO will treat the directive as a regex-based one.

Given that whitelist directives dictate where uBO should be completely disabled, be very careful with regex-based directives, you could easily mistakenly cause uBO to be disabled on more sites than you intended. Typically, only advanced users will resort to regex-based directives, and only for cases where no other syntax can do the job.

### A Youtube channel

There are user scripts on [Greasy Fork](https://greasyfork.org/), for example: [YouTube - whitelist channels in uBlock Origin](https://greasyfork.org/en/scripts/22308-youtube-whitelist-channels-in-ublock-origin). I can't vouch for the scripts, you will have to find out yourself whether they work.

Someone posted instructions on reddit: [Any way to whitelist certain youtube channels?](https://www.reddit.com/r/ublock/comments/4x4jol/any_way_to_whitelist_certain_youtube_channels/).

### Other details

If you re-enable uBlock by clicking the whitelist button in the popup while a whitelist directive you handcrafted is in effect, your handcrafted whitelist directive will simply be commented out. This way you can bring it back to life if ever you un-whitelist by mistake.