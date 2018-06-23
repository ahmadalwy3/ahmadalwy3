[Back to _Dynamic-filtering_](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering)

***

The ability to turned off uBlock everywhere has been requested many times: [#40](https://github.com/gorhill/uBlock/issues/40), [#403](https://github.com/gorhill/uBlock/issues/403).

I wasn't really planning to provide this functionality as I fail to see why it should be implemented in uBlock when the browsers themselves offer this ability through the disabling of extensions.

In any case, the ability to "disable" uBlock everywhere is now available, as a side effect of the ability to create a global `allow` rule for all network requests:

![Allow everything everywhere](https://vgy.me/5eUSeO.png)

Though it's more _"allow everything from everywhere"_, it's as good as _"globally turn off uBlock"_. You can revert it by clicking on the eraser button.

Keep in mind:
 - [dynamic rule precedence logic](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering:-precedence), which means that the above will work as expected as long as you do not have existing higher precedence rules which override with the global _allow-all_ rule.
 - cosmetic filtering will still apply, so you may also want to [disable cosmetic filtering everywhere by default](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-cosmetic-filtering).