# Baron Schwartz, Teams are Systems Too, Theory of Constraints in Action

This is the story of how he came to understand systems as teams

as the team grew:

- problems with billable time utilization; people at 30-50% and didn't know how to increase it, but it seemed like people were working hard
- lots of demand, so unpredictable in how they'd schedule people to work on stuff
- Baron couldn't figure out when anybody was going to get to anything
- customers unhappy
- but then he'd hear from consultants who had nothing to do

Then he was advised to read Goldratt's "The Goal"

and since he's read it, he sees systems in everything

1. What's the business goal?
  - to make money
  - businesses are systems to produce money
2. How
  - higher throughput
  - reduce inventory: inventory is something you've spent money on that you haven't gotten paid for yet
  - minimize operating expenses

Business Optimization

- Theory of Constraints
- 2 things slow it down
  1. dependencies in time, and dependencies in flow of work... everything that has to be true before something else can happen
  1. variations... things fluctuate, demand is never steady

- these are strongly related

How constraints impact systems

- with strongly coupled dependencies, variations in one part of the pipeline have big downstream effects
- how to contend?
  - decouple things, make them asynch... this helps build a buffer where work can sit
  - this can help bring back predictability
  - but they have to be small
  - and they also represent waste... inventory is sitting
- the worst thing you can do is look for waste and then trim it to fit demand
  - this just exacerbates demand

- this gets to the bottleneck stuff... any optimization not made at a bottleneck is an illusion

- you need to identify the bottlenecks... these often are the things with 100% utilization
- and you then make that bottleneck the leader, the pace setter
- and you work to improve its capacity, or remove it if you can
- then other bottlenecks will emerge
- in The Goal, this is demonstrated through the "Herbie" boy scout story
- in the phoenix project, Herbie is Brent

Baron realized he was the Herbie... he was the bottleneck
- and he was creating lots of fluctuation
- he'd whip back and forth between consulting and making sales
- and the feedback loop was way too long
- analogy to steering a canoe... steer one way, then overcorrect... (reminds me a lot of kayaking)

- so they added predictability by hiring someone to focus just on sales

Other problems they had

- variations in skill
- not enough knowledge sharing (this is a dependency: who can actually do the work)
- interruptions... unplanned work, firefighting
- unexpected problems with long delays... ssh keys and vpn setup hosed or not working, eg
- people moving on and off of vacation... wind down, ramping up
- big timezone gaps

Creating a special team that was completely interrupt driven
  - they worked on the fires, or pre-work
  - this enabled the other consultants to keep working


Book: The E Myth Revisited
  - how lessons of franchises can apply to any organizations

Applying to your org

- seek out things that are not predictable, things that will introduce big fluctuations
  - (he tells the story of the overworked sales guy, and his pipeline doesn't get worked)
  - recruiting: be recruiting for the stuff you know is coming down the pike
- identifying the herbie in IT
  - look for very specialized knowledge, like DBAs
  - they can get overburdened and reactive
  - look for people stuck waiting for help b/c they don't have the knowledge or access
- be vigilant about WIP
- look for things that take just a bit too long than they should... 5 minutes is a long time
