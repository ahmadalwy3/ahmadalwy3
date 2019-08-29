You can manually edit rules for per-site switches in the _"My rules"_ pane in the dashboard.

There are no temporary vs. permanent settings for the [per-site switches](./Quick-guide:-popup-user-interface#the-site-based-switches), any change to one or more switches will be immediately reflected in the permanent settings.

There are currently three per-site switches supported:

- `no-popups`: To block **all** popups.
- `no-strict-blocking`: To disable strict blocking.
- `no-cosmetic-filtering`: To disable cosmetic filtering.

When toggled through the popup UI, these switches will apply only to the current web site. However you can edit them manually using the _"My rules"_ pane in the dashboard.

The syntax is as follow:

    switch-name: hostname state

The switch name must be followed by a column `:`, a space, then the hostname on which the switch must apply. Use `*` as a hostname placeholder to indicate you want the switch to apply everywhere. Following is the state of the switch, which can be `on` or `off` (`true` or `false` are also valid).

When switches share a common hostname ancestor, the most specific wins. For example, if you have:

    no-popups: example.com on
    no-popups: www.example.com off

and you visit `www.example.com`, the "no popups" switch will be turned off (popup allowed unless blocked by a static filter).

All switches are `off` by default, meaning there is no point in creating an entry such as:

    no-popups: www.example.com off

Unless it is to override a related broader entry for which the switch is `on`.

### Caveats

- Chromium-based browsers: If you block popups everywhere by default (`no-popups: * true`), this will break _"Open link in new tab"_ in the context menu. This is because of Chrome API limitations.
