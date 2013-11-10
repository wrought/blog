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

Thanks to [tunabananas](http://twitter.com/tunabananas)' adventures in Berlin, I got to pick up a physical copy of [Wireless Networks in the Developing World](http://wndw.net/) (WNDW). The book is a complete guide to running wireless networks, including background, regulatory information, technology resources, and community resources from experts in creating and maintaining networks in a wide variety of locations. It's an excellent source that I highly recommend to anyone interested in internet, wireless, mesh/local networking, community utilities, and information and communication technologies for development (ict4d). Further, you are entitled to copy, share, and remix the book since it is released under a Creative Commons Attribution Share-Alike (cc-by-sa) license, so long as your derivative work uses the same license (others can do the same to your version). 

I was disappointed to find that the [wndw.net](http://wndw.net/) website hosted only PDF and ebook formats, with no source files. With this opportunity and liberty of a permissive license, I did the following:

* Obtained a source copy of book \([.odt](https://github.com/wrought/wireless-networking-in-the-developing-world/src/)\) from Jane Butler.
* Used LibreOffice to export an HTML format of the book \([.html](https://github.com/wrought/wireless-networking-in-the-developing-world/src/)\).
    * This version is generally fairly good, including MathML for the equations and mathematical statements, but there are some formatting issues, namely in the Glossary.
    * Also created a simpler copy to clean and improve the HTML \([.html](https://github.com/wrought/wireless-networking-in-the-developing-world/wndw.html)\) which includes MathJax JavaScript from the mathjax CDN to format MathML into beautiful mathematical representations. 
* Used Pandoc to generate a MarkDown version based on the HTML format \([.md](https://github.com/wrought/wireless-networking-in-the-developing-world/wndw.md)\).
    * This version is actually really clean, *except* the math and tables, which need to be reformatted.
* Used Pandoc again to generate a MediaWiki format based on the MarkDown format \([.wiki](https://github.com/wrought/wireless-networking-in-the-developing-world/wndw.wiki)\).
    * Then, I posted the MediaWiki version [on WikiSource](https://en.wikisource.org/wiki/Wireless_Networking_in_the_Developing_World), along with a PDF [on Wikimedia Commons](https://commons.wikimedia.org/wiki/File:).

## @TODO

There's a stack of issues on github to handle all the opportunities and tasks.

