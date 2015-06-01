# Microservices at orbitz


## History

- circa 2000, typical web app, web app that communicates with a business layer
  - business layer was the existing travel backends... I'm guessing mainframes

- 2004, switched to services model
- 2012, platform constantly evolving
- today, multiple brands, multiple sites, hundreds of apps, thousands of instances

- ended up with a bunch of monolithic services instead of one giant monolith
- process was bogging them down

## Docker

- they use consul for service discovery
- docker doesn't really have disk, so had to figure out how to deal with that
- use ELK for log forwarding
- beware port stuff with docker... need to register its external port with consul
- graphite for monitoring
- marathon and mesos
- haproxy sitting in front of docker-based web services
- open source project called bamboo to deal with port mapping stuff, rewriting haproxy configs on the fly
- they wanted to enable faster service development and deployment, enable teams to own their stuff in prod, and trivialize the idea of a release

## Jenkins, docker, ansible, marathon

- starts with their microservice generator. They use yeoman
- yo microservice
- humans must review pull requests
- jenkins bot merges into master once another human approves the PR

- most of their jenkins slaves run in mesos and our docker slaves
- they use job-dsl-plugin to build their pipelines
- create jar files with the build number (via envinject plugin) to make it easy to trace jar to jenkins build
- then grabs a docker image and adds the jar; this emits a docker image that's tagged with the unique version
- docker image published to artifactory
- they use ansible as the engine for deployment
- they don't want apps to care about environment specific stuff
  - so ansible passes in app-specific env vars: consul_host={{ansible_fqdn}}
- health checks are very important for these types of rolling deploys
  - they use spring boot, which has health checks out of the box
- once the new docker image comes alive and health checks are good, it should gracefully undeploy the old version


### how to handle failures?

- what if there's a failed or partially failed deployment?
- what happens when a VM moves?
- what if we need to add capacity, i.e. deploy a microservice to lots more hosts?

- so they kind of started over
- went with marathon, and they use ansible to work with marathon, using a custom ansible module they wrote
- ansible doesn't have to worry about hosts now, just clusters
- ansible talks to marathon via its http api, BUT: that API is async, so they had to build in logic into their module to deal with that, basically: "wait till deployed" because async doesn't work well in a pipeline
- now they do a blue-green deploy
  - both the old and new docker image are running
  - give marathon the health endpoint to hit
  - then the old version is gracefully shutdown and deploy
- deploys happen to the entire cluster in parallel, not serially
- yeah... they rely on marathon to do a lot of the heavy lifting
- they're now deploying to about 20 different environments in about 10 minutes

### smoke / acceptance testing

- they encourage unit tests over post-deploy acceptance tests
- they wrote a little framework to let them do acceptance testing across a cluster

### paper trail

- because they have pipelines, they were able to skip the manual approval process in Service Now
- instead, they auto-register a ticket in service now and then close it via jenkins, too
