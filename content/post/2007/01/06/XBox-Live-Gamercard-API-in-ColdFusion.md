{
	"title": "XBox Live Gamercard API in ColdFusion",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2007-01-06T11:01:00+06:00",
	"url": "/2007/01/06/XBox-Live-Gamercard-API-in-ColdFusion",
	"guid": "1757"
}

There isn't a real API for XBox Live, but I thought it would be fun to whip one up. This UDF is a bit ugly and needs to be cleaned. I'll release to <a href="http://www.cflib.org">CFlib</a> once I've made it nicer. Right now it returns gamescore (nerd score!), a link to your gamer image, your last five games played, your XBox Live level, and a link to your XBox Live URL. 

To get your data, you just pass in your XBox Live username:

<code>
&lt;cfset info = getGamerCard('cfjedimaster')&gt;
&lt;cfset info2 = getGamerCard('boyzoid')&gt;
</code>

I've attached the UDF and test code to this blog entry. Hopefully Microsoft will come to their senses and create a real API soon so we can avoid all this silly string parsing.<p><a href='enclosures/D%3A%5Cwebsites%5Cdev%2Ecamdenfamily%2Ecom%5Cenclosures%2Ftest%2Ecfm%2Ezip'>Download attached file.</a></p>