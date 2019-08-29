Dynamic filtering, introduced in version 0.7.0.0, allows a user to filter dynamically certain classes of requests on a 1st- and 3rd-party basis. Currently, `script` and `iframe` objects can be dynamically filtered, i.e. filtered on or off without having to create a custom filter.

This feature is not suited for users who like an install-and-forget blocker. Thus it is tucked away by default, and all dynamic filters are turned off by default.

**DO NOT USE IF YOU DO NOT UNDERSTAND HOW IT WORKS AND WHAT IT DOES.**

Dynamic filtering is targeted toward users who wish to have that additional bit of control about where their browser is allowed to connect and what it is allowed to execute, see it as a _extremely_ simplified (yet useful) _NoScript_ or [_µMatrix_](https://github.com/gorhill/uMatrix).

Dynamic filtering is a useful feature security-wise. For example, blocking 3rd-party `<iframe>` by default would have protected users in the case of the [jQuery.com malware attack](http://www.riskiq.com/resources/blog/jquerycom-malware-attack-puts-privileged-enterprise-it-accounts-risk). Disabling inline javascript is also often useful to work around anti-blockers on some sites. Using dynamic filtering can help speed up _significantly_ how fast web pages load.

See [examples of usefulness/benefits](./Dynamic-filtering---examples) of using dynamic filtering.

Of course, blocking portion of a page may cause page breakage, sometimes benign, sometimes severe. It is up to the user to choose how to make use of this feature.

![Figure 1](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/dynamic-filtering-1.png)

The "default" row above refers to the default settings to use for any web site. These default settings will take effect on all sites **unless** there are specific settings for the current site, which specific settings appear in the row above.

Columns:

1. to block inline `<script>` tags, i.e. javascript code which is embedded directly in the main document.
2. to block 1st-party `<script>` tags.
3. to block 3rd-party `<script>` tags.
4. to block 1st-party `<iframe>` tags.
5. to block 3rd-party `<iframe>` tags.

Whether a request is "1st-party" or "3rd-party" to a page is derived from the domain names extracted from the URL address of the net request and the URL address of the page: they have to be the same. So `www.arstechnica.com` is 1st-party to `arstechnica.com`, while `arstechnica.net` is 3rd-party to `arstechnica.com`. Domain names are extracted as per [Mozilla's Public Suffix List](https://publicsuffix.org/).

![Figure 2](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/dynamic-filtering-2.png)

Color scheme:

- Reddish indicates dynamic filtering in effect.
- Grayish indicates no dynamic filtering in effect.
- Darker red indicates dynamic filtering in effect, bypass default setting.
- Darker gray indicates no dynamic filtering in effect, bypass default setting.

So in the illustration above we have:

- Default settings:
    - Do not block inline `<script>` tags
    - Do not block 1st-party `<script>` tags
    - Block 3rd-party `<script>` tags
    - Do not block 1st-party `<iframe>` tags
    - Block 3rd-party `<iframe>` tags

- Site-specific settings:
    - Block inline `<script>` tags
    - Do not block 3rd-party `<script>` tags

The user interface is not terribly self-explanatory, but I really want to keep it as uncluttered as possible. Once you read the doc here, using dynamic filtering should require no further explanation.

Network requests blocked through dynamic filtering will be reported just as any other in the request log:

![Figure 3](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/dynamic-filtering-3.png)

Dynamic filters are always deemed [important](./Filter-syntax-extensions#network-filters), thus they will show up with the `important` filter option attached to them. When a network request is blocked because of a dynamic filtering default setting, the hostname will be reported as `*`, as seen in the picture above.
