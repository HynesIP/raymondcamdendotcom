{
	"title": "This blog...",
	"categories": [
		"Misc"
	],
	"tags": [],
	"date": "2014-03-14T11:03:00+06:00",
	"url": "/2014/03/14/This-blog",
	"guid": "5174"
}

<p>
I have to apologize. For a while now this server has had issues. Sometimes I have to restart the services every morning. Sometimes it runs fine for days. My host, <a href="http://www.edgewebhosting.net/">Edge Web</a>, are very proactive and helpful, I know this because I'll get multiple phone calls, emails, etc as they try to repair my server. This bugs me because I am costing them time for something I should be able to correct myself. They give me a good deal as I help promote ColdFusion and provide open source and community resources, but at the end of the day, I don't want to be a burden to them as I'm not really paying my fair share there.
</p>

<p>
The issues I have on my box are something involving Apache or ColdFusion. If I could spend a day just hacking away at it I could possibly figure it out. I <strong>have</strong> spent time digging into it (and as I said, so have Edge Web), but at the end of the day, I do not want to be a server administrator. I don't want to have to worry about tuning. I want this site to continue to be a resource for folks who want to learn. If that means ditching all my dependancies, then so be it. 
</p>

<p>
Right now I'm considering moving to static. I can't move to S3 because they don't support regex URL replacements. I could easily use one regex rewrite rule to go from /index.cfm/2014/3/12/Reprint-What-in-the-heck-is-JSONP-and-why-would-you-use-it to /2014/3/12/Reprint-What-in-the-heck-is-JSONP-and-why-would-you-use-it, but that isn't supported with S3 hosting. The other big issue is comments. Disqus allows for importing, but I currently have 50000+ comments here. I'd have to be careful to not miss anything. Everything is lagniappe. I'm more than willing to push search to a custom Google search engine. Any ColdFusion demos would fail, but I typically post my code in downloadable format as well.
</p>

<p>
During the time I wrote this post - I had to restart Apache multiple times - so heck - it may not be related to ColdFusion (or MySQL) at all. That being said - I don't care. I want to simplify as much as possible so I can focus on having this site up 100% of the time.
</p>