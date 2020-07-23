[Back to "Dynamic-filtering"](./Dynamic-filtering)

***

"Blacklist mode" can be achieved in UBO [Advanced users](./Advanced-user-features) mode in following way:

- global allow `all` cell
    - "global" = 1st column
    - "allow" = green

![allow all](https://user-images.githubusercontent.com/886325/88310853-712a7480-cd10-11ea-994f-dde6862d62f7.png)
<br>After changes to [1.28.0](https://github.com/gorhill/uBlock/releases/tag/1.28.0) access to _allow_ rules is limited. Read [release notes](https://github.com/gorhill/uBlock/releases/tag/1.28.0) to learn how to make it available.

Nothing will be blocked, static filtering is completely bypassed: "green" means "allow unconditionally".

To "blacklist" a specific site:

- local noop `all` cell
    - "local" = 2nd column
    - "noop" = dark gray

This will cause the current site to become subjected to static filtering (EasyList, EasyPrivacy etc, i.e. whatever filter lists is in effect).

![block here](https://user-images.githubusercontent.com/886325/88309652-e7c67280-cd0e-11ea-8d5a-494ee83c29b5.png)

Dynamic filtering disengaged for current site: "gray" means disengage dynamic filtering, but apply static filtering.

Keep in mind cosmetic filtering will still apply, so you may also want to [disable cosmetic filtering everywhere by default](./Per-site-switches#no-cosmetic-filtering).

In the screenshots above, 3rd-party frames are blocked to remind this is [a good habit in general](./Dynamic-filtering:-Benefits-of-blocking-3rd-party-iframe-tags), and to illustrate that narrower dynamic rules prevails over more generic ones.
