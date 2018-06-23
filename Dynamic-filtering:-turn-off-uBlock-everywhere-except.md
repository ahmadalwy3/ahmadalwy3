[Back to "Dynamic-filtering"](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering)

***

"Blacklist mode" can be achieved in UBO [Advanced users](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) mode in following way:

- global allow `all` cell
    - "global" = 1st column
    - "allow" = green

![allow all](https://vgy.me/WyvT5C.png)

Nothing will be blocked, static filtering is completely bypassed: "green" means "allow unconditionally".

To "blacklist" a specific site:

- local noop `all` cell
    - "local" = 2nd column
    - "noop" = dark gray

This will cause the current site to become subjected to static filtering (EasyList, EasyPrivacy etc, i.e. whatever filter lists is in effect).

![block here](https://vgy.me/SnYE6y.png)

Dynamic filtering disengaged for current site: "gray" means disengage dynamic filtering, but apply static filtering.

Keep in mind cosmetic filtering will still apply, so you may also want to [disable cosmetic filtering everywhere by default](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-cosmetic-filtering).

In the screenshots above, 3rd-party frames are blocked to remind this is [a good habit in general](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering:-Benefits-of-blocking-3rd-party-iframe-tags), and to illustrate that narrower dynamic rules prevails over more generic ones.