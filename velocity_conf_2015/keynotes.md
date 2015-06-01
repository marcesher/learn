# Thursday May 28

## Laura Bel

1. think like a villain
1. create safe spaces to play, i.e. break things


## Dana Quinn, Intuit journey to public cloud

- dev environments where engineers can spin up dev envs in the cloud, which are then automatically brought down after hours of nonuse
- cloud-native; they're willing to take the risk of vendor lock-in b/c of the benefits it affords. They've intentionally taken on the risk
- don't bring legacy management patterns into your cloud environment
  - you find new metrics to track
    - eg: average instance age, utilization
  - antipatterns to watch for: manual steps for bringing up a provisioned instance, eg
- remember to "shut the cloud off"... devs probably aren't used to tracking spending
- empower teams to manage their own spending
  - don't leave the cloud running and wasting money
- load test generation has been a big win for them, because it's so easy to launch and shut down load tests on demand
- They're open sourcing their load test generation system, the one they use for turbotax... go see it at their booth

## Dave McCrory, Bash, running a data tier at scale

- data lakes, data gravity... this is the dude from the recent devops cafe podcast
- brings up CAP, says you can choose both C and A. I think he just flubbed and didn't actually mean that


## performance and reliability at verizon edge CDN

- "tools shaping culture"
-"coalmine": used to manage release of code and config changes; metaphor is canary in the coalmine
- dashboard of ongoing releases, with rich links to other stuff... incident management, customer support
- I think he was saying that maintenance teams sit in the important meetings: release reviews, design reviews, postmortems

## Astrid Atkinson, Google, managing distributed systems over long periods of time

- Planning for the long game.

  - Rule 1: imagine you are going to be very very successful, but you do not know where you're going to end up
    - act as if you have to live with the consequences of your choices for a long time
  - 2: complexity increases over time
  - 3: Scale systems, not teams
       - adding scale shouldn't mean adding people

- How systems grow: diversification

- Starting small... too much is as bad as too little
- When enabling growth, Manage software, not machines
  - get to a place where engineers can run their own services
  - you want as much standardization as you can get. "anything you can standardize will pay off in spades"
  - eg every single server at google ships with a tiny http server with a status page, so for every server you can go to /status and see what you're used to seeing
  - this is how on-call people can troubleshoot a system they've never even heard of

- engineering for maintainability
  - keep an eye on what's costing time, and consider "cost" broadly... it's not just money
  - dev speed isn't the most important thing; also need to consider ops
  - use shared infrastructure
  - apps must expect degraded services
  - use exponential backoff when doing retries, but you need to also introduce jitter so you don't get everything pinging at 2,4,8 secs simultaneously etc

- Consolidating systems
  - eventually, after you grow a lot, you'll discover opportunities to consolidate down
  - be conservative: avoid bulding new systems wherever possible
  - eg you have 5 different image processing systems because one team said "no, the existing one won't work for us; ours is different"

- Boring
  - boring == stability

- Second systems
  - complete rewrites are almost never the answer
  - if you do need to rewrite, get changes to production early; iterate early and often
  - big changes require a lot of lead time
  - you have to move the biggest customer first
    - if you start small and optimize for that, you'll never know what it's like for the biggest

- rules of the long game

  - don't let the weeds get higher than the garden
  - take care of your team
    - avoid burnout
    - your team is your service

# Bruce Lawson, Opera software, "where your next users are coming from"

- lots of stats about how the world is growing, what users across the world are using the internet for, what kinds of devices they're using
- lots of users are on low-spec devices
- he says we need to build for these devices b/c so many users are on them

- installable web apps... now available on android chrome, coming on android opera, nonstandard implementation in safari for apple
- json manifest, lets users basically bookmark the app onto the home screen and then when they open it, it opens the browser but in full screen, no browser chrome
- looks and feels like natively installed app, but it's just a web app

- proxy browsers, like opera mini
- small binary on the phone, user requests page, goes to opera servers where the app is pre-rendered, and compressed binary sent back to phone.
  - much smaller data and battery footprint
  - most web apps have 60 separate assets they're pulling down
  - this combines all those into a single binary

- this does require tradeoffs
  - no JS only APIs
  - no rounded corners or gradients
  - animations (css/svg) show only first frame
  - no webfonts... use svg
  - for example, if you're using angular, be aware you're potentially locking out hundreds of millions of users

- it's not just about the phones, either... it's about the network
- even as devices advance, networks are slow to improve

- What's next:

- for past 10 years, opera mini focused on compression
- next X years, opera focusing on compatibility



# Patrick Lightbody, New Relic, So you're a software business... now what?

- burrito app on apple watch
- every company is a software company

# Ariya Hidayat

- hug a scientist. we're all standing on the shoulders of giants
- "it's in our best interest to show gratitude and stay humble"

# Mikey Dickerson, USDS

- hc.gov created the urgency for USDS
- december, got $20 million in funding
- they're now trying to do something 100 times bigger than what he thought they'd be building... 500-600 people scattered across all 20+ federal agencies

- this is a talk about interacting with bureaucracy
- bureacracy is nothing more than lots of people working together to get something done
- anything worth doing in this world requires working with a large group of people

- learned they often get pattern matched to other IT reforms... bungeeing in to fix things, get good press, leave the agency with no support
- he says they're actually not interested in those types of projects
- "I'm doing the best I can with the rest of the year and a half I have left"
- he's not sure they've done enough yet that's worth institutionalizing, so he's not worrying about "how to institutionalize" it just yet

- his takeaways for us:

1. simplify your message, goals, founding statement
  - they're not religious even about the stuff in the digital service playbook
  - they have a lot of tactics... they like open source, but because it saves them from license fees, etc
  - they like open data, because it enables others to build stuff so they don't have to
  - they like agile methodology, in the cases where it leads to less waste
  - these are tactics, not religious credos

1. you are better off the bigger you can pitch your tent
- "stakeholder is a word that means someone who's going to be part of the problem or part of the solution"
- if you can win hearts and minds, it helps a lot
- you will not win all the hearts and minds. never. playing field always tipped in favor of inertia and status quo
- "it is a non-goal to undermine or replace the existing industrial-contractor complex"

1. you have to make it as easy as you can to make the people who have been part of the problem, to be part of the change / solution

  - if you have a big contractor, for example, who's been part of the problem, they can either be a big harm or a big help to your change effort
  - you'll need to make friends with people you didn't think you would have


# Laine Campbell, recruiting for diversity in tech

- "Every single one of you is recruiting for your company, in your actions and behaviors. You're bringing them in or you're sending them away"
- diversity is 2 dimensional: inherent and acquired

- I'm not writing down her bullet points... go get her slides

- "the meritocracy is broken"

- "if you don't have a diverse enough team to hold a balanced interview, contract out"