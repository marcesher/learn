 @noahsussman
 falsehoodsabouttime.com
 - lives in new york

Noah Sussman

 - helped Etsy with their high throughput continuous delivery process

 - most of what he's talking about he learned at etsy


## Canonical Agile release cycle

 - sprint of 2 or more weeks
 - start deployment at end of sprint
 - hand off to qa for testing
 - release


## Continuous Delivery environment

 - minimum viable feature set
 - deployment decoupled from release
 - real time data on how releases impact revenue
 - constant tweaks to live features


## How CD differs from canonical agile
 - large features deployed piecemeal over time
 - config flags
 - dark launches
 - wire-offs (what is that?)
 - **every** feature is part of A/B campaign
 - there is no "done done"

## Releasing a features is decoupled from deploying code

  - new code is deployed dark, behind a config flag
  - when the feature is considered complete, all the pieces of that feature that were deployed piecemeal are then enabled, fia a config vlag

  - he says this process is quite chaotic, like an airport without an air traffic controller
  - developers deploy directly to prod, without asking permission, without rigorous testing.
  - when the change is deployed, the developer then goes and checks it out

## Observed behavior of complex systems

 - emergent behaviores require unplanned responses
 - improvements are discovered, not designed
   - especially because users find the opportunities for improvements, once a feature is out there
   - improvements are often not designed by people in a meeting room
 - users of the system have complex expectations
 - such systems are never complete

## QA Happens when?
 - he says **complete testing is impossible**
 - what is "quality assurance"?
 - you can not authoritatively assure that there are no defects
 - quotes Dekker: "we are not custodians of inherently safe systems"
 - "testing is everyone's job"
   - everyone is responsible for quality, all of the time

## Falsehoods about QA
 - There are a finite number of bugs
 - there are a finite number of detectable bugs
 - all severity one bugs can be found before release
 - software is built to specifications
  - requirements are vulnerable to human interpretation
  - which makes it harder for QA to test that developers built the thing to the spec
  - specs get out of date quickly
 - at some point, software is finished

 Truth: Many bugs - even sev 1 bugs - result from small changes

 Note to self: I need to find his slide on the 'swiss cheese principle'

## Many small anomalies

 - swiss cheese model of risk presents a strong case for prioritizing the elimination of small errors rather than focusing on the mitigation of large catastrophic errors

 - unit testing is great at eliminating small errors

 - if layers of swiss cheese have enough holes, you can eventually line up the layers to get a "line" through the holes

 - "the best software engineering principles... quality assurance, testing... the highest standards -- it's not going to be enough"
   - Nancy Leveson
 - the above are required... but they will not be sufficient

## Leveson: How to limit risk

 1. Oversight
  - need support for things like selenium / automation from at least a high level engineering director
 2. Limit complexity
  - This applies to communication as well as systems
  - think about the challenger disaster
 3. Systems thinking
  - continuous delivery helps here b/c it flattens things out and spreads quality thinking across, not just focused on testing / testers / QA

## QA Happens when?

 - **Exploratory testing** can be performed any time
   - contrast to "automated checking", which is the things we do with selenium
 - Rigorous, **scientific** approach
 - Focus on **customer satisfaction** rather than a spec
 - Equally useful before or after a release

 - you automate away all the boring crap so that testers can focus on exploratory testing
 - exploratory tests are not scripted, not planned in advance
 - they find the things you didn't think about (and thus didn't automate)

 - developers make assumptions and then validate it's true... this is what unit and integration tests do
 - but there's still a need to invalidate assumptions
  - this is the "residue" that's left over after all assumptions have been validated

## Monitoring

 - "sufficiently advanced monitoring is indistinguishable from testing" - Ed Keyes
 - talks about Etsy's monitoring
 - 2012: etsy collected >250K real-time metrics
 - they use nagios, and they integrate it with selenium
 - he says we'll be surprised that the monitoring tools are surprisingly similar to functional test tools
 - Deciding which metrics matter is a human problem
 - humans must pick the graphs that are most important... those are the things that get surfaced on dashboards
 - graphs are best when they're easy enough to read that they surface problems in a way that even an exec cay say "that looks funny"
 - all that data, even the stuff that isn't immediately surfaced on a dashboard, help you identify and fix problems that otherwise would've taken way too long
   - tells the story about how they correlated a spike in network traffic and clogged network switch in 8 hours instead of days or weeks


## teaching QA

 - teach your QA people how to read diffs and logs
  - git logs
 - QA people can then get good at noticing bugs and correlating them with code changes
 - QA people need to get closer to the technology

## Lesson Learned

 - No aspect of continuous delivery is less risky... it's just different risk
 - pay attention to your efficiency-to-thoroughness trade-offs
 - CD amortizes risk over many deployments and exploratory tests
   - it does not save the risk till the end

 - Watch your graphs; test your whole system; incrementally improve the product

- he says to look for the amazon talk from velocity conf on how they do continuous delivery
- recommends etsy engineering blog
- talks very highly about chad dickerson, etsy CEO, and how he's an avid continuous delivery advocate
