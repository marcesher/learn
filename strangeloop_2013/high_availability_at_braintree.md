Paul Gross
@pgr0ss
pgrs.net

High  Availability at Braintree


# Why is uptime important to braintree

- they process 10 billion annually
- 19K per minute for their merchants
- if they go down, their merchants look bad and it loses them a lot of money


- check out high_availability page on wikipedia for "nines"

- 5 9s: 5.26 inutes per year
- he says 5 nines is "unbelievably difficult"

# 3 causes of downtime

 - planned maintenance
 - unplanned failure
 - people mistakes

## planned maintenance

 - code deploys
 - ruby on rails app
   - in early days, put up maint page, deploy, run db migrations, take down maint page.
   - basically down for the entire time of the deploy
 - switched from mysql to postgres
   - ddl migs are very fast
   - add indexes without locking tables, using "concurrently" keyword
   - transactional DDL
   - see the link in his slides for how to migrate from mysqlto postgres

 - new deploy:
   - add new tables and columns, roll out new code server by server, add indexes
   - zero downtime
   - they added 2 new migrate tasks: migrate_pre and migrate_post
 - one problem:
   - rails caches columns when it starts
   - means you can't actually delete columns
   - can't drop columns in a post migration
   - need to tell rails to forget columns
   - so they added a deleted_columns property to Rails models and some other whacky rails hooey
   - important: they don't delete columns right away, so that they can always roll back at least one release

 - they runmultiple versions of the code at once
   - consequence of doing server by server deploy
   - fine for most features since most features or additive
   - feature switches for when it's not OK (dark deploys)
   - they feature switch almost all new features
   - this also helps prevent need to roll back

### Limitations with this approach
 - column renames... they generally don't do it
 - database failover
 - other infrastructure changes
 - they essentially wanted a way to pause traffic

## Broxy

 - Braintree Proxy
 - Python / Tornado app (evented)
 - Accepts web requests from apache and feeds them into a redis queue
 - on the way back, it reads the response from redis and sends back to apache

 - Dispatchers
   - lightweight rack adapter
   - takees requests from redis
   - processes them through rails
   - still use rails, but via a queue rather than a webserver

### Suspend traffic

 - suspend the dispatchers
 - lets requests queue up above the dispatchers
 - they can then do db maintenance, etc
 - when done, they restart the dispatchers and it processes the queue
 - consequently, users see long running requests, not failed requests
 - maybe from 2 sec to 20-30 seconds
 - they try to keep maintenance downtime to less than 30 seconds
 - because they provide the client libraries, they can build intelligence into them b/c the clients know about the fact that these things happen

## Summary:

- pre and post migrations
- rolling deploys
- postgres b/c it's fast for ddl
- broxy to pause traffic


# Unplanned Failures

- servers will fail, networks go down, etc

## Server Failure

 - Load balancers
 - they built their own; they don't like big black boxes, and load balancers are that
   - LVS / IPVS -- kernel level routing
   - use pacemaker
   - BigBrother and LitmusPaper

 - BigBrother
   - runs on load balancer
   - checks status of backends
   - update ipvs rules based on results of status checks

 - LitmusPaper
   - runs on backend servers
   - queried by bigbrother via http
   - returns a health level, which is a scale
     - for example, maybe the app is up but cpu is spiked, so it returns a lower health level
   - so it's the corollary to BigBrother

### Stateful Services

 - load balancers and postgres clusters
 - use pacemaker to manage failover
 - the do a lot of virtual IP monkeying

## Network failure

 - internetpulse.com
   - shows status of services in ISPs
   - very cool!

 - Networking - inbound

   - BGP routes traffic through multiple ISPs and data centers
   - use Pingdom to test connectivity
   - I **really** need our systems engineering guys to watch this

 - Networking - outbound

   - Braintree also talks to other vendors... check credit card validity and balance, etc
   - they connect to many processing networks
   - ISP outages are usually partial
   - sometimes, they can't reach every endpoint on all of their ISPs
   - needed a way to choose an ISP per processing network
     - use the best ISP for that path
   - **Processor proxies**
     - instead of connecting directly, they connect through proxies
     - one proxy per tcp endpoint
     - **Mallory** is what they built
       - python/tornado
       - proxies requests
       - SSL verification, not just encryption
       - Acts like LitmusPaper, and BigBrother can directly query it
       - github.com/braintree/mallory

 - Connection Failures

   - let things heal
   - then retry request because they know that, for example, the healthcheck will show low health and mallory will eventually route around it

 Summary

   - load balancing
   - redundancy across isps
   - let system heal and retry again

# People make mistakes

 - they can cause outages
 - they can exacerbate existing issues
 - they want to reduce the people factor to the degree possible, knowing it's not possible to completely eliminate it

## Automate everything

 - reduces errors
 - speeds up processes
 - less fiddling around in production
 - capistrano and puppet


## Safeguards

 - dangerous tasks refuse to run in production
 - can't drop the prod database, for example
 - prompts include environment name
   - says in Red letters: "production"
   - green letters for dev
 - read-only database and logs

## Monitoring

 - Nagios
 - lots of custom checks... did nightly thingie run successfully, eg
 - hooked into PagerDuty
 - Multi-app log tail (with sampling)
 - use tmux, split vertically, with commands you'er running on the left and logs on the right
 - Graphite and munin for graphing
   - started with munin, moving everything to graphite
 - keep an eye on the monitoring while you'er doing the work
 - huge point here: you want to knwo right away if you screwed something up, so the graphs and pagerduty should alert you right away, while you're still there in the terminal so you can fix it before more damage is done


# Takeaways

- this kernel level load balancing is **very** interesting
- create staging environments just like production and pratice all this, including causing outages
- I need to go back through all these notes and, one by one, compare them with what we have in place at work and see where it makes sense to explore. For example, pingdom and external availability
