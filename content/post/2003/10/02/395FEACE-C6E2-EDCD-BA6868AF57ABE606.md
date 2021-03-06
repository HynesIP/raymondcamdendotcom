{
	"title": "Odd Issue with cfcontent, cfsetting, and wrapper tags...",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2003-10-02T13:10:12+06:00",
	"url": "/2003/10/02/395FEACE-C6E2-EDCD-BA6868AF57ABE606",
	"oldurl": "http://www.raymondcamden.com/2003/1/2/395FEACE-C6E2-EDCD-BA6868AF57ABE606"
}

I've been in Memphis this week migrating an application we wrote for a bank from CF5 to MX 6.1. In general, it has gone very nicely. The Code Analyzer was <i>wonderful</i> for pointing out the obvious stuff, and the rest of the issues we ran into were fairly minor... until today. We have a report that we generate on screen, as well as giving you the option to export to a text file. We used cfheader/cfcontent to handle the export, using code like so:

			
&lt;cfheader name="Content-Disposition" value="attachment; filename=foo.txt"&gt;<br>
&lt;cfcontent type="text/plain" reset="yes"&gt;

This was working in CF5, but under MX 6.1, we kept getting a blank page (not in the browser, but in the text file that was created). The first thing I did was to remove the cfheader/content to ensure that text really was coming out. It was. I then tried a different browser and that didn't work either. This particular piece of code was buried a bit deep, so I did a copy/paste into a new CFM, and discovered it worked fine!

So, I dug around quite a bit more, and have found what I believe to be a bug in CFMX. The issue involved two things: One, I was using cfsetting enablecfoutputonly="true" and two, I was using a "wrapper" tag for layout. By "wrapper" I mean code that looks like this, &lt;cf_display&gt; stuff &lt;/cf_display&gt;. If I switched the cfsetting to false, the problem went away. If I kept it at either true or false, but removed the custom tag calls, the problem also went away. It seems as if the user of the wrapper tag confused things. 

Anyway, as always I share my headaches to help prevent yours. :) Also, I made sure to log a  bug at <a href="http://www.macromedia.com/go/wish">http://www.macromedia.com/go/wish</a>.