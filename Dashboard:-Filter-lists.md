- Back to [Wiki home](https://github.com/gorhill/uBlock/wiki)
- Back to [Dashboard](https://github.com/gorhill/uBlock/wiki/Dashboard)

***

The _Filter lists_ pane is where you subscribe to filter lists. The filter lists to which you subscribe will feed uBlock Origin's [static filtering engine](https://github.com/gorhill/uBlock/wiki/Overview-of-uBlock's-network-filtering-engine:-details#static-filtering).

The picture below shows uBlock Origin's default selection of filter lists. You can add more, or remove some of the filter lists already selected by default (for reference, most other blockers have only EasyList selected).

If you remove filter lists, it is still strongly advised to at least keep _uBlock filters_ selected: these filters are optimized for uBlock Origin.

The more filter lists one add, the higher the likelihood some web pages may not render properly, due to higher probability of false positives. When this occurs, you should report the issue to the maintainers of the filter list causing the issue, or create your own exception filters to fix the issue.

![Filter lists pane](https://cloud.githubusercontent.com/assets/585534/24972255/cbf77306-1f88-11e7-808e-1e1ac934120f.png)

uBlock Origin discards duplicate filters, so the number of filters used within a filter list depends on how many duplicate filters were detected within that filter list. The order in which the filter lists are loaded into memory is undefined.

When you hover the cursor over the clock icon of a filter list, a tooltip will tell you when the list was last updated. If you click the clock icon, uBO will mark the list as out-of-date. Lists which are out of date will be automatically updated in the background eventually when you check the option _"Auto update filter lists"_. You can force out-of-date lists to be immediately updated by clicking _"Update now"_.

Related: [_"Launch and filter lists load performance"_](https://github.com/gorhill/uBlock/wiki/Launch-and-filter-lists-load-performance).

***

##### Auto-update filter lists

If you check this option, uBlock Origin will update automatically the currently selected filter lists at regular interval. This option is checked by default (recommended).

Filter lists are automatically updated according to:
- the [_Expires_ directive](https://adblockplus.org/filters#special-comments) if present in filter list header
- or `updateAfter` attribute if found in list entry in [`assets.json`](https://github.com/gorhill/uBlock/blob/master/assets/assets.json)
- or every 5 days by default.

##### Update now

This button is available for use if and only if there is at least one filter list which is deemed outdated. If this condition is fulfilled, you can force an update of all filter lists which are deemed out of date.

When a filter list has been updated using a newer version from its remote location, a clock icon will be present aside the filter list. You can force an update of a single filter list by clicking the clock icon of that filter list only, which will reset "last update" timestamp for this list, remove its content from storage, and cause the _"Update now"_ button to become available for use:

![](https://cloud.githubusercontent.com/assets/585534/25020937/4a6a55b6-205e-11e7-94ac-9c51697f9f90.gif)

Note: "uBlock filters" entry is special - forcing update of this filter list, will also update additional resources when possible (library of resources used by [Scriptlet injection](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#scriptlet-injection), allowed to be updated on Chromium browser and develpment buils).

##### Purge all caches

This will reset "last update" timestamp for all of the subscribed filter lists. Essentially, this will cause all filter lists to become out of date. This can be used to force an update of all filter lists.

Clicking this button with <kbd>Ctrl</kbd> and <kbd>Shift</kbd> pressed will remove all locally cached content of filter lists, which will force uBO to rebuild all of its databases from the beginning.

##### Parse and enforce cosmetic filters

Un-check this option if you do not want cosmetic filters to be parsed and enforced. This option is mostly of interest for those who want to further reduce uBlock Origin's memory and CPU footprint. Cosmetic filtering has no value privacy-wise, its only purpose is to [hide elements](https://adblockplus.org/filters#elemhide) on a web page which can't be blocked otherwise. An example of this are the ads served with some Google Search results.

Note that if you disable this option, your own custom cosmetic filters (if any) will still be enforced.

##### Stock filter lists

This is a collection of various filter lists, grouped by purpose. To use a specific filter list, just select it through its checkbox. Any change in the selection of filter lists must be committed by using the _Apply change_ button, which will appear if and only if the current selection of filter lists differs from the previous selection of filter lists.

> ***
> **Important:** The more filter lists are selected, the higher the likelihood of web site breakage. The quality of the selected filter lists also affects the likelihood of web site breakage. The _EasyList_-related filter lists are high quality filter lists, as they are actively maintained.
> ***

##### Custom filter lists

You can import custom 3rd-party filter lists: place check mark next to "Import..." in the "Custom" section and paste the URL of where a filter lists can be fetched from in the text area that appears. These custom filter lists will be also automatically updated on a regular basis.

On some specific web pages, it is possible to subscribe to a 3rd-party filter list by simply clicking on a link to the filter list. There is such a page for uBlock Origin: [Filter lists from around the web](https://github.com/gorhill/uBlock/wiki/Filter-lists-from-around-the-web).