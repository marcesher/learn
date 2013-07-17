# Continuous Delivery and Devops -- Redmonk panel

http://expertintegratedsystemsblog.com/index.php/2013/06/opinionated-infrastructure-devops-and-continuous-delivery-leveraging-cloud/

Netflix: they removed every impediment they could to deploying faster
 - no one asks for permission or worries about cost when spinning up EC2 instances
 - they've built their own tools (aka asgard) and are open sourcing them


James asks Kohsuke: are Jenkins and Chef/Puppet starting to overlap?

 - Kohsuke started Jenkins to enable his colleagues to be safer and more productive
 - He didn't start with a grand strategy... just helping people
 - He doesn't believe Jenkins and C/P paths have crossed yet


Adrian Cockroft
 - Netflix doesn't have an architecture committee that decides all the things
 - practices emerge
 - the best solutions tend to win
 - continual experimentation


Puppet dude and James G. -- standards are bad
 - We don't want Chef and PUppet to arrive at a common standard for automation
 - Puppet dude says standards are BS; just go win in the market
 - IBM dude sort of agrees, says things in the automation stack are still emerging and standards aren't yet helpful
   - However, he says the cloud space needs standards

 - Luke Kanies (Puppet dude): standards committees require lots of people to **stop working** for months and years, and by the time they emerge it's already out of date


Biggest takeaway: as you build these automation practices, ensure the business is aware of them and how they can transform the way business is done
 - how can these practices change business strategy
 - wait, we can deploy that quickly? We can spin up an environment that fast? What does that now enable us to think about that we never would have thought of before

Who should we be learning from?


Luke Kanies
 - points out Pinterest as doing really interesting things with autoscaling
 - tools for doing reconciliation against puppet db, eg

Kohsuke
 - sees a big problem is that sharing solutions is hard from one context to another
 - we see conference presentations about some awesome solution, but to do it yourself you have to build it from scratch

Dave McCrory (warner bros)
 - Doesn't think there are a lot of examples today
 - the companies doing good stuff today will become the examples
 - there is no one company that is the reference for doing things right

 - WB's goal is to build a "composable enterprise"
  - if a group wants to experiment with something quickly and cheaply, WB's goal is to enable that

Daniel Berg (IBM)
 - agrees there is no great model yet
 - but sees enterprise customers doing great things internally (private clouds, eg)
 

Adrian Cockcroft
 - anything old and not changing, you wrap it in an API
 - "speed wins"
 - netflix 3 or 4 years ago when they moved toward streaming put the cloud budget and tools into the hands of the dev group and out of traditional IT; traditional IT still manages the datacenters

Dan Berg
 - everything should be an API, and treat APIs as an organizational asset
 - manage and simplify APIs
 - ensure composability of services
