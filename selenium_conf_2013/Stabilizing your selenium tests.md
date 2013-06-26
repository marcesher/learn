Talk from dude from Groupon



#Stability is a journey, not a destination

 - stability is ephemeral... once you achieve it, it goes away so quickly


# Culture changes
 - convince management that flakey tests waste a lot of money
 - discourage developers from relying on tests
 - prevent red build from merging into master
 - red master is not OK
   - should be shameful

# Fix Ajax Waiting
 - ajax things take too long
 - many people move to jquery and use evaluate_script
   - TIPS: check for evaluate_script("jQuery.active") == 0
   - e_s('$(":animated").length') == 0
   - give all interactions time to finish
     - slows down tests, but worth it for greenness

# Self contained tests
 - separate databases
 - self reliant tests
 - use setup/teardown
 - make sure tests do not rely on order

# Faster feedback loop
 - fight to get build to 10 minutes
  - parallelization helped them get from 3 hours to 15 minutes
    - downside: faster to push code than test locally
 - notify of failures before build is finished
   - rspec/cucumber early notification formatters
   - engineering.groupon.com
   - so when a first faiulre happens, an email is sent to developer saying "your build will fail, here's why..."
     - developers can start fixing busted builds even before it finishes
     - plugins coming to open source

# Flakey Detector

 - check jenkins or git diff
 - if a test was modified, kick off flake detector build
   - run changed test 5k times in 10 mins
   - in random order
   - they should always be green
   -- see upcoming blog post for details


# Flaky Environment

 - tests get blamed if environment fails
   - devs blame tests for failures
   - eg a test box with 24 cores has passing tests, but 12 core box has failing tests
 - standardize test boxes
   - chef, puppet, etc

# Windows tips

 - Move mouse out of browser in IE  -- something, not sure what, but this helps
 - Maximize test window - tests will behave differently when window is smaller, especially with JS
 - Don't use RDP / RDC
   - it'll affect your tests
   - Use VNC!
   - forces windows to not go into GUI-less mode

# Linux tips
 - Run firefox in separate Desktop
 - each parallel thread runs into a different Desktop in VNC


# Speed up tests
 - parallelize more
 - decide: does this have to be a selenium test?
   - can it be a unit test?
   - can it be headless?
   - can you run jasmine instead?

# Black Hole Proxy

 - capture any external requests, return 200
   - cuts off any external request!
   - see tests speed up a lot
   - reliability goes up
   - solves problems with CDNs, etc
   - "em-proxy"
   - https://gist.github.com/dimacus/5757573

# Gem Cacher

 - cache any external dependencies locally
 - don't rely on rubygens to always be up
 - local maven repo


# github.com/groupon/Selenium-Grid-Extras

 - basic idea is to help maintain the environment to produce stable tests
 - turn selenium grid nodes into dumb browsers
 - reboot windows
 - capture entire desktop chrome, not just browser
   - very helpful for detecting popups, etc
 - lots of future plans
  - record videos, share files with grid nodes, spin up / down vms on the fly
  - image comparison
  - auto update selenium webdriver
  - and more