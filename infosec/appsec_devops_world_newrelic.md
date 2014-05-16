http://blog.newrelic.com/2013/12/19/appsec-devops-world/

Shaun Gordon

New Relic infosec director

- security and speed of delivery are not mutually exclusive, but you have to
modify the way you do security

- with agile, we're now doing weekly, daily, even hourly delivery, but most security
professionals are still in waterfall mindset

# Traditional waterfall SDLC Security:

1. Requirements
2. Design
  - security folks review the architecture that's proposed
  - start to do threat modeling
3. Development
  - secure coding practices
  - static analysis
  - white box testing
4. Testing
  - dynamic analysis
    - think: nessus webapp scanner
  - security requirements testing
5. Release
  - penetration testing (white hack hacker; very manual)
  - security assessment
    - did we miss anything?
    - often includes manual code review
  - security sign-off
6. Production
  - vulnerability scanning
  - more pen testing

This whole process involves gates.. you can't move from one step to the other
until the security team approves moving to the next step

# Security people also like to see:

  - separation of duties
    - devs develop
    - release engineers release
    - devs should never release to prod
  - Management sign-off for release
    - senior manager must review every single change and sign-off
  - Limits on production access
    - devs, qa can't get to prod


Gordon says: this model simply will not work with Agile / continuous delivery

So how to modify it?

# "Continuous Deployment Security"

## Requirements:

  - low to no friction (can't slow us down)
  - must be transparent
    - this is a mantra for him
    - developers shouldn't change what they do to fit with the security lifecycle
      - rather, security must change how they do to match development lifecycle
      - no significant changes to development process
  - must actually make us more secure
    - processes can't be value-less box-checking


## Strategies and Tactics:

 - Automation
 - Devs must be trained
 - Lightweight processes
 - Triage: pick and choose what to look at; look at what's important
 - Quickly detect and respond to incidents
   - he thinks this is turning a weakness (no heavy processes up front)
   as a strength, because this enables security fixes to be deployed just
   as quickly as any other fix

Step 1: Remove those stop signs (gates).
Step 2: Recognize that the silos described above don't really exist
Step 3: look at each item... how does it change?

## What the Security lifecycle looks like now:

### Requirements & Design:

For any new feature:

  - get security involved right away (lighter weight, and easier)
  - They have a "Required security evaluation" that happens
    very early in the design phase
    - short meeting, < 25 minutes, includes a
      1. technical overview,
      2. business context,
      3. developer concerns
  - outcomes:
    - Risk assessment? Low risk? high risk?
    - If low risk... good to go
    - If high risk, they'll take a deeper dive, do threat modeling
    - Developers must documentn all outcomes from this meeting


Threat modeling @ New Relic:

  - If a feature is classified as risky enough to warrant threat modeling,
    they try to complete the threat modeling in a few days
  - Identify your assets (what you're trying to protect) and the threats against them
    - this helps focus your limited security resources to target the real, actual threats
      - contrasted with what he calls the "peanut butter" approach to security, which is to thinly
      apply your limited resources across the whole thing, whether or not an actual threat exists
  - How?
    1. Decompose your application
    1. Identify your assets
    1. Enumerate the threats against the assets
    1. Rate and rank your threats
      - for each threat, what's the likelihood (high/med/low), and what's the impact (high/med/low)
    1. Address or accept

  - He says this is one of the best tools they have

### Dev, testing, release

  - ensure devs have the right training
  - create libraries and services that they can use (reusable security)
    - eg authentication service, security event logging, input validation regex patterns, encryption libraries
  - Static analysis
    - this is frought with peril, due to so many false positives
    - throwing a whole mess of findings at a developer, especiall if it's
    full of false positives, will turn developers off to security
    - one key is to do it on every commit, since commits are generally small
    - they use brakeman + jenkins. Great for ruby shops, but...
  - Whitebox testing
    - Giv developers easy to use, targeted tools, and train them on them
    - they don't give them the tools the pros use b/c it'd be too difficult
  - they do continuous vulnerability scanning in all environments
    - good to do against staging and test to find things sooner
  - penetration testing: this takes a very long time to do right, so it's
  not possible to do it for every release.
    - instead, they do it in production on a regular basis

  - Security assessment: this is going to be really heavyweight
    - automated commit triage
    - nightly script that looks at all the commits, produces email
    report sent to the security team
    - commits are ranked (high/med/low)
      - they're looking for methods that are constantly causing problems
      - they look for modules (auth modules, etc) that are higher risk
      - then, for the high risk ones, they look at them right away
      - this works great for them and doesn't take much time
  - They got rid of sign-offs, but they rely on teh fact that they
  have quick detection and recovery

### Separation of Duties

  - They deal with this through accountability
  - Yes, you can release, but security needs to know who did what when

### Management release sign-off

  - replaced with a "sidekick" process
  - think batman and robin
  - for every release, at least one other person looks at the release (another dev, QA engineer)

### Production access

 - Provide enabling tools instead
 - ask people, why do you think you need prod access, and try to solve for those needs


# Conclusion:

 - automation
 - triage
 - quick detect / response

# Auditors

 - What about auditors?
 - Auditors are even more behind the curve than security people. They're still extremely waterfall
 - New relic approaches this with compensating controls
   - auditors want "A". New Relic isn't doing "A", but they're doing this other thing that compensates
 - Comes down to being able to tell the story, just like Shaun is doing here
   - "This is what we're doing instead"
   - They've passed 2 SOC-2 audits as a result