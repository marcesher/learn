# Twitter Infosec team

Details: http://itrevolution.com/heres-how-the-amazing-twitter-infosec-team-helps-devops/

Slides: http://www.slideshare.net/xplodersuv/putting-your-robots-to-work-14901538

Watch: http://vimeo.com/channels/appsecusa/54250716


"We're on the product security team at Twitter, which means we work on code that ships"


- Twitter grew very quickly
- Fail Whale
- Lots of infrastructure and security challenges
- Shows the BarackObama hack, which spawned all this.

- First challenge:
  - dealing with a large, constantly changing codebase which was under constant attack

- had a lot of white hats who were reporting vulnerabilities
- they were able to fix a lot of the big issues
- gained them some time to look forward and be reflective

- this happened around the time of a hack week, so:
- they were out of firefighting mode, needed to look into automation to help them with security

# Lay out philosophical guidelines
  - used them to shape what they were going to build

  1. Get right info to right people
    - secure code isn't about tech; it's about people interacting with tech
    - augment existing social processes
    - communicating about vulnerabilities is just as important as finding them
    - "What we didn't want was to run a tool that generated this huge report and then send it to someone"

  1. Find bugs as quickly as possible
    -
  1. Don't repeat your mistakes
    - they were dealing with the same bugs over and over
    - 'best predictor of the next bug is the last bug'
    -

  1. Analyze from many angles
    - they use multiple tools to capture different types of issues

  1. Let people prove you wrong
    - security automation results aren't always accurate
    - they want engineers to have a voice in the process and to
      trust the results of tests
    - they don't want to give false positives to engineers

  1. Help people help themselves
    - most people want to do the right thing

  1. Automate dumb work
    - the point is to not do work you can delegate to a machine
    - if it doesn't require judgment or creativity, it's suitable for automation

  1. Keep it tailored
    - they've found that building their own tools has helped them save time and money
    - each org is different... uses different tech, has different processes

# Automate Workflow

  - That's the point of this presentation
  - Tool automation without workflow automation only gets you part way


# Automating Security

  - Not just about using automated tools
  - You have manual tasks:
    - code review
    - pen testing
    - external reports coming in about vulnerabilities


  - How to automate?
    - You can automate some of this stuff
    - Code review: static analysis tools
    - Pen testing - use available analysis tools
    - External reports: use the browser! When it detects a problem, have it submit to twitter (CSP... more on that later)

  - They wanted to automate the workflow!

    - Even with automated tools, the workflow was still manual
    - they want machines to automate the workflow

      - eg: run static analysis on code commit
      - run dynamic pen test tools in background
      - gather reports, issue notifications

  - They started with Jenkins
    - but it fell down after a few months... not the right fit

  - So they build the Security Automation Dashboard (SADB)
    - central service to handle all the automation tools, gather reports, issue notifications
    - single place to see what the issues are with any given project
    - other tools report into SADB
    - SADB figures out whether to notify developers or security team


## Automated Tools

### Brakeman

 - static analysis for Ruby on Rails
 - Fits in with "find bugs as quickly as possible"

 - on code commit, Mesos runs Brakeman on the commit, sends stuff to SADB
   - SADB can then notify devs if something's amiss
   - aligns with "Get the right info to the right people"

 - Brakeman generates detailed information
   - aligns with "help people help themlselves

 - On each info, it has a "False positive report button"
   - Brilliant!!!
   - aligns with "let people prove you wrong"

 - When SADB detects a fix, it emails dev telling them they fixed it


### Phantom Gang

 - Dynamic analysis tool
 - It looks for "mixed-content"
   - sensitive forms posting over http
   - old, vulnerable versions of jquery
   - forms without authenticity tokens
 - Different from an XSS checker, for example

 - What is it?

   - Nodejs based
   - spins up a bunch of instances of phantomjs
   - if it finds issues, it posts results to SADB
     - in this case, it files an issue in their JIRA
     - no notifications yet, b/c it's difficult to know who should get the report

### CSP (Content Security Policy)

   - See https://blog.twitter.com/2011/improving-browser-security-csp
   - Twitter is a big fan of CSP
   - it's a policy that defines what can run on a given page
   - Great for protecting certain things and for analyzing what's going on on a website
   - Any CSP violation is sent to an endpoint
     - then written to a hadoop cluster, to try to find trends and also false positives
     - CSP requires a *lot* of tuning

   - Can use it to detect XSS, for example
   - If a browser that supports CSP catches this, it protects that user,
     BUT: it doesn't help the users who don't have CSP-supported browsers
     - So this is a case where a browser helps them find a problem, and then they can fix it so that all browsers are safe

   - Aligns with "analyze from many angles"

### HTTP Strict Transport Security

  - make use of other useful headers
  - see his slides for details

  - So they decided to apply these headers to all applications
  - Aligns with "automate dumb work"


### ThreatDeck

  - Started with one dude's use of tweetdeck that looked for suspicious stuff in twitter feeds

### Roshambo (from Ro-Sham-Bo)

 - Lets them add infosec people's names to critical sections of the code
   so that when those sections were changed, infosec was automatically included in the code review

