Damien Sereni
dev tools team at facebook

"Moving Fast with Selenium at Facebook"

motto: "move fast and break stuff"
 - don't be afraid to break things
 - but have a lot of tests



their goal in dev tools is to enable engineers to be productive, even as they grow massively
  - and over time, developer commits have largely tracked the increase in the number of engineers


Life of a code change
 - Sandbox
   - write code here
 - Code review
 - code lands in trunk
   - only one branch; no feature branches
 - Release Branch
 - Push to prod

 **Engineer responsible for all of that process**

 - engineer has to write all the tests
 - the engineer is responsible for that code when it's out on prod

How they release determines a lot about how they test their code

- Weekly release process: Sunday @ 6pm pacific
 - trunk becomes the release branch
 - completely automatic
 - that release branch is tested till tuesday
 - on tuesday, that's pushed

- twice daily releases
 - engineers op in to those releases

- they're adamant about keeping trunk clean, which is why they test so much

they use "phabricator" for code review

 - automated tests run against code before it's even reviewed

"Sandcastle"
  - try out a UI change in a sandbox environment

Coverage

 - they show test coverage for every change that gets reviewed
 - they have no target for test coverage
 - but test coverage is an indication of risk to reviewers

- Speed of tests is more important than completeness
     - they want < 10 minutes between submitting for code review change and getting test results
     - lots and lots of parallelism
     - not running useless tests
     - encourage smaller, more focused tests
     - tests focus on one particular interaction
     - tests themselves need to be fast

- Signal > coverage
     - Disable failing / flaky tests
     - bot assigns a task to whoever broke the test
     - after 24 hours, the bot automatically deletes the test
     - so that gives the test breaker 24 hours to fix the test
     - if they don't fix it, it probably wasn't that important in the first place

- Use the same language
     - minimize cognitive dissonance
     - there are no "test writers"... everyone writes tests
     - they started with Watir, but ditched it b/c no one was keen on it (it's ruby)

- cross browser
 - most tests run on the 3 major browsers
 - parallel runs
 - they don't test across the full matrix of OS and browser.... sounds like they do just the 3 major browsers
 - says they don't get much benefit out of doing a full matrix

FB open sourced their php webdriver bindings

 - and it sucked!
 - devs hated it... too hard to use, api was awful
 - devs ended up reinventing the wheel in their tests

Today: PHP Webdriver Bindings 2

 - announcing open source release today
 - based closely on java bindings
 - github.com/facebook/php-webdriver

How they integrate tests and code

  - all html elements have a "test id" that becomes an attribute of the element
  - this is how they test facebook! their selenium tests look for that testid, not for the "real ID"
  - this gets them out of the problem of IDs changing, etc
  - makes tests a lot less fragile
  - in practice, this is rendered as a css class

What about mobile?

  - Mobile first
  - features are targeted for mobile first
  - if you own "photos", you also own it for mobile

Mobile release

 - time-based release process, just like web
 - every 4 weeks
 - thursday @ 5pm pacific

UI testing for native mobile

 - Use the same language as the code is written in
 - based on webdriver (reuse infrastructure / skills)
 - Work across apps
   - FB app, Messenger App, FB Home app

 - Objective C Test code, Obj-C Webdriver bindings
 - Java test code, Java webdriver bindings
 - talk to phones with json wire protocol / http
   - so what's the middleware? what's in between the json wire protocol and the devices

 - He says they're only just starting for native mobile testing