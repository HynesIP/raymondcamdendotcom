{
	"title": "Simple math tricks with ColdFusion 8 Ajax tags",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2008-02-21T09:02:00+06:00",
	"url": "/2008/02/21/Simple-math-tricks-with-ColdFusion-8-Ajax-tags",
	"guid": "2664"
}

A reader yesterday asked me an interesting question. Using ColdFusion 8 and bindings, is it possible to do simple mathematics? For example, he wanted something like this:

<code>
&lt;input type="text" name="res" bind="{field1}*{field2}"&gt;
</code>

While that isn't possible, you can do it using cfajaxproxy. (Oh my sweet cfajaxproxy - is there anything you cannot do???) Consider the following example:

<code>
&lt;cfajaxproxy bind="javascript:doMultiply({first},{second})" /&gt;
&lt;script&gt;
function doMultiply(x,y) {
	document.getElementById("result").value = x*y;
}
&lt;/script&gt;

&lt;form&gt;
&lt;input id="first" size="3"&gt; X &lt;input id="second" size="3"&gt; = &lt;input id="result"&gt;

&lt;/form&gt;
</code>

The form has 3 fields. The first two are for the numbers I'll be multiplying. The last field is for the result. I use the cfajaxproxy tag to bind to the first two fields. I run the JavaScript function, doMultiply, whenever first or second changes. And that's it! I should probably add a check to see if x and y are numeric, but you get the idea.