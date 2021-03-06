{
	"title": "Second draft - JavaScript Library for Behance Integration",
	"categories": [
		"Design",
		"Development",
		"JavaScript"
	],
	"tags": [],
	"date": "2013-10-17T10:10:00+06:00",
	"url": "/2013/10/17/Second-draft-JavaScript-Library-for-Behance-Integration",
	"guid": "5062"
}

<p>
Yesterday I <a href="http://www.raymondcamden.com/index.cfm/2013/10/16/First-draft--JavaScript-Library-for-Behance-Integration">blogged</a> an example of using the <a href="http://www.behance.net">Behance API</a> via JavaScript. In the first draft of my demo I built in basic support to get projects for a user. While this worked fine, it put the onus of displaying those projects on the coder, and for folks who may not be good with JavaScript, I wanted to provide a simpler solution.
</p>
<!--more-->
<p>
With that in mind, I've added a new method to the API: renderProjects. Given a username, a place to put crap, and a template div (more on that in a second), it will handle fetching and rendering the projects for you. Here is an example of the front end HTML:
</p>

<pre><code class="language-markup">&lt;!doctype html&gt;
&lt;html lang=&quot;en&quot;&gt;
	&lt;head&gt;
	&lt;style&gt;
		.project {
			background-color: rgba(7, 219, 64, 0.72);
			width: 280px;
			float: left;
			margin: 0px 10px 10px 10px;
		}
	&lt;&#x2F;style&gt;
	&lt;&#x2F;head&gt;
	
	&lt;body&gt;
		
		&lt;h1&gt;My Projects&lt;&#x2F;h1&gt;
		&lt;div id=&quot;projects&quot;&gt;
		
		&lt;&#x2F;div&gt;
		
		&lt;script src=&quot;jquery-2.0.0.min.js&quot;&gt;&lt;&#x2F;script&gt;
		&lt;script src=&quot;behance_api.js&quot;&gt;&lt;&#x2F;script&gt;
		&lt;script src=&quot;demo2.js&quot;&gt;&lt;&#x2F;script&gt;
		
		&lt;script id=&quot;projectTemplate&quot; type=&quot;text&#x2F;x-behance-template&quot;&gt;
		&lt;div class=&quot;project&quot;&gt;
		&lt;h2&gt;&lt;a href=&quot;{{url}}&quot;&gt;{{name}}&lt;&#x2F;a&gt;&lt;&#x2F;h2&gt;
		&lt;i&gt;Created: {{created}}&lt;&#x2F;i&gt;&lt;br&#x2F;&gt;
		&lt;i&gt;Fields: {{fields}}&lt;&#x2F;i&gt;&lt;br&#x2F;&gt;
		&lt;i&gt;Stats: Appreciations={{appreciations}}, Comments={{comments}}, Views={{views}}&lt;&#x2F;i&gt;&lt;br&#x2F;&gt;
		&lt;img src=&quot;{{covers_230}}&quot;&gt;
		&lt;&#x2F;div&gt;
		&lt;&#x2F;script&gt;

	&lt;&#x2F;body&gt;
&lt;&#x2F;html&gt;</code></pre>

<p>
For the most part this is the same as yesterday's code, but notice the new script block at the bottom. You are allowed to build script blocks that contain stuff besides JavaScript. <a href="http://handlebarsjs.com/">Handlebars.js</a> makes use of this as well. The code within this block will not be displayed to the end user but can be picked up by JavaScript. 
</p>

<p>
Inside the block I've put my considerable design skills to use to create a basic template for my projects. The values inside the squiggly brackets represent tokens that the JavaScript code will replace. The JavaScript for this template is much simpler now that the rendering is being done at the library level.
</p>

<pre><code class="language-javascript">&#x2F;* global $,console,document,behanceAPI *&#x2F;
var behancekey = &quot;vNvOiZI0cD9yfx0z4es9Ix6r4L2J7KdI&quot;;

$(document).ready(function() {
	
	&#x2F;&#x2F;Set my key
	behanceAPI.setKey(behancekey);
	
	&#x2F;&#x2F;Now get my projects
	behanceAPI.renderProjects(&quot;gwilson&quot;, &quot;projects&quot;, &quot;projectTemplate&quot;);

});</code></pre>

<p>
Now let's look at the library.
</p>

<pre><code class="language-javascript">/* global console,$ */
var behanceAPI = function() {
	var key;
	var baseURL = "http://www.behance.net/v2/";
	
	function _toDateStr(d) {
		return new Date(d*1000).toString();	
	}
	
	function _renderTemplate(p, template) {
		var result = template;
		//console.dir(p);
		result = result.replace(/{{name}}/gi, p.name);
		result = result.replace(/{{url}}/gi, p.url);
		if(p.covers[115]) result = result.replace(/{{covers_115}}/gi, p.covers[115]);
		if(p.covers[202]) result = result.replace(/{{covers_202}}/gi, p.covers[202]);
		if(p.covers[230]) result = result.replace(/{{covers_230}}/gi, p.covers[230]);
		if(p.covers[404]) result = result.replace(/{{covers_404}}/gi, p.covers[404]);
		
		var created = _toDateStr(p.created_on);
		result = result.replace(/{{created}}/gi, created);

		var modified = _toDateStr(p.modified_on);
		result = result.replace(/{{modified}}/gi, modified);

		result = result.replace(/{{fields}}/gi, p.fields.join(", "));

		result = result.replace(/{{appreciations}}/gi, p.stats.appreciations);
		result = result.replace(/{{comments}}/gi, p.stats.comments);
		result = result.replace(/{{views}}/gi, p.stats.views);
		
		return result;
	}
	
	function setKey(k) {
		key = k;	
	}
	
	function getProjects(user, cb) {
		var url = baseURL + "users/" + user + "/projects?api_key=" + key + "&callback=";
		$.get(url, {}, function(res, code) {
			cb(res.projects);
		}, "JSONP");
	}
	
	function renderProjects(user, displayId, templateId) {
		var templateOb = $("#" + templateId);
		var renderDom = $("#" + displayId);
		
		if(templateOb.length === 0 || renderDom.length === 0) {
			//Throw an error?
			return;
		}

		var template = $.trim(templateOb.html());
		getProjects(user, function(p) {
			var s = "";
			for(var i=0; i&lt;p.length; i++) {
				s += _renderTemplate(p[i], template);	
			}
			renderDom.html(s);
		});
	}
	
	return {
		setKey: setKey,
		getProjects: getProjects,
		renderProjects: renderProjects
	};
	
}();</code></pre> 

<p>
For the most part I assume this is self-explanatory. You can see my code pick up the DOM item for the template and grab out the HTML. That HTML, plus a project, is sent to _renderTemplate where the real work is done. I do a bit of manipulation where I can to help out, like on dates and the field list.
</p>

<p>
So to be clear, this is <strong>not</strong> as powerful of a solution as Handlebars, but as my library would still let you use it if you wanted to, I thought this was a nice simple way for users to quickly handle the layout. Here is a screenshot. 
</p>

<p>
<img src="https://static.raymondcamden.com/images/bapi.jpg" />
</p>

<p>
Anyway, this was fun, but I'll probably stop working on this unless I get bored, or unless someone asks me to continue. There is already a public JavaScript library for Behance (but not with my cool function), so unless there is interest, I'll just leave this for now as a fun experiment. 
</p><p><a href='enclosures/C%3A%5Chosts%5C2013%2Eraymondcamden%2Ecom%5Cenclosures%2FArchive%2021%2Ezip'>Download attached file.</a></p>