https://www.youtube.com/watch?v=fMucUohYWI4

slides: http://www.slideshare.net/ITRevolution/thursday-500-elisabeth-hendrickson-gb-final

DevOps Enterprise Summit 2014

She says her role is "Care and feeding of feedback cycles"

- No one at Pivotal Labs has "Quality Engineer" in their titles; everyone is responsible for quality

## Feedback:

- you do a thing and find out how it went
- in dev, we need feedback on:
  - the extent to which our intentions match our need
  - to which implementation matches intentions
  - to which implementation met the need
  - these are *not* transitive... obviously you can have intentions that meet the need but have it fail in implementation

- "feedback latency": the time between when you do a thing and when you can observe results about that thing

- "spec" stands for "speculation"
- the longer the distance between when you do a thing and when you observe it, your speculation level is rising
- greater the speculation, greater the risk... the area under the speculation curve is risk

- "empirical evidence trumps speculation every single time"
- until we put our ideas into production, we don't know. we're speculating
- delivering small stuff fast eliminates speculation buildup
- however, in practice, if you have a "stabilization sprint", you're probably fragile
  - "stabilization sprint" means you're not done-done till the end
  - means stability is speculative until the end
  - she says this is just a different form of waterfall with the exact same risk curve
- information value: a little feedback now is worth more than a little feedback later
  - information has a short shelf life

## Different kinds of feedback

- you need **all** of them

- local unit and integration testing
  - always be git pulling and running all the fast tests before pushing your stuff
  - if stuff breaks, you fix it, even if it isn't with your code
- automated tests in CI
- story acceptance testing
  - the best people to do this testing are the people who asked for the feature in the first place
  - at pivotal, this is the product managers
- exploratory testing
  - discovering risks, getting information about the system
  - this in part answers the question: "who tests the tests"
- environment monitoring / metrics
  - canaries in different environments (dev, staging)
  - if something on a graph spikes, ask why immediately
- support tickets
  - recognize patterns
  - get the right engineer on tickets

## Visibility

- their team room has lots of monitors
- "checkman" -- compacts a whole lot of builds on a single page; open source, written by pivotal
- each team gets a monitor for their builds
- monitors for metrics (datadog) for each environment

## Feedback recipe

- check + explore + release
- automated checks on all check-ins
- explore to discover other risks, verify checks are sufficient
- release early and often
  - even if you can't actually release, you need to rehearse them

## Tightening feedback loops

- work in small pieces
  - they keep stories to a few days max; if it's bigger than that, split them
- find and squash wait states
  - she tells a story about gerrit and how long it took an engineer to get a single change accepted
- parallelize
  - deployments and tests
- remove duplicate tests...
  - dig deep and find tests that test the same thing
- drive tests to lowest level  possible
  - ensure that system level tests aren't testing stuff at the lowest level; turn those into unit tests

## Learning organizations

- fast feedback creates learning organizations
-