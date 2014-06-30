# What Makes Mobile Websites Tick? How Do We Make Them Faster? Insights from WebPagetest and HTTPArchive

Doug Sillars (AT&T), Andy Davies (NCC

I'm sitting in this talk to learn more about webpagetest and HTTParchive


"head of line blocking"

  - second time i've heard this today... need to learn more

- shows examples with lots of JS requests causing blocking

- shows example of a heavy page with a lot of requests, but it has a high speed index b/c all the scripts were loaded async, at the end

- some big learnings

 - no external requests in the header was one of the key factors in getting high speed index scores
 - inline your critical CSS in the first 15K, to avoid fetching external CSS And building the css object model
 - very fast sites always compress their html
 - images are bulk of download
 - but the trend now is that fonts -- font transfer size and font requests -- are growing big time
   - but most sites don't use fonts, so how is it that the average looks so high?
     - sites that download megabytes of fonts!
   - fonts may block rendering (firefox, chrome)
   - you can lazy load fonts; cache in local storage; web font loader js; font load events api

- irony: the responsive sites tend to have about the same performance as mobile specific (think: http://foo/m)


**takeaways**

 - reduce number of requests
 - crucial to minify and gzip
 - optimize fonts if you're using them
 - inline the critical stuff and don't rely on external files to download

 download the raw data: mobile.httparchive.org/downloads.php

 or explore it in a big query

 igvita.com/2013/06/20/http-archive-bigquery-web-performance-answers
 http://bigqueri.es/

 Using WebPageTest book: bit.ly/usingwebpagetest