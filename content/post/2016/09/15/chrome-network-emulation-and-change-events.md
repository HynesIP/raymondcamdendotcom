
{
	"title": "Chrome Network Emulation and Change Events",
	"date": "2016-09-15T10:58:00-07:00",
	"categories": [
		"Development","JavaScript"
	],
	"tags": [],
	"url": "/2016/09/15/chrome-network-emulation-and-change-events"
}

So this is more a FYI then anything else, but a while ago, Chrome released support to emulate different network conditions in dev tools. (Oddly, it doesn't seem to be documented in the [Chrome DevTools Network](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading?utm_source=dcc&utm_medium=redirect&utm_campaign=2016q3) help page.) Basically you can select from different speeds and even quickly toggle offline/online. If you've never seen it - here is what it looks like:

<!--more-->

![Network Tools](https://static.raymondcamden.com/images/2016/09/chromenetwork1.png)

Clicking the dropdown reveals the following options:

![Network Tools](https://static.raymondcamden.com/images/2016/09/chromenetwork2.png)

So this worked well, except in one pretty important aspect. If you had JavaScript code that listened for network changes or simply checked for the connection (see documentation here: ["Online and offline events"](https://developer.mozilla.org/en-US/docs/Online_and_offline_events)) it would not pick up on changes done via Dev Tools. 

So for those of us trying to write code to properly handle a web page going offline, that meant you had to test the old fashion way - turn your wifi off. (Which killed everything, including your super important Twitter feed.)

I filed a bug report for this nearly two years ago: [Issue 422956](https://bugs.chromium.org/p/chromium/issues/detail?id=422956&can=2&start=0&num=100&q=&colspec=ID%20Pri%20M%20Stars%20ReleaseBlock%20Component%20Status%20Owner%20Summary%20OS%20Modified&groupby=&sort=) 

Yesterday I was doing some testing and discovered that it *appears* to be fixed. I tested using the simple Gist in my bug report and `navigator.onLine` correctly responded. Also, my `online` and `offline` event handlers ran fine too.

Now it worries me that the bug hasn't been updated. It's possible that it hasn't been QAed. But for now, it certainly seems a bit safe to use. 