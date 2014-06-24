4/22/2014

sean mccullough

i-tier: breaking up the monolith

note: I'm passively interested in this, so I'm kinda sitting back and relaxing and just going to write down the highlight reel

this is a story about the tech not being able to keep up with the business, and actually holding the business back

 - it's that thing people keep saying now: every company is now a software company

- big problem: lots of different teams working in the same codebase; problem amplified by acquisitions and those devs not familiar with the code

- they needed to get to a place where teams were decoupled, not stepping on each other's toes

- He said they had a bakeoff... try out different techs

- says bakeoffs are futile b/c they devolve into religious wars

- He shows "Grout", which is a routing controller / A/B thing that lets them pass x% of traffic to certain URLs

- "gconfig" -- configuration as a service

  - some config can change on the fly
  - config can be promoted from uat - staging - prod
  - this is how they roll out feature flags from one environment to another

  - this eliminated the need for a releng team to roll out config changes across a 100+ node cluster
    - just add it to gconfig and it'll get pulled soon (the nodes all heartbeat against gconfig every few minutes)


- layouts as a service, too

  - lets them coordinate the look and feel across all of their services

- they did what everyone tells you not to do: big rewrite, cut over the whole company at once. everyone stop what you'er doing, port your shiz, and we're switching over by XYZ date

- Groupon has 1200 developers; 150 front-end developers.  globally distributed
  - What in the fuck does groupon do that it requires so many people?!

 - they were able to do this b/c they had monitoring on all the key business metrics
   - they knew how everything was performing, etc


- he talked about one of the problems with putting the ops onus on the dev team was that the dev teams weren't prepared for it
  - they didn't understand the kind of ops skills that would be required of front-end devs, for example
  - this was a big pain point for them

- this guy is really clear, articulate, and honest about the problems they encountered, both technically and socially/culturally, while undergoing the rewrite

- open source: testium -- mocha/node/webdriver, but synchronous.
  - this is so funny... they basically fixed the thing I was bitching about when I tried mocha