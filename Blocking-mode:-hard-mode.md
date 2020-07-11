[Back to _Blocking mode_](./Blocking-mode)

***

Roughly similar to using Adblock Plus with many filter lists + NoScript with 1st-party scripts/frames automatically whitelisted + RequestPolicy with 1st-party resources automatically whitelisted.

Blocking-wise, this is a small leap from [medium mode](./Blocking-mode:-medium-mode). This mode will however lead to a higher likelihood of broken web sites, and thus will likely require intervention the first time you visit a site, since even passive 3rd-party resources (i.e. images, css) are blocked with this mode.

This mode will block all 3rd parties by default, so it keeps privacy exposure to 3rd parties to a minimum.

![3rd-party network requests are blocked by default](https://user-images.githubusercontent.com/585534/86542007-c298ce00-bedf-11ea-9d63-e2b424c6dc71.png)<br>
<sup>3rd-party network requests are blocked by default.</sup>

![red badge](https://user-images.githubusercontent.com/886325/64036700-1c0fce00-cb54-11e9-9fad-49f72c4fa086.png)
<br>Starting with [v1.21.7b5](https://github.com/gorhill/uBlock/commit/7ff750eaf6007bdea4e843d3314fc7275b1ce945), a red badge on uBlock₀ toolbar button indicates activation of the hard mode.

With a single click, it is possible to toggle the hard mode into the [medium mode](./Blocking-mode:-medium-mode): it's just a matter of assigning a local noop rule to the _3rd-party_ cell.

##### Characteristics

- Web pages will load fast.
- Your privacy exposure to 3rd parties is reduced to a minimum.
- You no longer depend mostly on 3rd-party filter lists to dictate what is blocked or not.
    - The static filter lists are still used to mop up whatever network requests is not blocked in this mode -- so double protection.
- Very high likelihood of web pages being broken: you have to be ready and willing to fix them when this happen.
    - Keep in mind though that as you build your ruleset for the sites you usually visit, you will spend less and less time fixing web pages.

##### How to enable this mode

_Settings_ pane:
- _I am an advanced user_: checked.

_3rd-party filters_ pane:
- All of uBlock Origin's custom filter lists: checked
- _EasyList_: checked
- _Peter Lowe’s Ad server list_: checked
- _EasyPrivacy_: checked
- _Online Malicious URL Blocklist_: checked
- All other filter lists: unchecked

_My rules_ pane:
- Add `* * 3p block`
- Add `* * 3p-script block`
- Add `* * 3p-frame block`

##### Tips

With few clicks, you can easily fall back into lesser blocking modes, if ever you do not have the willingness to figure the necessary rules for a given site.

Fall back into [medium mode](./Blocking-mode:-medium-mode) for the current site:
- set a local noop rule for the _3rd-party_ cell.

Fall back into [easy mode](./Blocking-mode:-easy-mode) for the current site:
- set a local noop rule for the _3rd-party_ cell.
- set a local noop rule for the _3rd-party script_ cell.
- Optionally, set a local noop rule for the _3rd-party frames_ cell.
