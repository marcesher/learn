# Ian Malpass, Failure is an Option

His truths:

1. You will create bugs
1. You will build the wrong thing
 - our understanding about markets will always be imperfect
 - you will spend time perfecting things that aren't worth perfecting
1. You will not foresee the unexpected (by definition)

These truths have consequences:

- you will lose money
- you will lose time
- you will lose data
- you will lose customers
- you will  lose credibility
  - this will make it hard to attract both customers and employees

- Failure is inevitable, but expensive failure is not

- how do we reduce the cost of failures?

- first reaction is to add barriers, checks, etc
  - but this just gives you deniability, CYA

- instead, what you need is speed and flexibility
- it's counterintuitive, but going faster helps you be safer

- this requires trust
- trust people to take responsibility
- trust ops to talk about the impact that developers are having on them

- do we just say "go fast we trust you" and we're done? of course not

So what's this look like in practice?


- At etsy, they can deploy at any time with minimal ceremony
- they use deployinator
- it's open to everyone; there are no gatekeepers
- because they do it often, this means deploying smaller chunks
- they rely heavily on code reviews, and code reviews are easier when they're smaller
- code reviews are a key way teams learn from one another
- if there's a failure, it's limited to a smaller surface area
- this also enables easier roll forward as opposed to rollback

- Manual testing: there's not a lot of manual testing at etsy as a distinct job function
- they do have QA people, but they're targeted toward the highest risk stuff
- QA is the responsibility of everyone

- Security: they're collaborators, not gatekeepers
- rather get their insight earlier rather than panic when it's too late

- Automated testing
- but there are tradeoffs here: more tests == more time
- they parallelize tests across very fast test machines
- they found a very small # of tests contributed to a lot of the runtime... and they deleted them
  - are these tests actually making us much safer?
  - the amount of safety wasn't worth the cost of slowing down
- same with flaky tests: if it's flaky, kill it

**Princess**

- Princess is their pre-prod environment
- all the code is deployed here first
- devs can manually test there while the tests are running

**watch the graphs**

- their graphs also show historical averages
- they have a deploy dashboard, but also make it easy for teams to make their own dashboards

**watch the logs**

- supergrep for log streaming
- easy to tell when something's going wrong; stacktraces link to github to make it easier to get to the code

**dark code**

- code deployed, but not released
- feature flags
- turn on feature for % of users
- flags for groups of users (staff, eg)
  - this lets them fail in private
- prototypes: users can join a group and get access to a feature

**building the wrong thing**

- CD, feature flags, and prototypes are key here
- A/B testing
- etsy isn't quite an MVP company, more like 'MVP-ish'


**expect the unexpected**

- tells a great story about incrementally stopping a spammer
- continuous deployment gave them time to fight the attack, a little bit at a time

- partial failures and degraded experiences
  - they keep feature flags in production, in case they need to turn something on/off
  - sure, that feature being down is suboptimal, but at least people can still buy

**blameless**

- learn from failure
- when talking about remediations, asking "does this new process slow us down and therefore increase our risk?"
- frank analysis, shared throughout the company
- this helps normalize the idea that it's OK to fail if you learn from it
- three-armed sweater award for best failure while trying to do something important
- that's how his awesome 4-star with a horse t-shirt came to be

**push the envelope**

- if you don't push the envelope, you'll remain slow
- their tooling gives them the ability to quickly recover
