Gene Kim DevOps Meetup - July 23, 2013

Gene's 14 year journey… what he's learned by watching high performing organizations since 1999

Phoenix project 170 page exerpt: http://itrevolution.com/the-phoenix-project-excerpt/

# High Performers

Where did the high performers come from?
- Non-commissioned officers
- Chemical Engineer
- software auditing

Why?
- discipline and rigor

Visible Ops: Playbook of high performers

This is his journey into devops

# Act I: IT operations fixing fragile artifacts

- keeping services running on fragile infrastructure
- the tragedy of these fragile things is that they often underpin critical business operations / applications
- eventually the org becomes unable to meet the promises they make
- when we miss promises, we often compensate by making even bigger promises which we can't make

# Act 2: Developers

"show me a developer who isn't causing an outage and I'll show you one who's on vacation"

- urgent, date driven projects put into the queue, driven by deadlines / promises
- often leave no time for the downstream work centers:
  - security, deployment,QA
- resulting in one more fragile artifact in production
- deployments start taking longer


**Consequently: Ops and dev at war**

- goals aren't achieved
- Sev I incidents going up
- more firefighting

**Infosec**

- after this, nothing's left for them
- they're just making auditors happy, not helping the business
- deprived of the ability to control outcomes
- a demoralizing position for them to be in as humans and professionals

**learning: we should empathize with them**


This is the downward spiral

The IT Core Chronic Conflict
---------------------

Every IT org is pressured to simultaneously:
- respond more quickly to urgent business needs
- provide stable, secure, and predictable IT service
- "time to market will always trump availability and security"

Every Company is an IT company
- 95% of all capital projects have an IT component
- 50% of all capital spending is technology related
- Saying "IT is not a core competency" is a self delusion


When the gap between where we are and where we need to be is "IT", that's the problem

# Act 3: A Better Way

Previously, it was impossible to be fast and nimble and simultaneously reliable and secure
Points to 10 Deploys per Day at Flickr -- john allspaw and paul hammond, velocity 2009

**DevOps:**

- Ops who think like devs
  - How can we script environments?

- Devs who think like ops
  - As I'm developing, how do I ensure success, reliability, security, etc in production?
  - i.e. concerned about this software as a living thing out in the wild, not just as a feature that works on my machine
  - What must I do to ensure that my software isn't setting off pagers for ops people at 2AM?
    - What if **I** am the one on pager duty? 


High performers always accelerate away from the herd: "the best always get better"

High performing DevOps teams
----------------------------------------

More agile:
 - 30x more frequent deployments
 - 8000x faster cycle time than their peers

More reliable:
- 2x the change success rate
- 12x faster MTTR (mean time to recovery)


The Goal
=============

no book he recommends more
changed how a generation of people thought about plant operations

The Three Ways
=================
set of principles from which these devops are derived

## The First Way: Flow

- flow from dev to ops
- the left-to-right flow of work
- this is the flow through the value stream
- Understand the flow of work
- Always seek to increase flow
- Never consciously pass defects downstream
- never allow local optimization to cause global degradation
- Achieve profound understanding of the system

Questions:
What is your lead time for changes? (how long does it take to go from code committed to code successfully running in production?)


Root causes of failures:

- first time code was deployed in an environment like production
- this is the first time the code was married to its environment

Countermeasure: ops must be able to deliver environments on demand which mirror their ultimate deployment environment

- make sure devs build the code and environment at the same time
- create a common deployment environment

Change the Agile sprint policy:

"at the end of each sprint, we must have working code and the environment in which it runs"

What agile nailed was: "large batch sizes kill"

the goal is to shrink batch sizes

Deploy Smaller Changes, More Frequently

- decouple feature releases from code deployments
- Require all developers check code into trunk daily, at least
- practice deploying smaller changes, which dramatically reduces risk and improves MTTR

Facebook Chat story:
- they tested the chat service for a year, even though it was not live for users
- the browser would send fake chat messages to the server
- so by the time they deployed, they had a year of experience with chat
- They built the chat service in erlang, with which they had little experience, so this also gave them a year of experience with a new technology, even though users weren't using it for real

Breaking the Bottlenecks in the flow
---------------------------

- environment creation
- code deployment
- test setup and run
- overly tight architecture
- hard to have high deploy rates when things are so tightly coupled

How orgs achieve high performance
--------------------------
- 89% are using infrastructure version control
- 82% are using automated code deployments

The first way: outcomes
----------------
- creating single repos for code and environments
- determinism in the release process
- consistent dev, test, prod environments all properly built before deployment begins
- continuous delivery pipeline
- free ourselves from the learned behavior of catastrophic deployments
- decreased cycle time
- Fast release cadence

## The Second Way: Feedback

how do we take the learnings from the first way and feed it back into the system to prevent problems?

- understand and respond to the needs of all customers, internal and external
- according to lean thinking, the most important customer is the internal one---- the next downstream work center
- optimize for the person who receives our work
- shorten and amplify all feedback loops: stop the line when necessary
- It is better to stop production and swarm the problem than to allow the problem to flow downstream
- Continuous Integration / Delivery depends upon stopping the line!
- Create quality at the source
- create and embed knowledge where we need it

"shared pain helps significantly with the achievement of shared goals"

Google:
- devs initially maintain their own service
- any app must be self managed for 6 months before being eligible to be managed by Ops
- even at google, the SRE (site reliability engineers) are the scarcest talent they have
- so the worst thing they can do is squander their time with crappy apps
- Test whether developers qualify for IT operations resources
- Types / frequency of pager alerts	
- production hygiene
- defect counts and severity
- Ops has a "hand back" clause
  - after the handoff, if it's shitty, it goes back to dev for management
  - "You're not worthy"
  - Gene likens it to getting a puppy handed to you. "Sorry, it's peeing all over the floor. You take it back till it's more mature"


Etsy
-------
- monitoring all the things
- devs must ship with telemetry


Integrating into Continuous Delivery
-------------------------------------

- The days of reviewing request for change docs in change management meetings are over
- adding more approvals, and more processes, results in more failure because it decreases feedback
- failures should result in more automated tests in the CD pipeline


The Second Way: Outcomes
-------------------------

- defects and security issues get fixed faster
- standardized and reusable ops and infosec user stories now part of the agile process
- all groups communicating and coordinating better
- everybody is getting more work done


## The Third Way: continual experimentation and learning

Foster a culture that rewards:
- experimentation and learning from failure
- repetition is the prerequisite to mastery
- repetition changes habits; habits change outcomes

Why?
- you need a culture that keeps pushing into the danger zone
- and have the habits that enable you to survive in the danger zone

Break things early and often
- do painful things more frequently
- Developers thank you b/c they know it makes deploys go more smoothly


Break things before production
- enforce consistency in code, environments, and configurations
- Add asserts to find misconfigurations, enforce https, etc
  - If config isn't right, FAIL!
- add static code analysis to automated continuous integration and testing process
- twitter built a tool called "breakman"
- "the days of doing code scanning at the end of a project and getting back a 200 page PDF are over"


Marty Cagan, eBay
- devote at least 20% of time to paying down technical debt
- or else, you'll eventually end up spending a lot more time

Recognize compounding technical debt
things that keep getting worse



Scott Cook, Intuit
- During their peak season, they ran 165 experiments in production! 
- because that's when they had the people on their site so that the experiments could yield results
- on april 16, those experiments wouldn't have mattered


If Gene could wave a magic wand:
----------------------------

- become conversant with devops and recognize these practices when you see them
- be energized about how practitioners can contribute in this organizational journey

Email Gene for these things: genek@realgenekim.me

DevOps Defensive Audit Toolkit (email gene with subject "audit")
Enterprise devops case studies 
Early draft of upcoming DevOps Cookbook (subject "cookbook")



"Any improvement not made at the bottleneck is an illusion"



My question re: dev and security relationship

look on itrevolution and go watch "amazing twitter infosec talk"

### Other discussion points 

- Use application logs to demonstrate to developers the frequency of hack attempts on the sites
  - xss, sql injection, etc
  - helps us to avoid the "ghost" problem, where we're always fighting this specter of being attacked by enemies that are unknown to us
  - get concrete; get out of spooky "OMG if you guys only knew what we had to defend against but we can't tell you bc it's classified" mode


- The Patrick Lightbody story:
  - Once developers and not ops started becoming responsible for their app failures in production (i.e. on pager duty), quality started to improve. it's the "shared pain toward shared goals" thing.

- Gene mentioned 2 documents or guidance related to auditing... I need to email him for the names

- Ensure that security tests (authentication, xss, sql injection, etc) are part of the automated test suite

- Find things that you always do "at the end", and stop doing that!
  - Do these things early, and do them often
