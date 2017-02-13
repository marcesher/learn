DevOps Principles:

- the three ways of devops
  - from the phoenix project
- small batches
- mvp

Tom boils down the three ways into:
  - process
  - communication
  - trying new things
  
  
Small batches principle

- talking about fire drills for datacenter failover, as a result of learning in 2013 that a big batch failover was not working, had SPOFs, took lots of coordination, etc
- desktop pc upgrades... do rollouts, no all at once
- new email server... same deal: migrate n users each week
- relationships: small batch = frequent constructive criticism, vs. letting frustrations build up then explode
- weight loss: lose 1 lb per week vs lose 100 pounds this year


MVP

- "deliver the goods sooner is better than all the goods later"
- each launch tests an assumption and helps make future decisions
- get a chance to pivot: users don't like it? change direction
- SREs get a chance to develop operational expertise
  - runbooks, upgrade process, failover, docs, etc
- if a project gets cancelled, at least you've delivered some value if you've done it iteratively; if it's all-or-nothing, you've delivered 80% of nothing, which is nothing

- Example: OS install automation. 

  1. Replace "carrying DVD to desktop" with netboot
  2. eliminate prompts
  3. customize OS
  4. start puppet
  ...
  
- Example: 6 month monitoring project
  - took 6 months to have a lot of debate, write a lot of specs, and end up with no monitoring
  - pivoted, started with an MVP, and achieved success