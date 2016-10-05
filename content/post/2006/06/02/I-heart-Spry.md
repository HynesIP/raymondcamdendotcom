{
	"title": "I heart Spry",
	"categories": [
		"Misc"
	],
	"tags": [],
	"date": "2006-06-02T17:06:00+06:00",
	"url": "/2006/06/02/I-heart-Spry",
	"guid": "1314"
}

I'm a bit late to the party, but I finally took some time to check out the <a href="http://labs.adobe.com/technologies/spry/">Spry framework</a>, Adobe's answer to the AJAX craze. I haven't been that impressed with AJAX. I mean, it's useful, yes. Very useful. But it's also kind of old and so it isn't really new to me. I've been thinking about learning a bit of AJAX for use in the back end of BlogCFC. I took some time early this morning to look at Spry.

Wow.

I mean, seriously, Adobe, could you make this a bit simpler? I think it was harder to put my shoes on this morning. Consider the following simple example (and this is <b>not</b> 100% complete, but it gives you an idea of how short the code is):

<code>
&lt;script type="text/javascript" src="includes/xpath.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="includes/SpryData.js"&gt;&lt;/script&gt;
&lt;!-- load the xml, notice the xpath support --&gt;
&lt;script type="text/javascript"&gt;
var dsHatches = new Spry.Data.XMLDataSet("dharma.xml", "hatches/hatch");
&lt;/script&gt;

&lt;!-- now bind it to an html table --&gt;
&lt;div id="Hatches_DIV" spryregion="dsHatches"&gt;
&lt;!--Display the data in a table--&gt;
&lt;table&gt;
&lt;tr&gt;
&lt;th&gt;Hatch&lt;/th&gt;
&lt;th&gt;Icon&lt;/th&gt;
&lt;th&gt;Active&lt;/th&gt;
&lt;/tr&gt;
&lt;tr spryrepeat="dsHatches"&gt;
&lt;td&gt;{hatch}&lt;/td&gt;
&lt;td&gt;&lt;img src="/images/dharma/{icon}"&gt;&lt;/td&gt;
&lt;td&gt;{active}&lt;/td&gt;
&lt;/tr&gt;
&lt;/table&gt;
&lt;/div&gt;
</code>

So the first line loads the data set from XML. It uses XPath to translate this into a data set. I can then bind it to a table by using the spryregion and spryrepeat tags. Notice the use of bound variables inside. 

For a more complete demo, check out the Spry front end version of <a href="http://ray.camdenfamily.com/demos/spry/blog.cfm">BlogCFC</a>. Make sure you view source on that.

I did run into one interesting problem. I knew that I needed XML, so I knew I couldn't just use my blog's main CFC. I wrote a new CFC that would handle the few methods I needed and return them as XML. (This was rather boring, but I did make two cool little functions you may like, arrayToXML and queryToXML. Both of these already exist on CFLib I think, but I wrote my own for the heck of it.) 

I thought that was all I needed, but it wasn't loading. Then I tried making the same request Spry was, and I found out what it was. ColdFusion was wrapping my response in WDDX. So what could I do? (I wish CFC's had an option to NOT wrap the result in WDDX and just return it "bare".) I wrote another file, this time a CFM. It simply acted as a proxy to call my other proxy CFC. It then returned the XML correctly. 

I think I spent more time in ColdFusion then I did in JavaScript. That to me is a good thing. It means Adobe really did a darn good job with this framework. This is exactly the kind of thing I can see using in real world applications. 

I definitely recommend my readers to take a few minutes and download the framework. I think you will find it worth your while.