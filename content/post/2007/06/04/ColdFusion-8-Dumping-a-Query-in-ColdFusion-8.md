{
	"title": "ColdFusion 8: Dumping a Query in ColdFusion 8",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2007-06-04T18:06:00+06:00",
	"url": "/2007/06/04/ColdFusion-8-Dumping-a-Query-in-ColdFusion-8",
	"guid": "2089"
}

So a small change - but a nice one. If you dump a query in ColdFusion 8, you now get a set of additional information along with the data. You get...

<ul>
<li>Whether or not the query was cached
<li>The execution time
<li>And best of all - the SQL!
<li>Lastly - if your SQL contained any cfqueryparam tags, there will be a SQLParameters key that is an array of the values used in the cfqueryparam tags.
</ul>

<b>Edited to add last bullet point.</b>

<br clear="left"><p><a href='enclosures/D%3A%5Cwebsites%5Cdev%2Ecamdenfamily%2Ecom%5Cenclosures%2Fqdump%2Epng'>Download attached file.</a></p>