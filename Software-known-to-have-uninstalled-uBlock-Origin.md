Some software may end up removing uBlock Origin ("uBO"). The reason why they removed uBO is not clear, but it could be that uBO contains the malware filter lists as part of its package -- the reason is that I want uBO to be up and running with all filters without having to download them at install time (the update process is automatic, i.e. the filter lists will be updated in the background eventually).

Here is a list of those software which are known to have uninstalled uBlock Origin:

- Avira AntiVirus:
    - https://github.com/gorhill/uBlock/issues/882
    - https://github.com/gorhill/uBlock/issues/1074

    Report form: https://analysis.avira.com/en/submit

- ClamAV:
    - https://github.com/gorhill/uBlock/issues/2315
    - https://github.com/uBlockOrigin/uBlock-issues/issues/599
    - https://github.com/uBlockOrigin/uBlock-issues/issues/698
    - https://github.com/uBlockOrigin/uBlock-issues/issues/700

    Report forms:
    - ClamAV: https://www.clamav.net/reports/fp
    - Immunet: https://www.immunet.com/false_positive
    - Malware Patrol: `fp (@) malwarepatrol.net`

- Junkware Removal Tool:
    - https://github.com/gorhill/uBlock/issues/882#issuecomment-154879542

    Support forum: https://forums.malwarebytes.com/forum/122-false-positives/

- SpyHunter 4:
    - https://github.com/gorhill/uBlock/issues/1009
    - [Of interest](http://www.bleepingcomputer.com/forums/t/550005/spyhunter-vs-malwarebytes-vs-iobit/#entry3491488): "In _my opinion_ SpyHunter is a **dubious program** with a high rate of [false positives](https://www.mywot.com/en/scorecard/enigmasoftware.com)".
