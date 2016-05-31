
{
	"title": "Adding (Limited) Pagination to Hugo",
	"date": "2016-05-31T15:01:00-07:00",
	"categories": [
		"Development"
	],
	"tags": [],
	"url": "/2016/05/31/adding-limited-pagination-to-hugo"
}

This is probably only going to be useful to a limit audience but I thought I'd share. When converting my site from WordPress to [Hugo](http://gohugo.io/) I discovered that the built-in [pagination support](http://gohugo.io/extras/pagination/) was a bit problematic for my site. Why? I have a large amount of content and at the default page size, I ended up with over five hundred pages of - well - pages. 

<!--more-->

To me - the solution was simple. Just get rid of the pagination. Frankly, I rarely "page back" to see older content. Heck, I rarely visit a blog's home page anyway. I'm typically on a blog because of a Google search result. Recently though I found myself trying to get links for my own content from a week or so ago and wanting to do a bit of paging. I did some basic research into how I could add pagination, but only for a limited subset of my content, say five pages or so. This is how I did it.

First, I edited the main pagination partial. My copy was blank as I didn't want pagination at all, so I copied the version from my theme and added a bit of logic. 

<pre><code class="language-javascript">
{{ if lt .Paginator.PageNumber 5 }}
	&lt;nav id=&quot;page-nav&quot;&gt;
	{{ if or (.Paginator.HasPrev) (.Paginator.HasNext) }}
		{{ if .Paginator.HasPrev }}
			&lt;a class=&quot;extend prev&quot; rel=&quot;prev&quot; href=&quot;{{.Paginator.Prev.URL}}&quot;&gt;
				&#x00ab; {{with .Site.Data.l10n.pagination.previous}}{{.}}{{end}}
			&lt;/a&gt;
		{{ end }}
		{{ if .Paginator.HasNext }}
			&lt;a class=&quot;extend next&quot; rel=&quot;next&quot; href=&quot;{{.Paginator.Next.URL}}&quot;&gt;
				{{with .Site.Data.l10n.pagination.next}}{{.}}{{end}} &#x00bb;
			&lt;/a&gt;
		{{ end }}
	{{ end }}
	&lt;/nav&gt;
{{ end }}
</code></pre> 

Even if you've never seen Go templates and Hugo before, you can probably figure out what's going on here. My change was literally just the IF condition wrapping the logic. I chose 5 as the total number of pages but you could use any number here. 

The next change was in the article_list partial. My code was initially this:

<pre><code class="language-javascript">
{{ range first 10 (where .Site.Pages "Type" "post") }}
</code></pre>

Again - I assume if you've never seen Go/Hugo before you can guess as to the logic here. The default code uses pagination and had looked like this before I removed it:

<pre><code class="language-javascript">
{{ $paginator := .Paginate (where .Site.Pages "Type" "post") }}
{{ range $paginator.Pages }}
</code></pre>

So my goal was to bring pagination back, but to limit it to the subset of posts that would be covered by the 5 pages of content I wanted to support. Here is what I came up with:

<pre><code class="language-javascript">
{{ $paginator := .Paginate ((first 50 (where .Site.Pages "Type" "post"))) }}
{{ range $paginator.Pages }}
</code></pre>

Obviously that's a bit of a hack. In theory I could use a site-wide variable and handle both parts dynamically, but for now, this is what worked for me. 

Actually, it didn't quite work. It seemed fine when I tested, but when I generated my static output, I was getting a huge amount of additional pages due to pagination. I [posted on the forums](https://discuss.gohugo.io/t/restrict-pagination-to-x-pages/3437/2) and actually got support from the developer who implemented pagination for Hugo. That's what I call good support!
