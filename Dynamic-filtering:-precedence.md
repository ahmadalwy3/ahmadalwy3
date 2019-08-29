[Back to "Dynamic-filtering"](./Dynamic-filtering)

***

First: Whitelist directives override both dynamic filtering _and_ static filtering. Whitelist directives appear in the [_Whitelist_ pane in the dashboard](./How-to-whitelist-a-web-site), and they are used to completely disable filtering. The [big blue button in the popup UI](./Quick-guide:-popup-user-interface#the-large-power-button) is used to easily whitelist the current site/page.

***

Dynamic `allow`/`block` rules override static filtering rules.
- Use `allow` to force requests to be allowed regardless of whether they would normally be blocked by static filtering.
    - Useful to fix sites broken by false positives in _EasyList_, _EasyPrivacy_ (or any other static filter lists).
- Use `block` to force requests to be blocked regardless of whether they would normally be allowed by static filtering.
    - Useful to block with 100% certainty, to bypass exception filters with which you may disagree in _EasyList_, _EasyPrivacy_ (or any other static filter lists).

There is a precedence logic for dynamic filtering cells:

Local rules override global rules.
- Local setting for `example.com` override global setting for `example.com`.

The party-specific cells override the type-specific cells.
- `3rd-party` override `images`
- `example.com` override `images`

The more specific the party, the higher the precedence.
- `example.com` overrides `3rd-party scripts`
- `www.example.com` overrides `example.com`

Party-specific and type-specific cells override non specific party cells:
- `3rd-party frames` overrides `3rd-party`

All cells override the `all` cells. The local `all` cell overrides the global `all` cell.

The UI is designed in such way that the precedence logic should quickly become obvious with usage.
