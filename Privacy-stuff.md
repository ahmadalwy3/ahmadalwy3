##### Settings

Unlike uMatrix, uBlock can't foil cookie headers. For privacy-minded users it is strongly suggested to...

- Enable _"Block third-party cookies and site data"_ in _"Content settings"_ / _"Cookies"_.
    - It works very well: see "Outbound cookies" in [this benchmark results](https://github.com/gorhill/uBlock/wiki/%C2%B5Block-and-others:-Blocking-ads,-trackers,-malwares).
    - But this may break some sites. For instance, you won't be able to enter comments on Youtube.
    - Useful to know: the block also applies to local storages, not just cookies.
- Enable _"Click to play"_ in _"Content settings"_ / _"Plug-ins"_.
- Disable _"Predict network actions to improve page load performance"_, as this causes DNS queries to be made even for blocked network requests (see issue #232).

##### Command line switches

These command line switches might be of interest to privacy-minded users:

- `--disable-component-extensions-with-background-pages`
    - _"Disable default component extensions with background pages"_ ([ref](http://peter.sh/experiments/chromium-command-line-switches/#disable-component-extensions-with-background-pages))
    - This seems to prevent Hangout Services to be launched by the browser as a background process. Even in Chromium there is [such a process](https://code.google.com/p/chromium/codesearch#chromium/src/chrome/browser/resources/hangout_services/background.html) launched even if you do not use Google's _Hangout_.
    - With other Chromium-based browsers, maybe more stuff would be disabled, you decide whether this is good or bad.
- `--disable-background-networking`
    - _"Disable several subsystems which run network requests in the background"_ ([ref](http://peter.sh/experiments/chromium-command-line-switches/#disable-background-networking))
- [add more switch of interests whenever new ones are found]

Another powerful command line switch is:

- `--host-rules="MAP *.google-analytics.com 0.0.0.0","MAP *.googleadservices.com 0.0.0.0","MAP *.doubleclick.net 0.0.0.0","MAP *.googletagservices.com 0.0.0.0"`
    - This switch maps those hostnames (or any other ones) to the IP address 0.0.0.0 ([ref](http://peter.sh/experiments/chromium-command-line-switches/#host-rules)) and hence blocks them effectively (even on the Chrome webstore where extensions like uBlock are disabled). 
    - _However, note that blocking those hostnames with that switch might break some websites. That's why blocking them with uMatrix is preferable since you can whitelist them as exceptions for those websites which won't work without them. Alternatively, you could use the `important` filter option mentioned below._

##### Regarding EasyPrivacy

In case you were not aware, using _EasyPrivacy_ doesn't protect completely against Google Analytics. So if you were using Adblock Plus with _EasyPrivacy_ (as [recommended by the EFF](https://www.eff.org/deeplinks/2012/04/4-simple-changes-protect-your-privacy-online)), you might have thought you were protected against Google Analytics. This is not necessarily the case.

If you are using uBlock, it protects you *more* against Google Analytics out of the box -- via _"Peter Lowe's Ad server"_ list. Yet, given that an exception filter may exist somewhere in one of the many lists, blocking Google Analytics (or similarly ubiquitous hostnames) is not possible with preset filter lists.

##### Overriding exception filters

However, in [uBlock 0.5.5.0](https://github.com/gorhill/uBlock/releases/tag/0.5.5.0) a new filter option `important` was introduced with the consequence that corresponding exception rules are ignored. Example: Adding

    ||google-analytics.com^$important

to _"Your filters"_ blocks Google Analytics regardless of existing exception rules. You can restrict this rule to specific domains like

    ||google-analytics.com^$important,domain=example1.com|example2.com

Or to all third-parties:

    ||facebook.com^$important,third-party
    ||linkedin.com^$important,third-party

##### Twitter widget

It's unclear why this one is not blocked by Fanboy Annoyance, as the list already blocks many other twitter widget-related stuff. So if you use above list, you may want to add the following to your filters:

`||platform.twitter.com/widgets.js$third-party`

##### Gravatar (et al)

Each time you visit a site which pull cute little avatar images aside (typically) a commenter's name, there is a corresponding request to [Gravatar](https://gravatar.com)'s web site, and the HTTP `referer` header contains the site you are visiting. The tracking potential is too much for me, so I block all these requests:

`||gravatar.com^$third-party`

It's unclear if, and how much this breaks things. But will prevent your browsing habits to be disclosed to gravatar.com. We can live without these cute thumbnails, can't we?

But this applies to any domain which is ubiquitous enough, `gravatar.com` is just one example among so many. 

To deal with this easily, [uMatrix](https://github.com/gorhill/uMatrix) is the best tool, as to blacklist a ubiquitous domain with 100% certainty is simply a matter of point and click.