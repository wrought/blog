title: WNDW and Pandoc Conversions
date: 2013-11-09 06:14:06
tags:
- wndw
- pandoc
- conversion
- odt
- html
- markdown
- mediawiki markup
- wikisource
- wireless
- ict4d
- mesh
- sudo mesh
- peoplesopen.net
---

Thanks to [tunabananas](http://twitter.com/tunabananas)' adventures in Berlin, I got to pick up a physical copy of [Wireless Networks in the Developing World](http://wndw.net/) (WNDW). The book is a complete guide to running wireless networks in a variety of environments, including: background knowledge, regulatory information, technology resources, and community resources from experts in creating and maintaining these networks. It's an excellent source that I highly recommend to anyone interested in internet, wireless, mesh/local networking, community utilities, and information and communication technologies for development (ict4d).

Further, you are entitled to copy, share, and remix the book since it is released under a [Creative Commons Attribution Share-Alike (cc-by-sa) license](http://creativecommons.org/licenses/by-sa/3.0/), so long as your derivative work uses the same license (others can do the same to your version). 

I was disappointed to find that the [wndw.net](http://wndw.net/) website hosted only PDF and ebook formats, with no source files. With this opportunity and liberty of a permissive license, I did the following:

* Obtained a source copy of the book \([.odt](https://github.com/wrought/wireless-networking-in-the-developing-world/blob/master/src/WNDW_UsTrade6_master%231.42.odt)\) from lead editor [Jane Butler](http://networktheworld.org/).
* Used LibreOffice to export an HTML format of the book \([.html](https://github.com/wrought/wireless-networking-in-the-developing-world/blob/master/src/WNDW_UsTrade6_master%231.42.html)\).
    * This version is generally fairly good, including MathML for the equations and mathematical statements, but there are some formatting issues, namely in the Glossary.
    * Also created a simpler copy to clean and improve the HTML \([.html](https://github.com/wrought/wireless-networking-in-the-developing-world/blob/master/wndw.html)\) which includes MathJax JavaScript from the mathjax CDN to format MathML into beautiful mathematical representations. 
* Used [Pandoc](http://johnmacfarlane.net/pandoc/) to generate a MarkDown version based on the HTML format \([.md](https://github.com/wrought/wireless-networking-in-the-developing-world/blob/master/wndw.md)\).
    * This version is actually really clean, *except* the math and tables, which need to be reformatted.
* Used Pandoc again to generate a MediaWiki format based on the MarkDown format \([.wiki](https://github.com/wrought/wireless-networking-in-the-developing-world/blob/master/wndw.wiki)\).
    * Then, I posted the MediaWiki version [on WikiSource](https://en.wikisource.org/wiki/Wireless_Networking_in_the_Developing_World), along with a PDF [on Wikimedia Commons](https://commons.wikimedia.org/wiki/File:).
    * The MediaWiki version still needs math and images to be added and uploaded respectively.

## Community Editing

Now there's a few versions, but especially a [MarkDown version of WNDW available](https://github.com/wrought/wireless-networking-in-the-developing-world/blob/master/wndw.md) tracked with git and hosted on github for folks to [fork](https://github.com/wrought/wireless-networking-in-the-developing-world/fork), edit, and [submit pull requests](https://github.com/wrought/wireless-networking-in-the-developing-world/pulls). This is an opportunity to engage with the wider readership of WNDW in order to incorporate edits directly, which can filter up to formalized versions, as well as this web version.

## @TODO

There's [a stack of issues on github](https://github.com/wrought/wireless-networking-in-the-developing-world/issues) to handle all the opportunities and tasks associated with converting and sharing this document far and wide!

