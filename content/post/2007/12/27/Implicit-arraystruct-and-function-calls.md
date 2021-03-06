{
	"title": "Implicit array/struct and function calls",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2007-12-27T07:12:00+06:00",
	"url": "/2007/12/27/Implicit-arraystruct-and-function-calls",
	"guid": "2562"
}

I'm thinking this is something folks have blogged about before, but I just ran into it today. When using array and struct implicit creation, you cannot use the syntax directly in a udf/method call. Let me explain. Consider this example:

<code>
&lt;cfset z = {name='r',age=34}&gt;
&lt;cfset somefunc(data=z)&gt;
</code>

In this example I use shorthand notation to creation a structure. I then pass it to somefunc as an argument named data. This works just fine. But this version, which should be the same, will give you a syntax error:

<code>
&lt;cfset somefunc(data={name='r',age=34})&gt;
</code>

I also tried the simpler form:

<code>
&lt;cfset somefunc({name='r',age=34})&gt;
</code>

Which also failed. It looks like you can only use the implicit creation in cfset statements. (Which is certainly ok, I'm just happy we have this shortcut!)