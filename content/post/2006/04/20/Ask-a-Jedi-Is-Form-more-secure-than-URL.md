{
	"title": "Ask a Jedi: Is Form more secure than URL?",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2006-04-20T14:04:00+06:00",
	"url": "/2006/04/20/Ask-a-Jedi-Is-Form-more-secure-than-URL",
	"guid": "1227"
}

Luis asks:

<blockquote>
Here is a question for you.  My superior, just informed me today that he does
not want any more url parameters on any of our public applications. Just form
submissions for EVERYTHING.  He is concerned with security and data type issues.
I think this is a &quot;bit&quot; drastic.  What is your opinion? Do you think
eliminating URL parameters for good from an app, menu items, etc.  the best for
an application? Can everything be done this way? how effective can it be?
</blockquote>

Let me be direct. This does <b>nothing</b> for you, security-wise. A person can change form values just as much as they can change URL values. At most you will slow down a hacker, but you will do nothing to stop them. So you have to ask yourself: Is the potential <i>hours</i> of work necessary for this change worth the benefit (slowing down a hacker by about 60 seconds)? I'd say most definitely not. You could make things a bit more secure by checking the referer value, but you could do that and still use the URL scope as well. 

Anyone else seen requests like this? Anyone actually have to go through with a change like this?