## Secrets Management in AWS -- Emmanuel Apau

Typical secrets solution involves using some kind of vault... app talks to vault, gets secret, uses secret

Problem: SO many vault solutions

He's demoing AWS Parameter Store (underneath "AWS Systems Manager")

- supports versioning, expiration, history, "last modified user" (i.e. user auditing)


Key Management Service (KMS): way to make customer-managed keys; encrypts your secrets that are stored in Parameter Store

- integrates with IAM

Emmanuel uses a key for dev, key for stage, key for prod, and sometimes you need a global key


There are API limits for parameters

Standard and Advanced types of parameters, each with different limitations

AWS Secret Manager

- different from parameter store
- big benefit: in-built rotations so you don't have to roll your own
- pricing is per secret, and per 10,000 API calls
- emmanuel suggests that secret manager is only useful when you need rotation; otherwise use parameter store


How to use in your app

- SDK
- on ec2 host startup, via user-data to store secrets as environment variables (he has an example, pretty slick)
- ECS task definitions has in-built integration
- Kubernetes - sounds like he's saying that it's kind of hard to use so use the k8s built-in secrets stuff (?) because otherwise you have ot build your own synchronization between aws parameter store and k8s secrets

Secrets Tips
- diversity of secrets per environment... use different secrets per environment
- fine tuned decrypt access roles for admins, devs, pms
- share secrets via secure channels
- use temporary credentials where possible, eg token based rds authentication
- make sure everyone understands the secret management process


Enforcer-Reloaded CLI
- AWS SSM parameter store management CLI
- Emmanuel created this it seems
- so that you don't have to use the AWS GUI
- kubernetes synchronization helper function (to address the k8s problem above)

- github.com/kave/enforcer
  - he forked it from his old job at upside travel



## Moving to Containers at Enterprise Scale - Latha Nagaraj

She's sharing finra's "enterprise scale container migration journey"

They moved to containers because:
- easily portable apps
- cost efficient, esp compared with traditional ec2 and autoscaling
- faster, esp for builds/deploys
- developer productivity, due to environment parity
- simple and lightweight, i.e. devs could maintain a dockerfile and compose file

Deciding what container management system to use

- first looked at AWS services... ECS, EKS, Fargate
- she's got a slide here for tradeoffs for each of these
- they chose ECS as the best fit for their needs (and their needs are pretty insane); they want to get to fargate but lack of encrypted storage is a blocker


Migration challenges
- many apps
- integrated security and compliance from the start, baked in
- automation from the start,
- support desired architecture
- rollout to dev teams

Desired architecture
- ALB on top for load balancing, which sits in front of ECS
- EC2 launch type
- ECR for registry
- a "Task" for them comprises an Identity Gateway, the app itself, and a splunk sidecar
- host uses collectd daemon
- multi-AZ deployment
- they use a custom AMI, optimized for their needs, based on a base amazon AMI; use CIS benchmark for docker security
- reusable, compliant finra base images
- app images focus on the code and configuration of the app

Infrastructure Automation
- "Provision" tool -- unclear if they built this or just use it
- has security and compliance practices built into it (she gives some examples)
- 

Delivery Pipeline
- the ECS Cluster jenkins pipeline is stored as code
- the ALB pipeline is stored as code
- the App/Service pipeline is stored as code; so they build the app docker container once and then promote it to different environments


Local Development Demo

- dockerfile, "FROM" their base image
- based on a spring boot app for this demo
- use multiple compose files that daisy chain 
- use "cloudpass" to get temporary aws token
- looks like their workflow is a build/deploy-locally workflow, i.e. not "F5" development, at least not for running the app in a local production-like way


Pipelines as code
- "F3" which they built, which is based on job-dsl; uses builder pattern
  - looks kinda similar to what we did, except java-ized
- the important thing here is that all of this is standardized... no snowflakes. If there's a springboot app, it always builds/deploys/configs the exact same way
  - this is how they're able to make standard, codified pipelines for ALB, ECS, App/Service
- 

Deployment strategies

ECS gives multiple options:

- Blue/Green via alb dns switch or target group switch
  - probabl not right option if multiple versions of the app can't deal with the same database
- zero downtime deployment with rolling upgrade

Future
- looking at fargate
- eks adoption for big data processing
- open sourcing the "provision" tool she talked about earlier, also "cloudpass" for that temp aws token, "portus" for security group management

they already have open source stuff: gatekeeper in particular, which AWS told us about earlier this year



# Recreation.gov - Martin Folkoff, SRE, booz allen

BAH hosts and builds the site; they make money when the public uses the site to reserve campsites, buy tickets, etc (i.e. transactions)

no agency actually pays bah for this; it's a new thing for booz

Started off without any legacy resources; able to use cloud, lots of resources... true greenfield

Took about a year and a half from beginning to go-live; MVP about 6 months into the project

Teams broken down by "domain"
Teams are full-stack teams; looks like they have SREs and security folks allocated to the team as "shared resources"... the "shared resources" scale up / scale down on a given domain team as needed

Domains are things like "camping", "permits", "tickets", cart/external accounts, etc. Sometimes a single team will work on multiple domains. domains can be split across the US

## Tech

- react front end
- cloudfront, route 53
- firewall
- Go for microservices backends
- EKS for hosting, with some lambda but nothing on the critical path
- Redis, cassandra, solr, rds aurora
- interesting... cassandra is the transactional workhorse, which can be problematic because it's not a transactional DB, so they had to build some things to work around that (i.e. make sure 2 people don't reserve the same campsite for the same time... 1960s style problems. lolz. )

- multi-region b/c didn't want any single points of failures
- interesting constraint: many parks don't have internet access and they work via fax, so this system sends hundreds of faxes to parks every morning telling them what their reservations are

## Integration patterns
- REST, GRPC, SNS/SQS, AWS SWF
- SWF si a "fully managed state tracker and task coordinator"
- they use grpc when possible, rest least best option


## CI/CD overview

- trunk-based development
- tech lead or some other human decides when it goes to a higher environment (i.e. dev to test to prod)
- it's all docker based, Jenkins as the CI/CD workhorse; just copies docker images from one ECR to another and then deploys to the higher environment from that higher environment's ECR

- their builds are heavily parameterized, and developers have a lot of responsibility there

## The Yosemite Story

- every year, yosemite tickets go on sale at a specific date and time. people all over the country are at their computers frantically hitting the buy button. 
- no way to autoscale for it... that's not responsive enough. They know it's coming so they have to just be prepared for it with capacity
- they have Jenkins jobs that do the work for this; scale up before the mad rush; then scan back down after it's passed

## Observability over Monitoring

- "observability lets you ask why a system isn't working"
- prometheus is a workhorse here; see his slide for the whole story though
- 

## 5 keys to reliability

- create strong domain boundaries -- contain failures
-- go get his slides for the rest



# Spoon Theory - Jamey Bash - Artemis (farming startup in brooklyn)

- core idea is that people have a finite amount of energy, and it runs out, and you never know how much someone has. 
  - the metaphor is that you have so many spoons, and you can run out of spoons, and no one can see your spoons (i.e. you don't know how many spoons someone has)
- started out in the chronically ill and disabled community
- broadened to encompass all marginalized groups
- applies to everyone, though


# DevSecOps to accelerate ATOs - Guarav Pal, CEO stackArmor

- note: i didn't take notes on this for most of the presentation. Great slides, good presentation

- Build security and compliance stuff into your CI/CD pipelines
- Infrastructure as code as a critical piece of creating secure infrastructure... repeatable, reviewable infrastructure
- product owners having some responsibility for ensuring security-related things get worked on... prioritizing vulnerability management along with other (feature) work
- it's not just the CISO's job... if you don't have security thinking at all levels the CISO doesn't matter. We hear it all the time but security is everyone's job
- Mentions choosing FedRAMP's solutions as getting you probably 50% of NIST 800-53 control "coverage". I like that "coverage" way of thinking (speaks to my former test-driven-development brain)


## New and emerging risks

- Supply Chain Risk
  - i.e. third party libraries and whatnot that your software uses
  - Josh Corman talked about this all the way back at the first devopsdays dc in 2015!
  - it's a huge problem, perhaps the most pressing
  - traditional NVD/CVE scanners do not adequately detect these kinds of issues
- Automation "exhaust"
  - code is the new "privileged user"
  - more and more humans aren't the ones doing the things that privileged users used to do
  - so the problem of ensuring that what the privileged user is doing is vetted
  - especially difficult when automation code deletes infrastructure and data and thus you lose forensics, i.e. stuff is ephemeral and could be gone by the time a security response is initiated


## NIST, ATOs, cybersecurity controls, and the Impact of DevOps on controls

- lots of controls especially around account management were created in a time when we were just talking about regular human users
- make sure roles for "cloud administrators" are adequately defined... this is the new superuser
- configuration related controls (the "CM"s) are moving away from just gold baselines and toward gold processes, configuration management

**I _really_ liked this presentation**


# Interdisciplinary Engineering - Marianne Bellotti - Auth0

- her team is called "internal services"... they go find common services that teams are using and they adopt and run them and make them shared services
  - ha... sounds like my team.

- Her key takeaway is about "Design"... design is not about making things pretty. It's about... that's the point of this presentation I think

- a huge part of design is User Expectations; how a user expects to use a system makes a big difference in how they use it and also how you maintain it

- the importance of Sensible defaults, and defaults that match the things you want users to do in production
  - eg if your docs say "don't do this in production" but then the default is to basically encouraging you to do just that in production, that default is going to win no matter what your docs say


- Talking about Feature Flags
- Introduced Gremlin, which is a type of chaos monkey
  - they set up a load test against a particular service and ran it while using Gremlin to "point a cannon at the service at the same time"
- the problem they had was that they had an internal feature flag service, and the team responsible for the service thought it was really great and robust, but the teams using the service thought it was flaky and unreliable
- so she was trying to get at 'why is there such a mismatch of perspective'
- so they sat down with teams that use the service and asked to watch them use the service
- and it came down to the fact that just using the service was an unpleasant experience; it wasn't about the actual reliability of the service as it was about the usability of the service

- User Research interviews
  - put a service in front of a user, watch them use it, ask them questions while they're using it
  - this is not a training! this isn't about you teaching them how to use something; you gotta hold yourself back from trying to show them how to do it, b/c that isn't learning
  - you're looking for confusing and misunderstanding; incorrect behavior; unpredictable outcomes

- you can do user research before writing any code... wireframes, paper wireframes, etc
- try to integrate user research into your devopsy things... it's not just about traditional features on a web app; this is about applying user research techniques to designing backend services

- "UX is a requirement for ops teams, too"

# Open Spaces Notes

- If you're running a platform-style team, treat what you do like a product... have a roadmap, communicate about it, let your platform's users know what to expect... can't just be an untransparent bug-fix shop. Think like a product manager

- K8s session... good Lord. The themes here are:
  - if people are running their own k8s or even using EKS, it's hard. 
  - many people in the room aren't using it, let alone using docker
  - lots of "they fixed that last month" type stuff
  - lots of talk of kludges, just working around problems to get things working
  - the one dude in the room who seems to have had the best time of it works at, you guessed it: Google


- platform engineering session
  - talking about what, in my interpretation, is basically what happens when you introduce a devops style team (like ours!) and then just end up creating another silo. I've been thinking about this a lot lately
  - obvious competing incentives: platform devs want the platform up / stable / etc; developers just want it to be easy to use, want more autonomy