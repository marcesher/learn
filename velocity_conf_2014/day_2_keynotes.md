# Scott Hanselman

- Basically, funniest keynote ever. Go watch it.


# Appium

Jonah Stiennon

Appium is like selenium but for controlling mobile devices

Runs the actual code you're going to ship to the app store

OK, this is pretty awesome

Appium runs like a selenium server, looking for http requests

Has a bunch of client libraries (ruby, java, javascript, etc)

# Lessons learned from pagespeed

Josh Marantz, google

- look into modpagespeed for apache
- ngxpagespeed for nginx

## it's not just the speed, it's the UX

  - mobile page speed can give UX tips

## mobile matters more

  - mobile sites need to run fast

## compression counts

  - gzip!
  - modpagespeed does this automatically

## caching counts

  - harder, though, because you need to update static assets
  - this is why you need automated tools

## dive into the details

  - run webpagetest religiously

## look at the html

## basic image compression matters

  - modpagespeed default compression can significantly reduce jpeg files

## Use real user monitoring (RUM)

  - use modpagespeed to set up experiments.... send x% of traffic to different configurations

## use tools

- ngxpagespeed.com
- modpagespeed.com
- atsspeed.com
- iispeed.com


# mobile web is not just a technical challenge

Lara Swanson, etsy

laraswanson.com/culture

They did not want an "m." mobile subdomain.

everything had to be on the regular URLs

team got together to mobilize all the things

But building desktop parity is hard

Engineers outside of the mobile dev team hated dealing with it

dictum came down: "everyone works on mobile web"

so they disbanded the mobile web team, and...

Mobile web basically stagnated for a year

Lara came on to try to fix this

Tried lots of things, but none of them worked

Feature teams still weren't mobilizing anything

They realized they were trying to solve a cultural problem with just technology

 - tools weren't the solution, and neither was just telling people "go do mobile web"

Turns out, the Performance team helped the feature team achieve a cultural shift

1. perf team educated feature team coworkers about importance of performance
1. partnered with other teams to build tools to show affect of performance on business metrics
1. Incentivizing coworkers: Seth walker's performance report on the public blog
   - devs banded together with the perf team to fix a glaring problem on the home page, which was surfaced by seth's first perf report blog post
   - they celebrate big performance wins

1. the perf team empowered devs at etsy to do site speed well


So how can they apply this to solving mobile web's culture problems at etsy

- educating coworkers... more lunch and learns, internal presentations
    - educate feature teams about how to do mobile web performance
    - workshops on how to test on mobile
    - lunch and learn on how to design for touch

- incentivizing coworkers

  - they built a badass device lab
  - put up some dashboards to show mobile traffic % (put on monitors) to show devs that the work they do on mobile matters


Their success metrics:

 - caring
 - shipping
 - teaching


You need to know your success metrics and decide which of them people aren't aligned

Sometimes it's hard to see what you're blind to


# sitespeed.io

Peter Hedenskog

- cmdline tool you can run against your site, in multiple browsers
- will crawl the site to the depth you give it
- emits a number of really useful looking reports, at the page level
- releasing 3.0 in a couple of weeks
  - completely rewritten using node
  - can collect data from pagespeed, webpagetest

# Using fiddler

Eric Lawrence, telerik, creator of fiddler

