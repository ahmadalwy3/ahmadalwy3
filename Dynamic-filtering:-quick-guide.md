[Back to _Dynamic-filtering_](./Dynamic-filtering)

***

Dynamic filtering pane ([available only to advanced users](./Advanced-user-features)) can be toggled off/on by clicking on the _Less_/_More_ buttons:

![figure 1](https://user-images.githubusercontent.com/585534/87428135-e16a2500-c5af-11ea-90a5-683ab79bffe5.png)

> ***
> **Important:**
>
> _Static filtering_ refers to the filters which comes from the filter lists, i.e. _EasyList_, _EasyPrivacy_, hpHosts, etc. _Dynamic filtering_ are those filtering rules which have an air of firewall rules. 
> ***

**First column**: what is to be dynamically filtered:

![figure 2](https://user-images.githubusercontent.com/585534/87428140-e4651580-c5af-11ea-9159-d4e82e4f68a7.png)

As you can see, you can create dynamic filtering rules for resource types, or hostnames according to their origin.

The color of an entry indicates whether all requests were blocked (reddish), all requests were allowed (greenish), or some were blocked some were allowed (yellowish).

In bold, domain names. Domain names are hostnames, but hostnames are not necessarily domain names from uBlock's point of view: domain names are extracted as per [Mozilla Public Suffix list](https://publicsuffix.org/).

**Second column**: **_global_** dynamic filtering rules, i.e. whatever rule appears in this column applies everywhere, on _all_ sites:

![figure 3](https://user-images.githubusercontent.com/585534/87428314-2a21de00-c5b0-11ea-89a3-f3da2026c58a.png)

**Third column**: **_local_** dynamic filtering rules, i.e. whatever rule appears in this column applies to the _current_ site only:

![figure 4](https://user-images.githubusercontent.com/585534/87428455-5a697c80-c5b0-11ea-9b5c-6c0517c4001a.png)

The cells in the third column gives an overview of how many requests were blocked/allowed:

- `-` or `+` = between 1-9 network requests were blocked or allowed, respectively
- `--` or `++` = between 10-99 network requests were blocked or allowed, respectively
- `---` or `+++` = 100 or more network requests were blocked or allowed, respectively
- blank cell = no network requests occurred for the specific hostname

So there are **global** dynamic filtering rules, and **local** dynamic filtering rules.

By default, there are no dynamic filtering rules at install time, so nothing is blocked by default by the dynamic filtering engine. You will have to create your own rules, according to your own prerogatives.

Sensible security- and privacy-wise: blocking all 3rd-party frames by default everywhere: 

![figure 5](https://user-images.githubusercontent.com/585534/87428834-ebd8ee80-c5b0-11ea-9670-85a349a3b347.png)

> ***
> **Important:**
>
> _Dynamic filtering_ overrides _static filtering_.
> 
> This means a _block_ dynamic rule will override any existing _allow_ static filters. This means you can block with 100% certainty using dynamic filtering rules. Similarly, an _allow_ dynamic filtering rule will override any existing _block_ static filters, i.e. you can allow with 100% certainty with dynamic filtering (useful to un-break sites broken by some static filters).
> 
> This may help understand how static and dynamic filtering interact: [Overview of uBlock's network filtering engine](./Overview-of-uBlock's-network-filtering-engine).
> ***

All embedded 3rd-party frames were blocked on the page. Good. However it appears there was an embedded YouTube video in the article:

![figure 6](https://user-images.githubusercontent.com/585534/87426719-a23ad480-c5ad-11ea-90ca-17b0e99bc09c.png)

If you want to block all 3rd-party frames by default, except for embedded YouTube videos on that particular site, two solutions.

##### First solution

Create a local  _noop_ rule for 3rd-party frames:

![figure 7](https://user-images.githubusercontent.com/585534/87426722-a4049800-c5ad-11ea-95f7-72b16d615051.png)

It works, the embedded YouTube video can now be played.

Note that a cell with a _noop_ rule is dark gray, while a cell with no rule at all is light gray (the default color). Hence gray means that no dynamic filtering will be applied to a cell. If a cell inherit a _block_ or _allow_ rule from a higher precedence cell, a _noop_ rule can be used to override the inherited _block_ or _allow_ rule. Conceptually, the purpose of _noop_ rules is to punch holes in your dynamic filtering ruleset so that network requests can pass through unimpeded.

However the above rule would result in all 3rd-party frames on the site to be unblocked. Not so good.

##### Second solution

Create a local _noop_ rule for `youtube.com` (and for the specific page used as example, a _noop_ rule for `google.com` also had to be created to un-break the embedded Youtube video):

![figure 8](https://user-images.githubusercontent.com/585534/87427192-68b69900-c5ae-11ea-9ffb-7ed5ff7bbc5b.png)

This will prevent dynamic filtering rules to apply to network requests to `youtube.com`, but only for the current site.

> ***
> **Important:**
>
> Remember that _noop_ rules bypass **only** broader dynamic filtering rules, static filtering is left completely intact, which means you won't see ads in the embedded YouTube videos.
> ***

What if you want to block 3rd-party frames everywhere by default, but want whatever embedded YouTube video to not be blocked by default on any site?

It is just a matter of creating a global _noop_ rule for `youtube.com`:

![figure 9](https://user-images.githubusercontent.com/585534/87427638-19249d00-c5af-11ea-9251-8a301d639958.png)

Which means: do not apply any dynamically filtering rule to `youtube.com` by default (i.e. everywhere).

> ***
> **Important:**
>
>  _Local_ dynamic filtering rules override _global_ ones.
> 
> In other words: **More specific dynamic filtering rules override less specific ones.** For example, dynamic filtering rules for `youtube.com` (specific) override dynamic filtering rules for `3rd-party frames` (generic).
> ***

All dynamic rules are temporary by default: Click the padlock if you want to persist the ruleset for a specific web site.

![figure 12](https://user-images.githubusercontent.com/585534/87427871-702a7200-c5af-11ea-8483-2275412a891b.png)

- The padlock will be visible **if and only if** there is at least one temporary rule in the pane
- This is really the optimal way to use dynamic filtering, as using this feature is often a matter of trial and error
- This prevents ruleset pollution: your ruleset will be only those rules which you will have explicitly persisted
- If you <kbd>Ctrl</kbd>-click to set/unset a rule, it will be immediately persisted (<kbd>command ⌘</kbd>-click on Mac)

***

We covered the _block_ and _noop_ dynamic filtering rules. What about the _allow_ rule?

The dynamic filtering _allow_ (green) rule is most useful to un-break sites broken by some static filters: **_allow_ rules will override all block filters from static filter lists**, and because of this, _allow_ rules are to be used only for exceptional cases and are rarely needed in the real world.

The only way to enable the ability to point-and-click to create _allow_ rules is to either:

- Tap twice on the <kbd>Ctrl</kbd> key while in the popup panel
- Set `filterAuthorMode` to `true` in [advanced settings](./Advanced-settings)

Doing so will enable the _allow_ rule creation widget in the popup panel:

![figure 10](https://user-images.githubusercontent.com/585534/87429361-a963e180-c5b1-11ea-9a21-1fdff36fb4ba.png)

This small obstacle to easily create _allow_ rule through point-and-click is [by design](https://github.com/gorhill/uBlock/releases/tag/1.28.0), as it has been found over the years that too many users are misusing dynamic filtering by creating _allow_ rules where _noop_ rules should have been used.

To reiterate, creating _allow_ rules will completely override related block filters from static filter lists, which may easily cause you to be less protected than if not using dynamic filtering at all -- _allow_ rules are to be used exceptionally, and most of the time, temporarily -- they are typically most useful to filter list maintainers in order to quickly narrow down filter issues.

Furthermore, when an _allow_ rule is set for the 1st-party domain, this will completely disable scriptlet injection and HTML filtering, again a behavior which is most useful to filter list maintainers. Scriptlet injection and HTML filtering are often used to deal with anti-blocker mechanisms.

> ***
> **Important:**
>
> Typically, use only narrow _allow_ dynamic filtering rules to un-break sites. As these _allow_ rules override any static filtering, this means if you use a too broad _allow_ dynamic filtering rule you could start to allow in ads/trackers/annoyances.
> ***

More: [Take control of your privacy in your own hands](https://github.com/chrisaljoudi/uBlock/issues/433#issuecomment-68488686) (will move this here eventually, I need a break)
