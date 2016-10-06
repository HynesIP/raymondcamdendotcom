{
	"title": "Working with StrongLoop (Part Three)",
	"categories": [
		"Development",
		"JavaScript"
	],
	"tags": [
		"strongloop"
	],
	"date": "2015-10-15T12:23:24+06:00",
	"url": "/2015/10/15/working-with-strongloop-part-three",
	"guid": "6948"
}

So this week I'm continuing my look into <a href="https://strongloop.com/">StrongLoop</a>. If you missed my previous entries, I'll include them in a list at the bottom. I'm kinda hopping around the technology picking and choosing what seems interesting to me so these posts may not be the best introduction to the platform, but I hope folks are finding it interesting. As a reminder, you can access the core documentation <a href="https://docs.strongloop.com/display/SL/Installing+StrongLoop">here</a> to start learning about it yourself. As I mentioned in the very first post, StrongLoop's Arc product runs on top of the open source <a href="http://loopback.io/">LoopBack</a> framework. Today's post is pretty much entirely based on that. 

When I began this series, I discussed how you could quickly generate APIs for your data. You've got a CLI and a visual component (that's where Arc comes in) that allow for rapid development. In five minutes, I can create a model for my data and have a complete set of APIs to list, find, create, update, and delete that data. This got me thinking though - given you get a set of CRUD operations out of the box, how do you modify the API to add or alter those operations?

<!--more-->

First - let's examine how you would add new methods to your remote API. The StrongLoop docs cover this very well (<a href="https://docs.strongloop.com/display/public/LB/Remote+methods">Remote methods</a> and I'm going to borrow from them liberally. To add a new method, you do two things. First, you define the method itself. Remember that every model item creates a model.js file and model.json file (where 'model' is replaced with the name of your model). I have a Cat model and I want to add a remote method that would let me return a cat by name instead of ID. (As an aside, the APIs generated by LoopBack already provide a way to filter by properties, so technically this is already done, but I wanted a specific method for this functionality.) I wrote a simple method that just returned a string.

<pre><code class="language-javascript">Cat.byName = function(name,cb) {
	cb(null,'you want '+name);	
};</code></pre>

In the code sample above, the null argument there is where you would use an error if something had gone wrong. We'll replace this logic with something real in a moment. That's step one. Step two is to expose the method remotely. Here is how you could do that.

<pre><code class="language-javascript">Cat.remoteMethod('byName', 
	{
		http: {path:'/name', verb:'get'},
		accepts:{arg:'name', type:'string'},
		returns:{arg:'name', type:'string'}
	}
);</code></pre>

In the code sample above, I'm defining that byName is remote and I'm defining how it is accessed (note the http section). I'm also defining that it accepts an argument and returns a string.

When I restart my application (and you do not need to do this via the CLI, if you have StrongLoop Arc running, you can reload from the UI), I can see, and test this, in the Explorer:

<img src="https://static.raymondcamden.com/images/wp-content/uploads/2015/10/shot15.png" alt="shot1" width="750" height="518" class="aligncenter size-full wp-image-6949" />

I then modified the code to do a real look up. I haven't really seen yet the CRUD methods you have available via code, but they are incredibly easy to use. Here is how I implemented it. 

<pre><code class="language-javascript">Cat.byName = function(name,cb) {
	console.log('find by name '+name);
	Cat.findOne({where:{name:name}}, function(err, cat) {
		cb(null,cat);
	});
};
		
Cat.remoteMethod('byName', 
	{
		http: {path:'/name', verb:'get'},
		accepts:{arg:'name', type:'string'},
		returns:{arg:'cat', type:'cat'}
	}
);</code></pre>

Simple, right? Also note I updated the return type to specifically say I'm returning a cat. My code doesn't handle an unknown cat well, but you get the basic idea. Here is the updated result:

<img src="https://static.raymondcamden.com/images/wp-content/uploads/2015/10/shot25.png" alt="shot2" width="750" height="397" class="aligncenter size-full wp-image-6953" />

Another interesting aspect is the ability to work with <a href="https://docs.strongloop.com/display/public/LB/Remote+hooks">remote hooks</a>. These are functions that run in conjunction with other API calls. They let you do something before and after a remote call. They also let you hook into an error event. You can use this for logging or to sanitize inputs for methods or modify results for output. What's cool is that you can even use wild cards to match multiple (or all) remote methods for automatic logging of <i>everything</i> your API does. StrongLoop differentiates between static and model methods, so this particular example will only match the static calls (you can match the other ones too of course):

<pre><code class="language-javascript">Cat.beforeRemote('*', function( ctx, cat, next) {
	console.log('calling '+JSON.stringify(ctx.methodString));
	next();
});</code></pre>

Not really rocket science, but I love how easy it is to do stuff like this. 

For the final bit of this post, how about blocking a particular method? You can hide a method following the guide here (<a href="https://docs.strongloop.com/display/public/LB/Authentication%2C+authorization%2C+and+permissions#Authentication,authorization,andpermissions-HidingmethodsandRESTendpoints">Hiding methods and REST endpoints</a>). This is actually from the security section and that's something I want to cover later on, but if you just want to blanket hide/block something, you can do it like so:

<pre><code class="language-javascript">Cat.disableRemoteMethod('findOne', true);</code></pre>

Again - super simple and incredibly quick to implement.

So - hopefully you are finding these posts interesting. I'm going to keep digging into StrongLoop and demonstrate more features over the next couple of weeks.

<h2>Previous Entries</h2>

<ul>
<li><a href="http://www.raymondcamden.com/2015/10/13/working-with-strongloop-part-two">Working with StrongLoop (Part Two)</a></li>
<li><a href="http://www.raymondcamden.com/2015/10/12/working-with-strongloop-part-one">Working with StrongLoop (Part One)</a></li>
</ul>

