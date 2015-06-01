# Mark Maun, ticketmaster, How Tools shape culture

- huge org, lots of teams

## opaque code

- opaque code, siloed deployments, fragmented ownership
- getting access to code was impossible
- people locked out from the beginning
- this was in subversion

- the point isn't "use these tools", but "use tools that work for your org"

### solution

- so they switched to gitlab
- increased transparency, integrated code review and merge requests
- group ownership
- this is a simple example of how switching from one repo tool to another dramatically changed their culture because it increased collaboration and transparency

## siloed deployments

- bad game of telephone, with handoffs. the people writing the code were not the people deploying the code
  - dev to qa to ops
  - "we even had a CAB"
  - they'd hand the ops guy a printed out doc with deployment instructions; did not work. still deploying the wrong thing
  - ad hoc executions
  - no uniform delivery platform across teams
  - no ownership. if the deploy didn't work, that's ops' problem

- lack of control (scheduling, quality)
- poor throughput
- lack of ownership

### solution

- they started using Rundeck
- simple tool that was what they needed. nothing fancy
- Mark wanted to use it on all projects; the vast majority of projects didn't know about it or care
- this was just in pre-production, not even prod yet. but it was a good step for them and they were proud of it
- then they hooked it up to jenkins, so jenkins did the build and rundeck did the deploy
- This was a safe way to self-service deployments; this solves the handoff problem

**prod adoption**

- forgiveness not permission
- got slapped on the hand, but not a big deal
- pick low risk projects
- buy in from early adopters
- empower others to use it
- evangelize success

**results**

- engineering holds the keys to deploying to prod, because they now have tools to enable them to do it safely and securely
- control over scheduling
- bandwidth issues erased
- you deploy it, you own it

## Fragmented ownership

- monitoring tools were system focused, not application focused
- no access for non operations
- no application integration
- no business metric monitoring
- developers not always in escalation path
- lousy mttd and mttr


### solution

- ZAbbix
- upload via zabbix api to on-board alerting
- node discovery
- metrics, thresholds, triggers
- healthcheck alerts
- wanted a simple dashboard that people could actually understand
- product and app owners could configure their alerts (via a text manifest)

- "organic alerting": where someone calls the helpdesk to let you know something's wrong
- engineers now fully on the escalation path
-product owners control the monitoring
- enabled a performance and ownership culture


## some other tools

- gatling for performance testing
- metrilyx for data visualization
- opentsdb for time series data
- cucumber for bdd functional tests

# Impacts

- improved collaboration between teams
- increased developer ownership
- greater visibility into production
- increased confidence in products
- greater focus on business value

# Takeaways

- tools steer behavior
- focus on the true believers first, not the skeptics
  - if you get the first 10%, the 80% will come on if you make it easy
- they didn't have an executive mandate, but it'd have been nice
- fail early, in preproduction