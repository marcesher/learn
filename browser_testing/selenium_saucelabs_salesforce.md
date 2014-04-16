4/16/2014 Webinar

David Louvton
Sagar Wanaselja

# Webdriver

SF loves webdriver

"we suffer the pain of latency" -- they want the pain of running tests in a real browser

- helps them catch multi-platform issues, dom issues, rendering issues, inconsistency between app layers

"business facing tests": are we building the right system?

"technology facing tests": are we building the system right?

Their portfolio:

- 50K selenium tests
- 7.5k webdriver tests
  - full browser compat, firefox, chrome, safari, IE 6-11, some run in phantom
- 2k JS unit tests
  - no dom required; 10ms avg execution time

- 1 Million browser tests per day
  - run on every checkin
  - run against multiple browsers
  - run against multiple branches



Their Selenium Infrastructure

 - automatically create, assign, close, reopen bug reports for test failures and flapping tests
 - test jobs must meet failure thresholds. code lines are locked for teams under thresholds
 - support all combos of OS and browser using portable VM templates

"Page Object Interfaces"
  - then, Web Impl, iOS impl, Android Impl, etc
  - Proper page object encapsulation  is:

    - make an api of your page for your test
    - no imports for openqa or selenium in your test
    - all references to driver and selenium in the page object
    - fail fast: call the page object factory in test setup
      - when you instantiate a page object, it should first determine that the page loaded properly
      - these determinations should happen in constructor
    - no assertions in page objects or any test utility
      - he says this is controversial but he believes it
      - assertions belong in tests
    - Share page objects across engineering teams
      - developer-complete UI should have a page object
      - if you can't make one it's not a testable page
      - this creates dependency challenges at scale
    - write the page objects iteratively, as required. don't try to write the whole thing all at once

Mobile is obviously challenging

- different page objects for different mobile platforms
- they do a lot of their mobile testing currently on chrome using a mobile user agent


Sagar shows a test converted from Selenium RC to WebDriver

 - Ha! this converted example has lots of sleeps/waits

 - you should not wait for page to load; rather, wait for something specific
 - shitty xpaths make it hard to understand what is being located
 - not enough assertions in this test he shows


 instead:

 - waitForElementVisible() instead of wait for page to load
 - replace locators with meaningful variable names, use IDs instead of xpath where possible
 - use guard conditions before taking action, eg if a light is supposed to be off, verify it's off before you turn it on, and then verify it gets turned on
   - they want to guarantee they're starting in the position they think they're in

 then, converted to page object:

 ```
 mypage.openAndWaitForCommentingReady();
 mypage.verifyNoFeedItemTimestamps();
 myfeed.verifyNoFeedItemsLiked();
 mypage.TypeComment(...)
 mypage.waitForAnyFeedItemTimestamp();
 mypage.ClickOnLikeForFeedWithText();
 mypage.waitForAnyFeedItemIsLiked();
 ```

Diagnosing Test Failures

- screenshot and html capture at failure point
- differences between localhost and automation VM
- optimistic timing assumptions
  - javascript, rendering, server response, etc
- defensive "negative" testing
- getting to 100% test passing


More tips

- version tests and app code (and configuration) together
- he doesn't like the test code living separately from the app code
  - this is especially important for page objects, he says
- Use Page Objects! "best thing since sliced bread"
- Use the API to set up the test, not the UI
- Anticipate selenium and browser releases
- Allocate capacity to browsers most used by customers
  - log the user agent on every page view

- for static / simple html pages, consider the HTML Unit driver!!!!!