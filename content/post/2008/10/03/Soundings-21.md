{
	"title": "Soundings 2.1",
	"categories": [
		"ColdFusion"
	],
	"tags": [],
	"date": "2008-10-03T11:10:00+06:00",
	"url": "/2008/10/03/Soundings-21",
	"guid": "3040"
}

I just released <a href="http://soundings.riaforge.org">Soundings</a> 2.1 to RIAForge. This is mainly just a bug fix release, although it has some nice user submitted UI improvements, including visually marking required survey items. Soundings also marks the first application of mine where I ripped out cflogon. A subtle issue with it (see below) caused two clients in the past week to have issues.

So the issue isn't a bug per se, but a feature that trips me up all the time. ColdFusion's roles based security will automatically tie in to web server security. Now imagine you want to see if someone is logged in. You do this by checking getAuthUser(). (ColdFusion 8 added isLoggedIn(), but Soundings has to work in older version.) Now imagine someone deploys Soundings on an Intranet where HTTP auth is in place.

All of a sudden getAuthUser will return a value and that application will think that a user is logged on to Soundings, where in reality it was just someone logged into the <i>web server</i>'s security system.

There is no way to say "I don't care about the web server, I have my own security model." That to me makes cflogon something I just can't use. In other applications I get around this by using a session variable so I can tell that someone has logged into my application.

To be honest, this issue probably only trips up people like myself - who write applications to be used by others - but as it hit two people in one week I figured it was just time to dump it.