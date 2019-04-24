Starting with version 0.2.0.0, you can find the change log and releases at this page:

<https://github.com/gorhill/uBlock/releases>

This is the proper Github-way to release new revisions/versions, and this simplifies my work. Thanks to [mikhaelkh](/mikhaelkh) for the [tip](/gorhill/httpswitchboard/issues/368).

### 0.1.4.8
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.8.zip) date: 10 July 2014
    - Sorry for the quick releases, I just want the contributors to be able to benefit from the results of their translation work.
- Swedish translation work from [contributor at Crowdin](https://crowdin.net/project/ublock/sv-SE/activity).
- Ukrainian translation work (partial) from [contributor at Crowdin](https://crowdin.net/project/ublock/uk/activity).

***

### 0.1.4.7
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.7.zip) date: 10 July 2014
- Brazilian Portuguese translation work from [contributor at Crowdin](https://crowdin.net/project/ublock/pt-BR/activity).
- Dutch translation work from [contributor at Crowdin](https://crowdin.net/project/ublock/nl/activity).
- Chinese translation work from [contributor on Github](/gorhill/uBlock/commit/8633ad3ad9cb9142eb9eadeb36f070bba87ecc05)

***

### 0.1.4.6
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.6.zip) date: 9 July 2014
- Dutch translation work (not complete) from [contributor at Crowdin](https://crowdin.net/project/ublock/nl/activity).
- Fixed <https://github.com/gorhill/uBlock/issues/51>: "Show the updated content of a list, not its content at install time".

***

### 0.1.4.5
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.5.zip) date: 9 July 2014
- Fixed <https://github.com/gorhill/uBlock/issues/50>: "Thepiratebay leaves behind blocked element divs".

***

### 0.1.4.4
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.4.zip) date: 8 July 2014
- Fixed <https://github.com/gorhill/uBlock/issues/49>: "Checkboxes in Settings tab not initialized properly".

***

### 0.1.4.3
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.3.zip) date: 8 July 2014
- [Performance work](/gorhill/uBlock/commit/c837f32fa728e73e6498a6395efb6acfcf9d1ac6): the handling of net requests went on average from above 220ms to under 180ms per net request (as per [reference benchmark](/gorhill/uBlock/wiki/Reference-benchmark)).

***

### 0.1.4.2
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.2.zip) date: 7 July 2014
- Fixed font family used to display requests in _Statistics_ tab.
- Now using `Number.toLocaleString` to display number of requests blocked since install.
    - As [suggested by a user on Wilders Securities Forums](http://www.wilderssecurity.com/threads/%C2%B5block-a-lean-and-fast-blocker.365273/page-4#post-2388950).
- This version was submitted to Opera web store.

***

### 0.1.4.1
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.1.zip) date: 7 July 2014
- Better layout for log of requests, emphasizing domains.
    - No open issue for this one. Changes in [069909117148e5e1bebf119dd532fd88e8dff1d6](https://github.com/gorhill/uBlock/commit/069909117148e5e1bebf119dd532fd88e8dff1d6).

***

### 0.1.4.0
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.4.0.zip) date: 6 July 2014
- **New settings:** _"Enable the logging of non-blocked requests"_
    - In the _Statistics_ tab in the dashboard.
    - Just like the other option to log blocked requests, except this one is to be able to see what was **not** blocked, along with the relevant exception filter it any.
    - Disabled by default.
    - Does not affect memory and CPU footprint if disabled.
    - Will likely increase a bit memory footprint when enabled (µBlock will still be quite below the memory footprint of big name blockers).
    - The logging opens the door to more advanced features if needed, like the disabling of specific filters, or to be able to easily create filters.
- Fixed <https://github.com/gorhill/uBlock/issues/47>: "Option to also log non-blocked requests".
- Fixed a few glitches which caused the blocking count to be reset constantly on Google Maps, and some others here and there, I didn't feel like opening an issue for each of these. Check [the commit](/gorhill/uBlock/commit/ee610b3aad679440da51da9449b345afda6f274d) if you are really that curious.

Also, I registered the [project at Crowdin](https://crowdin.net/project/ublock), so if you want to contribute translation work, that would be the place to do it. I'm learning how all this work, so I might have been clumsy when setting up the project, but it currently works, I might just decide to restructure the directory tree if I can do it without losing work (I thought it had to reflect the project's directory tree here at Github).

***

### 0.1.3.4
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.3.4.zip) date: 5 July 2014
- Fixed <https://github.com/gorhill/uBlock/issues/46>: "uBlock blocking behind the scene requests while it should not".
    - This was breaking the ability to log in a user's Google account from the browser's _Apps_ page (`chrome://apps`, or `chrome://chrome-signin`).

***

### 0.1.3.3
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.3.3.zip) date: 5 July 2014
- Fixed <https://github.com/gorhill/uBlock/issues/44>: "EasyList Czech and Slovak moved".
- Fixed <https://github.com/gorhill/uBlock/issues/41>: "Extremely generic element hiding selectors are current performance bottleneck".
    - Probably users won't notice this performance improvement, as the test case used was a demanding one:
        - Tested page, heavily bloated front page of [www.si.com](http://www.si.com) ([a demanding page](http://www.youtube.com/watch?v=1NmQvv7MGbE) for cosmetic filters)
        - I used many lists with cosmetic filters in them: _EasyList_, _EasyPrivacy_, _Fanboy Annoyance_, _Fanboy Enhanced Tracking_, _Fanboy Anti-Facebook_.
        - The improvement cuts µBlock's cosmetic filters implementation overhead from 90ms to 60ms per page load for that particularly demanding page (over 2,500 HTML elements), with the above lists (representing over 33,500 cosmetic filters).
        - So if µBlock can do well with this one page, it most certainly can do very well with almost everything else.

***

### 0.1.3.2
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.3.2.zip) date: 2 July 2014
- Translation [work](/gorhill/uBlock/commit/c1421d04236eca315c63704b2e4be9a1f55dd888) by [tlu1024](/tlu1024) (German)
- Fixed <https://github.com/gorhill/uBlock/issues/42>: "Filters using the `~example.com` syntax for the `domain=` option are broken".

***

### 0.1.3.1
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.3.1.zip) date: 2 July 2014
- Translation [work](/gorhill/uBlock/commit/a0a3f5b30b1abae610a14606b6cf3991487e4775) by [faye925](/faye925) (Chinese Simplified)
- Translation [work](/gorhill/uBlock/commit/bdcd1ceadad2fe45136a2fb0b419a798bbdf3214) by [tailHey](/tailHey) (French)

***

### 0.1.3.0
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.3.0.zip) date: 2 July 2014
- New _"Statistics"_ tab in the dashboard: to see which requests were blocked on a particular page.
    - Optional, disabled by default in order to prevent overhead such a feature introduce for users who will never care about this level of details.
    - If enabled, there will be a small eye icon in the popup to easily access the tab.
- Translation work by [Ginohax](/Ginohax) (Italian).
- Fixed <https://github.com/gorhill/uBlock/issues/37>: "Avoid avoidable overhead in contentscript_end.js ..."
- Fixed <https://github.com/gorhill/uBlock/issues/12>: "Possibility to view blocked elements + corresponding filters"

***

### 0.1.2.0
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.2.0.zip) date: 30 June 2014
- Translation work by [Ginohax](/Ginohax) (Italian).
- Added exception filters [to make hpHosts more usable](/gorhill/uBlock/issues/17).

***

### 0.1.1.1
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.1.1.zip) date: 29 June 2014
- Translation work by [tailHey](/tailHey) ([French](/gorhill/uBlock/commits?author=tailHey)) and [tlu1024](/tlu1024) ([German](https://github.com/gorhill/uBlock/commits?author=tlu1024)).
- Fixed <https://github.com/gorhill/uBlock/issues/33>: "Need translation of detailed description: German".
- Fixed <https://github.com/gorhill/uBlock/issues/28>: "Parse and enforce Adblock+ element hiding filters option not working properly".

***

### 0.1.1.0
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.1.0.zip) date: 27 June 2014
- **New setting:** In _"Settings"_ tab of the dashboard: _"Hide placeholders of blocked elements"_.
    - Check to prevent blocked images and frames to take space on the page.
- [Translation work](/gorhill/uBlock/pull/24) by [tlu1024](/tlu1024) (German)
- Fixed <https://github.com/gorhill/ublock/issues/25>: "Add the new Fanboy's "Anti-Facebook Filters".
- Fixed <https://github.com/gorhill/ublock/issues/7>: "Blocked contents don't always disappear properly".

***

### 0.1.0.11
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.11.zip) date: 27 June 2014
- Fixed <https://github.com/gorhill/ublock/issues/21>: "Have uBlock maintain its own list of filters to unbreak sites".
- Fixed <https://github.com/gorhill/ublock/issues/20>: "Cannot directly access forum on xda-developers.com from front page".

***

### 0.1.0.10
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.10.zip) date: 26 June 2014
- Fixed <https://github.com/gorhill/ublock/issues/18>: "Conflict with HTTPS Everywhere extension in Chrome".
    * In order to fix this, I had to reverse the partial solution put in place to fix [issue #7](/gorhill/uBlock/issues/7#issuecomment-47301344), "Blocked contents don't always disappear properly".
- [Fixed bad test](/gorhill/uBlock/commit/a6496e5cfb76d1a13d3ca8836cb21d5969b49ae7) in request handler.

***

### 0.1.0.9
- Release date: Not released yet
- Fixed <https://github.com/gorhill/ublock/issues/16>: "Changelog links wrong".
    * The link was right, problem was an issue with mixing jQuery's `$()` with `window.addEventListener('load', ...)`.

***

### 0.1.0.8
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.8.zip) date: 25 June 2014
- Fixed <https://github.com/gorhill/ublock/issues/14>: "Twitter glitches when using Fanboy’s Annoyance List".

***

### 0.1.0.7
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.7.zip) date: 25 June 2014
- Fixed <https://github.com/gorhill/ublock/issues/13>: "Google ads on Google.com".

***

### 0.1.0.6
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.6.zip) date: 24 June 2014
- Partially addressed <https://github.com/gorhill/ublock/issues/7> and <https://github.com/gorhill/ublock/issues/11>: Redirecting to no-op contents whenever possible.

***

### 0.1.0.5
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.5.zip) date: 24 June 2014
- Added a hint in the popup about the purpose of the power button. See <https://github.com/gorhill/uBlock/commit/225bc2d33c5743f0ce1394e2dac9aa0c37c14e48?

***

### 0.1.0.4
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.4.zip) date: 24 June 2014
- Fixed <https://github.com/gorhill/ublock/issues/1>: "It blocks playing music on soundcloud.com".

***

### 0.1.0.0
- [Release](/gorhill/ublock/blob/4de8f0fdeb6b539b18d92a3243bd2fc4dfb7e27c/dist/ublock_0.1.0.0.zip) date: 23 June 2014
- First release.