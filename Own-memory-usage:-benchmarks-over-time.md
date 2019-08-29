Just a place for me to keep track of comparative memory usage over time. Screenshot before/after [reference benchmark](./Reference-benchmark). Great care taken to ensure memory was garbage collected before screenshots taken. To force memory garbage collection, browser left on idle for more than 1 minute, then dev console of each extension opened, _Timeline_ tab, then clicked twice on the trash can icon.

### 23 December 2014

- Chromium 39.0.2171.65 64-bit (Linux)
- uBlock 0.8.2.2
- AdBlock 2.15
- Adblock Plus 1.8.8
- Adguard AdBlocker 1.0.3.8

Before benchmark started:<br>
![before](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-20141223-before.png)

After benchmark completed:<br>
![after](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-20141223-after.png)

Observations during benchmark:
- ABP/AdBlock/Adguard are CPU intensive. Whereas uBlock consistently show at most low-single digit CPU usage, other blockers are most often showing double-digit CPU usage, and sometimes in the high double-digit range.

Settings:
- **uBlock 0.8.2.2**: _EasyList_, _EasyPrivacy_, _Peter Lowe's_, _Fanboy’s Social Blocking List‎_, all malware lists (3). Launched with a valid selfie (i.e. less memory churning at launch).
- **AdBlock 2.15**: _AdBlock custom filters_, _EasyList_, _EasyPrivacy_, _Peter Lowe's_, _Fanboy’s Social Blocking List‎_, _Malware protection_.
- **Adblock Plus 1.8.5**: _EasyList_, _EasyPrivacy_, _Peter Lowe's_, _Fanboy’s Social Blocking List‎_, _Malware Domains_. _Acceptable ads_ disabled.
- **Adguard AdBlocker 1.0.3.8**: _English filters_, _Spyware filter_, _Peter Lowe's_, _Social media filter‎_, _Phishing and malware protection_. _Allow acceptable ads_ disabled.
- Browser's _Click-to-play_ enabled
- Browser's _Block third-party cookies and site data_ checked

Notes:

- Users should mind [privacy issues](http://adguard.com/en/how-malware-blocked.html#extension) raised when enabling AdGuard's _Malware/phishing protection_.

### 18 September 2014

- Chromium 37.0.2062.94 64-bit (Linux)
- uBlock v 0.6.2.1
- AdBlock 2.7.13
- Adblock Plus 1.8.5
- Ghostery 5.4.0
- Disconnect 5.18.15

Before benchmark started:<br>
![before](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-20140918-before.png)

After benchmark completed:<br>
![after](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-20140918-after.png)

Observations during benchmark:
- AdBlock is *very* CPU intensive. Adblock Plus also, although to a lesser degree compared to AdBlock.

Settings:
- **uBlock v 0.6.2.1**: _EasyList_, _EasyPrivacy_, _Peter Lowe's_, _Fanboy’s Social Blocking List‎_, all malware lists (3). Launched with a valid selfie (i.e. less memory churning at launch).
- **AdBlock 2.7.13**: _AdBlock custom filters_, _EasyList_, _EasyPrivacy_, _Fanboy’s Social Blocking List‎_, _Malware protection_.
- **Adblock Plus 1.8.5**: _EasyList_, _EasyPrivacy_, _Fanboy’s Social Blocking List‎_, _Malware Domains_. _Acceptable ads_ disabled.
- **Ghostery 5.4.0**: _Blocking all trackers_. Ghostrank not selected. _Alert bubble_ disabled.
- **Disconnect 5.18.15**: Default settings.

Notes:

I chose to not benchmark AdGuard, because of the privacy issues when enabling _Malware/phishing protection_.
