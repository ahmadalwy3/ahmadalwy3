[Back to _Blocking mode_](./Blocking-mode)

***

Roughly similar to using Adblock Plus with many filter lists + NoScript with 1st-party scripts/frames automatically whitelisted. Unlike NoScript however, you can easily point-and-click to block/allow scripts _on a per-site basis_.

Blocking-wise, this is one significant leap from [easy mode](./Blocking-mode:-easy-mode). However, be ready to accept that you will have to un-break websites, though at a lesser rate than [hard mode](./Blocking-mode:-hard-mode), since passive 3rd-party resources (i.e. images, css) are not blocked in medium mode.

This is where you start to use [dynamic filtering](./Dynamic-filtering), a feature available only when you tell uBlock Origin that you are an [advanced user](./Advanced-user-features). Be sure to read [the guide](./Dynamic-filtering) before, it is assumed that you understand well how dynamic filtering works in order to use medium mode effectively.

![3rd-party scripts are blocked by default](https://user-images.githubusercontent.com/585534/86541955-5c13b000-bedf-11ea-9e9c-30a1aff691a0.png)
<br>3rd-party scripts and frames are blocked by default.

![blue badge](https://user-images.githubusercontent.com/886325/64036718-229e4580-cb54-11e9-91d3-10b6d95b6068.png)
<br>Starting with [v1.21.7b5](https://github.com/gorhill/uBlock/commit/7ff750eaf6007bdea4e843d3314fc7275b1ce945), a blue badge on uBlock₀ toolbar button indicates activation of the medium mode.

Using medium mode will significantly improve your browser performance, and similarly significantly reduce your privacy exposure compared to easy mode.

##### Characteristics

- Web pages will load significantly faster compared to the [_easy mode_](./Blocking-mode:-easy-mode).
- Your privacy exposure will be significantly reduced compared to easy mode.
- You no longer depend mostly on 3rd-party filter lists to dictate what is blocked or not.
    - The static filter lists are still used to mop up whatever network requests are not blocked in this mode -- so double protection.
- High likelihood of web pages being broken: you have to be ready and willing to fix them when this happens.
    - Keep in mind though that as you build your ruleset for the sites you usually visit, you will spend less and less time fixing web pages.

##### How to enable this mode

_Settings_ pane:
- _I am an advanced user_: checked.

_3rd-party filters_ pane:
- All of uBlock Origin's filter lists: checked
- _EasyList_: checked
- _Peter Lowe’s Ad server list_: checked
- _EasyPrivacy_: checked
- _Online Malicious URL Blocklist‎_: checked
- All other filter lists: unchecked

_My rules_ pane:
- Add `* * 3p-script block`
- Add `* * 3p-frame block`

##### Tips

With one click or two, you can easily fall back into lesser blocking mode, if ever you do not have the willingness to figure the necessary rules for a given site.

To fall back into [easy mode](./Blocking-mode:-easy-mode):
- Set a local noop rule for the _3rd-party script_ cell:<br>
  ![3rd-party scripts allowed](https://user-images.githubusercontent.com/585534/86541958-5ddd7380-bedf-11ea-97bd-99f4e6a79196.png)
- Set a local noop rule for the _3rd-party frames_ cell (optional, as blocking 3rd-party frames is less likely to break websites):<br>
  ![3rd-party frames allowed](https://user-images.githubusercontent.com/585534/86541962-603fcd80-bedf-11ea-9f80-94f9a7c243b6.png)
- If you want the rules to stick, click the padlock to make them permanent.

Using local noop rules ensure that the resulting lesser blocking mode applies _only_ to the current site so that medium mode is still enforced everywhere else.
