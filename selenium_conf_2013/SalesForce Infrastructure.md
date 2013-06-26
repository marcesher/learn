# SalesForce Infrastructure

Leads with: how many of you love selenium and never have problems with selenium failures?... "Selenium Failures Everywhere"

**Goal**: teach us from salesforce's mistakes with Selenium

Automation Infrastructure Mission:

    Provide the fastest possible feedback on code changes so that development is fun and efficient

 - They want to automatically create and assign bugs to developers who break the build

 - 13.6M test executions every day on a shared infrastructure, split among dev, stage, prod
 - Millions of Selenium tests every day, most in staging, many in dev, some in prod
 - 100,000 of machine hours every week... selenium about 25% of that


 **Autotest**
   - internal build tool that triggers on scm checkin
   - magic is that if it finds failures, it figures out whom to assign the failures to
   - Multiple Hosts -- Sub Runs
   - Multithreaded
   - Parallel threads to set up test data
   - The tests are grouped into "Sub Runs", and they can be assigned a priority so that high priority tests run sooner
     - then, process results from all runs

Checkins are not constant
 - slows down on weekends
 - huge spikes before code freezes
 - Consequently, hard to model and predict capacity
 - Need an elastic infrastructure

Numbers
 - 75K Distinct Selenium tests (10% of test inventory)
 - 52 Selenium Autotests (multiple browsers and code lines (dev, stage, prod))
 - Autotest have up to 70 parallel sub runs for faster results

Selenium Infrastructure
 - Automatically create, assign, close, and reopen bug reports for test failures and flaky tests
   - Moves the burden of test faiulres from the automation folks to the entire organization
 - algorithms for detecting flakiness
   - test that fails, passes, fails, passes... gets flagged as a flaky test and assigned to test writer for fixing due to its "flappiness"
 - Autotests must meet failure thresholds (99%+)
   - code lines are locked for teams under thresholds
   - too many test failures? code is locked until devs / QEs get their failures fixed
   - he says this is the key for them
   - they have an automatic mechanism to "lock the line" (a perforce lock) for certain teams / people
     - people bitch and hate them, but... it gets results
   - Code Coverage autotests enforce high code coverage and reduce duplication

Initially started with a home-grown, static infrastructure
 - very expensive, very brittle, not exploiting all the power
 - find the slides online for the rest of it... it shows "the old way"


Why not selenium Grid?
 - not dynamic
   - didn't scale, low utilization, lots of maintenance, lots of idle instances
 - hard to decide when to flash a vm
   - how do I know when to restart this vm, considering the vm's different use cases and tests?
   - flappers make it very difficult
 - difficult to configure
   - don't know ahead of time what vm a selenium test will run on
   - so don't know what configuration that vm might need to service those tests

**To the cloud**

 - salesforce knows the cloud, and so:
 **SalesForce Dynamic Grid**
 - uses JClouds to provision vms
 - they can run in openstack, ec2, vmware, etc
 - every single test gets its own unique, identical environments
 - the identical-ness is critical to eliminating flappers
   - if environments aren't identical, it's hard to isolate why a flapper fails when it does


## SalesForce Dynamic Grid

 - support for all combination of OS and Browser
   - portable vm templates
     - these vm templates can then be deployed in any cloud
   - better resource allocation
   - no maintenance

 - deterministic and identical test environment
   - reduces flappers