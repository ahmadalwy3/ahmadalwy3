- Back to [Wiki home](https://github.com/gorhill/uBlock/wiki)
- Back to [Dashboard](https://github.com/gorhill/uBlock/wiki/Dashboard)

***

The _3rd-party filters_ pane is where you subscribe to filter lists. The filter lists to which you subscribe will feed uBlock Origin's [static filtering engine](https://github.com/gorhill/uBlock/wiki/Overview-of-uBlock's-network-filtering-engine:-details#static-filtering).

The picture below shows uBlock Origin's default selection of filter lists. You can add more, or remove some of the filter lists already selected by default (for reference, most other blockers have only EasyList selected).

If you remove filter lists, it is still strongly advised to at least keep _uBlock filters_ selected: these filters are optimized for uBlock Origin.

The more filter lists one add, the higher the likelihood some web pages may not render properly. When this occurs, you should report the issue to the maintainers of the filter list causing the issue, or create your own exception filters to fix the issue.

![3rd-party filter pane](https://cloud.githubusercontent.com/assets/585534/24972255/cbf77306-1f88-11e7-808e-1e1ac934120f.png)

uBlock Origin discards duplicate filters, so the number of filters used within a filter list depends on how many duplicate filters were detected within that filter list. The order in which the filter lists are loaded into memory is undefined.

When you hover the cursor over the clock icon of a filter list, a tooltip will tell you when the list was last updated. If you click the clock icon, uBO will mark the list as out-of-date. Lists which are out of date will be automatically updated in the background eventually when you check the option _"Auto update filter lists"_. You can force out-of-date lists to be immediately updated by clicking _"Update now"_.

Related: [_"Launch and filter lists load performance"_](https://github.com/gorhill/uBlock/wiki/Launch-and-filter-lists-load-performance).

***

##### Auto-update filter lists

If you check this option, uBlock Origin will update automatically the currently selected filter lists at regular interval. This option is checked by default (recommended).

Filter lists are automatically updated roughly every 5 days by default, or according to the _Expires_ directive present in some filter lists.

##### Update now

This button is available for use if and only if there is at least one filter list which is deemed outdated. If this condition is fulfilled, you can force an update of all filter lists which are deemed out of date.

When a filter list has been updated using a newer version from its remote location, a clock icon will be present aside the filter list. You can force an update of a single filter list by clicking the clock icon of that filter list only. This will cause the _"Update now"_ button to become available for use:

![](https://cloud.githubusercontent.com/assets/585534/25020937/4a6a55b6-205e-11e7-94ac-9c51697f9f90.gif)

##### Purge all caches

This will remove all locally cached copies of filter lists. Essentially, this will cause all filter lists to become out of date. This can be used to force an update of all filter lists.

##### Parse and enforce cosmetic filters

Un-check this option if you do not want cosmetic filters to be parsed and enforced. This option is mostly of interest for those who want to further reduce uBlock Origin's memory and CPU footprint. Cosmetic filtering has no value privacy-wise, its only purpose is to [hide elements](https://adblockplus.org/filters#elemhide) on a web page which can't be blocked otherwise. An example of this are the ads served with some Google Search results.

Note that disabling this option will also cause your own custom cosmetic filters (if any) to be ignored.

##### Stock filter lists

This is a collection of various filter lists, grouped by purpose. To use a specific filter list, just select it through its checkbox. Any change in the selection of filter lists must be committed by using the _Apply change_ button, which will appear if and only if the current selection of filter lists differs from the previous selection of filter lists.

> ***
> **Important:** The more filter lists are selected, the higher the likelihood of web site breakage. The quality of the selected filter lists also affects the likelihood of web site breakage. The _EasyList_-related filter lists are high quality filter lists, as they are actively maintained.
> ***

##### Custom filter lists

You can import custom 3rd-party filter lists: just paste in the text area the URL of where a filter lists can be fetched. These custom filter lists will be also automatically updated on a regular basis.

On some specific web pages, it is possible to subscribe to a 3rd-party filter list by simply clicking on a link to the filter list. There is such a page for uBlock Origin: [Filter lists from around the web](https://github.com/gorhill/uBlock/wiki/Filter-lists-from-around-the-web).