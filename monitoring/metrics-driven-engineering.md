http://www.slideshare.net/mikebrittain/metrics-driven-engineering

http://www.usievents.com/en/conferences/12-paris-usi-2013/sessions/1079-metrics-driven-engineering

Mike Brittain

## Process

At the lowest level of monitoring:

System metrics:

 - Are the servers and network OK?
 - how many queries per second?
 - what's the total outgoing bandwidth?
 - these things should be relatively stable


App level metrics

 - how long does photo resize take, eg?

Business metrics
 - how many transactions per minute?

Time-series data show anomalies, etc

Etsy builds small distributed teams
And they give those teams tools to gather metrics

These trendlines also help identify candidates for performance improvement

Metrics help you identify goals and problems

- All engineers ship code
- First day at etsy, an engineer ships
- How do they support this?
  - First day: you put yourself on the website
  - Second day is when you do your insurance forms

They make deployments and testing so that they are as simple as possible

 - single button for each
 - takes about 15 minutes for the process, 90 for code to get to prod

- 50 deploys a day

This looks crazy and unsafe

- Metrics are key to safeguarding this

They also do code and architecture reviews

- thousands of unit tests
- also have functional test

"Failure is not an option"

  - This is **not** the approach at Etsy
  - Failure is expected. Failure is inevitable

Metrics help engineers understand the impact of the changes they're making from front to back

Dashboards are always in front of people

**Open Access** of data

- metrics are on the walls
- cross-team exposure to metrics


**Who's going to build all of this stuff?**

 - At Etsy, engineers build these things
 - This is devops... shared responsibility
 - logging, graphing, trending, alerting
 - metrics are a part of every feature
 - part of developing a feature is deciding what metrics you need to collect


## Tools

Simple, open source tools

**Ganglia**

  - used for collecting data from servers, networks, and applications
  - it is cluster oriented
  - not as friendly for individual app metrics
  - gmetad -- write your own custom metrics
  - community submitted metrics you can use

**Graphite**
 - get tremendous use out of graphite
 - more positioned toward individual application metrics
 - create new metrics on the fly
 - customize via URLs and display functions

Log Formats

 - getting the format right is very important so you can get the right data from your logs
 - **Apache**
   - they put about 30 extra fields into apache logs
   - execution time, memory consumed by php process, whether user is signed in, whether desktop or mobile, whether it's being translated into another language
   - they use a php function for doing this;  you can probably write your own

 - want richer error logging
  - their error logging has a "namespace", such as "login"
  - unique request ID
  - however, it's too much data for simply viewing (tailing)

**Logster**

 - simple log parsers
 - Run by cron
 - keeps a cursor on log files
 - output to graphite

 1. You write a logster parser (i.e. a regex)
 1. Aggregate values
 3. Send the values as metric objects to the collectors

 - Super useful if you have an app or server that already has logs
 - you can just use logster to start pulling that data together and aggregating

**Statsd**

 - names and values
 - send over UDP
 - this sends them to graphite
 - simple counter metrics
 - statsd automatically aggregates min, upper, 90th%


**Deployments**

 - During a deployment, they send a metric indicating a deployment (with a value of 1)
 - eg "events.site.deployed:1"
 - then, by using a URL function in graphite, you can turn that value into a vertical line
 - this lets you correlate events with trendlines
 - Sometimes (often?), they won't catch something in a test, but a metric will catch it
 - they also use absence of vertical lines: if an increase in a metric doesn't correlate with a known event (such as a deployment)
  - helps answer the question "should we be looking at different systems?"


**Dashboards**

 - you want to aggregate graphs and put them together
 - look at Etsy's dashboard code github.com/etsy/dashboard
 - Easy to create new dashboards
   - doesnt' matter how pretty they are
   - what matters is that time frames are consistent
 - monkeying with dashboard urls is hard
 - so make it easy to exposing an API for dashboarding

**Automatically monitoring graphs**

 - use graphite URLs to get raw data
 - curl + graphite URLs + nagios == ability to start paging on anomalies
 - Business metrics + confidence bands == alertable


Closing

- add metrics to get visibility
- make metrics accessible
- make them required for all features that go out
- make it dead simple for engineers to add to application
