title: Semantic MediaWiki API Web Maps
date: 2013-11-01 04:45:36
tags:
- mediawiki
- semantic mediawiki
- semantic mediawiki api
- api
- maps
- leaflet
- geojson
- hackerspaces.org
- hackerspaces
- residencies
- exchanges
- open street map
---

Working on a [new feature](https://github.com/chgrp/ba/issues/1) for BACH, the Bay Area Consortium of Hackerspaces, home page at [ba.chgrp.org](http://ba.chgrp.org/), which is hosted [on github](https://github.com/chgrp/ba).

The goal is to embed a map of global hackerspaces offering residencies and exchanges to give context to the value for groups in the bay area to participate in residencies and exchanges as well.

[David](twitter.com/dcht00)@TODO of [Cyberhippietotalism](http://hackerspaces.org/wiki/Cyberhippietotalism) added some maps and data queries to the [hackerspaces.org](http://hackerspaces.org) wiki pages on [Residencies](http://hackerspaces.org/wiki/Residencies) and [Exchanges](http://hackerspaces.org/wiki/Exchanges).

Hackerspaces.org happens to be the largest live implementation of [Semantic Mediawiki](semantic-mediawiki.org) (SMW), an engine that enables more powerful storage and retrieval of data saved in a [MediaWiki](http://mediawiki.org) wiki (the same software implemented on the Wikimedia foundation projects, built originally for Wikipedia). 

Excellently, SMW provides a default API that allows for programmatic access.

You can see the [help doc](http://hackerspaces.org/w/api.php) from the implementation on hackerspaces.org.

I took the same "ASK" queries from the Residencies and Exchanges pages to construct API queries like this:
<pre>http://hackerspaces.org/w/api.php?action=askargs&format=jsonfm&conditions=|Category:Hackerspace|exchanges::!no|hackerspace%20status::active|&parameters=|%3FHas%20coordinates|Location::!null|limit=500|format=map|width=1100|height=480|zoom=2|center=16%C2%B0%20N,%207%C2%B0%20E|markercluster=off|&printouts=location</pre>

Unfortunately these queries took some massaging. The ASK syntax is already unintuitive, but further, the api documentation is lengthy and a bit inconsistent. On the other hand, at least this is possible!

I had previously poked at a feature like this for BACH&mdash;inspired by the Swiss hackerspace community: http://hackerspaces.ce?

However, this application requires a server-side component, which is unnecessary here.
