[Back to _Blocking mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode)

***

Roughly similar to using Adblock Plus with many filter lists + NoScript with 1st-party scripts/frames automatically whitelisted + RequestPolicy with 1st-party resources automatically whitelisted.

Blocking-wise, this is a small leap from [medium mode](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-medium-mode). This mode will however lead to a higher likelihood of broken web sites, and thus will likely require intervention the first time you visit a site, since even passive 3rd-party resources (i.e. images, css) are blocked with this mode.

This mode will block all 3rd parties by default, so it keeps privacy exposure to 3rd parties to a minimum.

![3rd-party network requests are blocked by default](https://cloud.githubusercontent.com/assets/585534/9021738/3d1e42cc-3821-11e5-82be-f236e5fb8ca3.png)<br>
<sup>3rd-party network requests are blocked by default.</sup>

With a single click, it is possible to toggle the hard mode into the [medium mode](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-medium-mode): it's just a matter of assigning a local noop rule to the _3rd-party_ cell.

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
- All of uBlock origin's custom filter lists: checked
- _EasyList_: checked
- _Peter Lowe’s Ad server list_: checked
- _EasyPrivacy_: checked
- _Malware Domain List‎_: checked
- _Malware domains_: checked
- All other filter lists: unchecked

_My rules_ pane:
- Add `* * 3p block`
- Add `* * 3p-script block`
- Add `* * 3p-frame block`

##### Tips

With few clicks, you can easily fall back into lesser blocking modes, if ever you do not have the willingness to figure the necessary rules for a given site.

Fall back into [medium mode](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-medium-mode) for the current site:
- set a local noop rule for the _3rd-party_ cell.

Fall back into [easy mode](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-easy-mode) for the current site:
- set a local noop rule for the _3rd-party_ cell.
- set a local noop rule for the _3rd-party script_ cell.
- Optionally, set a local noop rule for the _3rd-party frames_ cell.
