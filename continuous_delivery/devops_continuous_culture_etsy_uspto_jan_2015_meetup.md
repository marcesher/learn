Ryan Frantz
- Remote (Annapolis, MD)
- senior ops engineer
- @ryan_frantz


- Technology can attract people, but culture keeps them

## Core engineering principles

- every engineer can push to prod at any time
- perfect is enemy of done
- believe engineers are going to do the right thing
- ship small, ship fast
- devs *can* push at any time
- favor simplicity and speed to ship... if we fail fast, we can learn faster
- maximize learning
- 'if it moves, graph it'... "measure everything"



- pushes per day is a means, not an end


- A + B != culture
- this is etsy's story, not yours
- you can't just copy etsy's approach and bam you're awesome

## Etsy's story

- group of skaters (shows pic of ditch ramp converted to standing desk)
- realized the craft community is huge, set out to change the world by bringing crafting to everyone
- 4 person startup, grew to 30 - 35, including 15 engineers
- very siloed culture, barriers to engineering collaboration
- "Sprouter" -- "Middleware of distrust"
  - project dedicated to stopping engineers touching databases
  - didn't trust developers to run queries directly against the database

2008, management changes

- Maria Thomas, from NPR, promoted to CEO
- emphasizes community and a culture that supports community
- Chad Dickerson comes from flickr to be CTO
- brings clear focus to engineering, drives to cut out silos. starts to kill sprouter

- 2006 to 2008

- lots of downtime
- low-impact engineering projects
- lots of firefighting

2009 Internal Improvements

- daily standups between dev and ops... this was tough because they're time consuming, need to get people together, etc
- but better than an absence of it b/c before that people weren't talking
- this was as much about dev team taking responsibility for their code in prod

- devtools team
  - deployinator
  - moved to apache
  - solidified network

2010

- allspaw, kellan mckree, both from flickr. shored up engineering team
- launched code as craft blog
- standardization and graphs
- moved to php and mysql for *everything*... got rid of snowflakes (mongo, etc)
- because it's php, they have a low barrier to entry for finding talent (!)
- 'if it moves, graph it'

## 2010 Ideals

### Management Ideals

 - blameless postmortems
 - 1:1s as core mgmt tool
   - these shouldn't be unidirectional
   - reports should feel empowered to ask manager questions, bring up problems, etc
   - he encourages 1:1s with other parts of the orgs, other teams
   - he encourages an hour because with a half hour, it becomes just a checklist. thinks 30 minutes isn't enough momentum
   - suggests shaking it up occasionally; get out of office, go for coffee
 - engineering career planning
   - people who set goals are more likely to be successful
   - so they make it clear what it takes to the next level... here's the roadmap

### Engineering Ideals

 - developer on-call
   - page dev directly; no need to go through ops first
   - devs actually wanted this; didn't want to need to go through ops first
 - a/b testing
 - feature flags and ramp up
 - schema change thursday
   - used to have a lot of schema changes, and that caused a lot of problems
   - so they limited it to 1 day a week
   - use schemanator to stack up schema changes; and makes it really easy to see all the changes for the database;
      making it easier to spot problems (hey, you're missing an index), unnecessary or duplicate changes, etc

## 2011 highlights

 - sprouter gone
 - nonstandard tech removed from productions
 - engineers receive 3 annual goals
   - speak at a conference
   - write  a blog post
   - release open source software


 - Org changes
   - Chad to CEO, Kellan to CTO, Allspaw to SVP Ops

 - lots of open source: statsd, logster, deployinator, supergrep, schemanator
 - automation and config management
 - security front and center
   - how to implement security without negative impact to culture

## 2011 - 2012 - focus on security

 - DevOpsSec
 - security alongside dev & ops as being integral to culture
 - applying core principles and learnings to security
 - emphasis on security being a facilitator and not a blocker
  - "you're only a blocker if you're the last to know"
  - not uncommon for security to be on the fringe because they're perceived as the folks that say No
 - build a human and effective security organization
 - with etsy, security is never "just no"... it's always "here's a way around it"

## 2012 - growth + foster our values

 - major changes around product
   - more internationalization
   - high impact products (shipping labels, gift cards)
 - explosive hiring, allow easy team transfers
 - became a B-Corp (benefit corporation)

 ### B-Corp?

   - aim to use business to solve social and environmental issues
   - impacts engineering
     - waste, recycling, compost, flushes (haha. not directly. they know how much water they're using)
     - efficiency of tech, data center usage, and partners
   - 'make the world more like etsy' -- extend the culture


## 2012 technical achievements

 - wholly separate payments environment
   - allows pci compliance without disrupting culture
   - interface with the web stack via a restricted internet facing API
   - keeps the payment part separate, easy to reason about

 - although regulation governs process, it doesn't mean it needs to govern productivity

 - serious about data science
   - hadoop cluster... moved off of AWS and onto own infrastructure for cost savings; full time data scientists
   - taking some chances and broadening of engineers


## 2013 - an interesting year

 - many of the hard engineering problems already solved
 - time to focus internally
 - no one engineer can learn everything any longer
 - focus on internal tooling

 - **Morgue** - used to capture post mortems, including IRC logs, images. Really helps capture timeline of an event
 - **Opsweekly**: categorize and report nagios alerts
 - **Superbit**: querying of vertica, elasticsearch, big data by anyone who knows sql
 - **Catapult**: communicates experiments and related metrics, including conversion impact
 - begin a refocus on mobile / api first product vision

 "Designated Ops"

   - ops engineers out onto other teams
   - visibility of ongoing projects
   - advocating for engineers
   - assignemnts rotate annually
   - builds tight relationships with folks on engineering teams


## 2014 - Org changes

  - everyone pushes on first day... not just engineering
  - yearly planning is restructured (planning is ongoing)

  - cultural acquisition
    - Paris based A Little Market (ALM)
    - integrating another engineering culture can be tough
    - language, timezone, human capital differences
    - can be successful, but don't understimate

  - technical:
    - from splunk to elk stack
    - mobile first
    - api first
    - technical work for quality of life: on-call sleep tracking


### ELK Lessons

 - communicate the hell out of it
 - technology can find its way into unexpected corners of the stack


## Conclusions

0 culture takes continuous work
- don't let potential changes like growth and security negatively influence culture. make them work
- never stop pushing