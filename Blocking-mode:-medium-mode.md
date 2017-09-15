[Back to _Blocking mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode)

***

Roughly similar to using Adblock Plus with many filter lists + NoScript with 1st-party scripts/frames automatically whitelisted. Unlike NoScript however, you can easily point-and-click to block/allow scripts _on a per-site basis_.

Blocking-wise, this is one significant leap from [easy mode](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-easy-mode). However, be ready to accept you will have to un-break web sites, though at a lesser rate than [hard mode](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-hard-mode), since passive 3rd-party resources (i.e. images, css) are not blocked in medium mode.

This is where you start to use [dynamic filtering](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering), a feature available only when you tell uBlock Origin that you are an [advanced user](https://github.com/gorhill/uBlock/wiki/Advanced-user-features). Be sure to read [the guide](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering) before, it is assumed that you understand well how dynamic filtering works in order to use effectively medium mode.

![3rd-party scripts are blocked by default](https://cloud.githubusercontent.com/assets/585534/9021740/41eac000-3821-11e5-9842-c4c6fea573c3.png)<br>
<sup>3rd-party scripts and frames are blocked by default.</sup>

Using medium mode will improve significantly your browser performance, and similarly reduce significantly your privacy exposure when compared to easy mode.

##### Characteristics

- Web pages will load significantly faster compared to the [_easy mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-easy-mode).
- Your privacy exposure will be significantly reduced compared to easy mode.
- You no longer depends mostly on 3rd-party filter lists to dictate what is blocked or not.
    - The static filter lists are still used to mop up whatever network requests is not blocked in this mode -- so double protection.
- High likelihood of web pages being broken: you have to be ready and willing to fix them when this happen.
    - Keep in mind though that as you build your ruleset for the sites you usually visit, you will spend less and less time fixing web pages.

##### How to enable this mode

_Settings_ pane:
- _I am an advanced user_: checked.

_3rd-party filters_ pane:
- All of uBlock Origin's filter lists: checked
- _EasyList_: checked
- _Peter Lowe’s Ad server list_: checked
- _EasyPrivacy_: checked
- _Malware Domain List‎_: checked
- _Malware domains_: checked
- All other filter lists: unchecked

_My rules_ pane:
- Add `* * 3p-script block`
- Add `* * 3p-frame block`

##### Tips

With one click or two, you can easily fall back into lesser blocking mode, if ever you do not have the willingness to figure the necessary rules for a given site.

To fall back into [easy mode](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-easy-mode):
- Set a local noop rule for the _3rd-party script_ cell:<br>
  ![3rd-party scripts allowed](https://cloud.githubusercontent.com/assets/585534/9775590/7777b176-571e-11e5-9647-12711e53df21.png)
- Set a local noop rule for the _3rd-party frames_ cell (optional, as blocking 3rd-party frames is less likely to break web sites):<br>
  ![3rd-party frames allowed](https://cloud.githubusercontent.com/assets/585534/9775665/ec770238-571e-11e5-9d63-a90e4e5d76ba.png)
- If you want the rules to stick, click the padlock to make them permanent.

Using local noop rules ensure that the resulting lesser blocking mode applies _only_ to the current site, so that medium mode is still enforced everywhere else.