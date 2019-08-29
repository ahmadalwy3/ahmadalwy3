No: it is significantly less resource intensive than Adblock Plus ("ABP").

Sloppy benchmarks can lead to the myth that uBlock is just a tad less resource intensive than ABP.

Rigorous benchmarks demonstrate that uBlock is significantly more efficient than ABP.

Examples of sloppiness:

- Using memory footprint figures **before** the browser's garbage collector kicks in
- Not taking measures to avoid tainting memory footprint with [Chromium bug 441500](https://code.google.com/p/chromium/issues/detail?id=441500)
- Using memory footprint figures while option pages for one of the extension are opened
- Disregarding the [contributed memory footprint to web pages](./Contributed-memory-usage:-benchmarks-over-time)
- Comparing memory footprint after extensions have run for a significantly different amount of time
- Using memory footprint figures after one of the extension has performed a one-time resource-intensive task (updating filter lists, etc.)
- Not taking into account the amount of filters in both extensions
