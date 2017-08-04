More specifically, debunking [@christianbute](https://twitter.com/christianbute)'s claim in <https://twitter.com/christianbute/status/893462816270815232>. Two tweets quoted verbatim:

> According to my tests, the best ad and malwaretising blocker for @MicrosoftEdge is AdGuard. Anything else just made the performance worse.

> Yes, even uBlock Origin slowed down my browsing experience. On stock settings or custom lists, doesn't matter. Don't want to mention others

I can't unfortunately investigate this claim on Microsoft Edge, as I do not have Windows. However, both extensions uses the same code on Microsoft Edge as they do on Chromium, thus I can at least benchmark with Chromium.

My objective measurements, benchmarking on Chromium 59 on Linux 64-bit:

uBO 1.13.8
- default settings/lists
- all lists up to date

Adguard 2.6.7
- English + Spyware filters
- disable "Allow search ads and websites' self-promotion"
- all lists up to date

Steps to reproduce:
1. Launch Chromium with only one of the blocker enabled
    - with pinned Extensions tab + only one new tab
    - no other extension
2. Open Chromium's own Task manager, wait for garbage collection in extension
3. Open background page of extension, select "Performance" pane
4. Click "Record" button in performance pane
5. Select the already opened "New tab" in browser
6. Right click on 20-tabs bookmark folder (see below), and select "Open all bookmarks"
7. Wait for all tabs to be loaded
8. Activate each of the newly opened tab one after the other
9. Click "Stop" button in Performance pane
10. Screenshot results in "Performance" pane

For the "memory usage" benchmark: all the same steps except developer tools of extension is not opened, and only Task manager is taken into account. Wait at least 2 minutes after step 8. before taking a screenshot of Task manager.

20-tabs bookmark folder in bookmarks bar (perused from top posts on Hacker News in the last year, hence "real life usage"):
- http://www.hntoplinks.com/year/2
- https://www.susanjfowler.com/blog/2017/2/19/reflecting-on-one-very-strange-year-at-uber
- http://www.nature.com/news/these-seven-alien-worlds-could-help-explain-how-planets-form-1.21512?WT.mc_id=TWT_NatureNews
- https://medium.com/@amyvertino/my-name-is-not-amy-i-am-an-uber-survivor-c6d6541e632f
- https://www.nytimes.com/2017/06/21/technology/uber-ceo-travis-kalanick.html?_r=0
- https://www.malwaretech.com/2017/05/how-to-accidentally-stop-a-global-cyber-attacks.html
- https://qz.com/937038/github-now-lets-its-workers-keep-the-ip-when-they-use-company-resources-for-personal-projects/?s=1
- https://techcrunch.com/2017/01/09/atlassian-acquires-trello/
- https://www.washingtonpost.com/news/the-fix/wp/2016/11/08/donald-trumps-path-to-victory-is-suddenly-looking-much-much-wider/?hpid=hp_hp-bignews3_fix-electoralmap-210am%3Ahomepage%2Fstory
- https://news.mit.edu/2017/tim-berners-lee-wins-turing-award-0404
- https://code.facebook.com/posts/1840075619545360
- https://www.blog.google/topics/public-policy/net-neutrality-day-action-help-preserve-open-internet/
- https://daringfireball.net/2017/06/fuck_facebook
- https://josephg.com/blog/electron-is-flash-for-the-desktop/
- https://privacylog.blogspot.ca/2017/04/what-happens-when-you-send-zero-day-to.html
- http://www.groundup.org.za/article/why-were-dropping-google-ads/
- http://www.sciencedirect.com/science/article/pii/S1525001617301107
- https://twitter.com/GambleLee/status/862307447276544000
- https://answers.microsoft.com/en-us/msoffice/forum/msoffice_onedrivefb-mso_o365brs/onedrive-for-business-open-is-very-slow-on-linux/3d33dc1b-3cc3-4c24-9998-9ab96bad31fc
- https://www.theatlantic.com/magazine/archive/2017/06/lolas-story/524490/?single_page=true
- https://www.theguardian.com/technology/2017/jan/13/whatsapp-design-feature-encrypted-messages

Results:

CPU usage (see pic):
- uBlock Origin (top): 4,662.3 ms (3,403.6 ms + 1,258.7 ms)
- Adguard (bottom): 14,424 ms (11,638.8 ms + 2,785.2 ms)

![c](https://user-images.githubusercontent.com/585534/28976229-1a45cc20-790b-11e7-83df-31372efd5e93.png)

Memory usage after all tabs loaded (see pic, top is after browser launch + garbage collection and before all tabs opened):
- uBlock Origin (left): 1,254 MB
- Adguard (right): 1,535 MB

![d](https://user-images.githubusercontent.com/585534/28976324-6910e2c2-790b-11e7-9388-3591daaed7b6.png)

### Conclusion:

Both extensions use essentially the same code on Microsoft Edge as they do on Chromium, so it is expected they will have the same relative performance outcome. Given that uBlock Origin consumes 1/3 of CPU cycles to actually accomplish more than Adguard (uBO's defaults includes Peter Lowe's and malware lists), to claim that the results are completely reversed on Microsoft Edge is quite an extraordinary claim, and thus needs to be substantiated by more than just a completely subjective and data-less assessment such as "methodology is real life usage".
