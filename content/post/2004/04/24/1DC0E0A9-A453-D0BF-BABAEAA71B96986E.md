{
	"title": "Jedi vs. the Web Services, Round Two",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2004-04-24T12:04:18+06:00",
	"url": "/2004/04/24/1DC0E0A9-A453-D0BF-BABAEAA71B96986E",
	"oldurl": "http://www.raymondcamden.com/2004/4/24/1DC0E0A9-A453-D0BF-BABAEAA71B96986E"
}

So, I got a lot of responses to my <a href="http://www.camdenfamily.com/morpheus/blog/index.cfm?mode=entry&entry=191F703F-AE90-A547-14D96B0CA6242145">earlier post</a> about using a WS under a virtual host. The recommendations pretty much centered around adding an alias to my jrun-web.xml file. This, however, didn't help. Another user suggested that maybe my folder structure was causing the issue - I had used dots in my main folder (tasktracker.jedi.com). However, switching to a simpler folder name didn't help.

On a whim, I decided to try switching to a new machine. This was a pure install of MX - no hotfixes, nothing. Under there - it worked perfectly - with no mods to any XML file or to anything else.

So, now I'm not sure what to do. I may consider simply applying the hotfixes to the second computer to see if it corrects the issue.

I'll post again when I find out more.