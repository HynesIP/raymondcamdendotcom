{
	"title": "Spry 1.4: Tabs",
	"categories": [
		"Misc"
	],
	"tags": [],
	"date": "2006-12-18T09:12:00+06:00",
	"url": "/2006/12/18/Spry-14-Tabs",
	"guid": "1721"
}

I've blogged about the tabs in <a href="http://labs.adobe.com/technologies/spry/">Spry 1.4</a> before, I even built a <a href="http://cfspry.riaforge.org/">ColdFusion wrapper</a> for the earlier code. However, now it is "officially" released. I've updated the <a href="http://www.coldfusionportal.org">ColdFusion Portal</a> to use the Spry tab code. I'll also be replacing the tab code in <a href="http://www.blogcfc.com">BlogCFC</a> as well. For a quick example of how easy it is to use the tab code, here is the sample code that ships with Spry (so in other words, apply the big old Adobe copyright to this code):

<code>
&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml"&gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" /&gt;
&lt;title&gt;Spry Tabbbed Panels&lt;/title&gt;
&lt;link href="SpryTabbedPanels.css" rel="stylesheet" type="text/css" /&gt;
&lt;script language="JavaScript" type="text/javascript" src="SpryTabbedPanels.js"&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;p&gt;&lt;/p&gt;
&lt;div class="TabbedPanels" id="tp1"&gt;
	&lt;ul class="TabbedPanelsTabGroup"&gt;
		&lt;li class="TabbedPanelsTab" tabindex="0"&gt;Tab 1&lt;/li&gt;

		&lt;li class="TabbedPanelsTab" tabindex="0"&gt;Tab 2&lt;/li&gt;
		&lt;li class="TabbedPanelsTab" tabindex="0"&gt;Tab 3&lt;/li&gt;
		&lt;li class="TabbedPanelsTab" tabindex="0"&gt;Tab 4&lt;/li&gt;
	&lt;/ul&gt;
	&lt;div class="TabbedPanelsContentGroup"&gt;
		&lt;div class="TabbedPanelsContent"&gt;Tab 1 Content&lt;/div&gt;
		&lt;div class="TabbedPanelsContent"&gt;Tab 2 Content&lt;/div&gt;

		&lt;div class="TabbedPanelsContent"&gt;Tab 3 Content&lt;/div&gt;
		&lt;div class="TabbedPanelsContent"&gt;Tab 4 Content&lt;/div&gt;
	&lt;/div&gt;
&lt;/div&gt;
&lt;script language="JavaScript" type="text/javascript"&gt;
var tp1 = new Spry.Widget.TabbedPanels("tp1", { defaultTab: 2 });
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</code>

You can see more examples <a href="http://labs.adobe.com/technologies/spry/samples/tabbedpanels/tabbed_panel_sample.htm">here</a>.