Cars.com

- 600 JVMs to support all environments
- 200 million page views per month

They cut their UI testing effort from 100 hours to 2 hours via automation -- just for one section of the site

went from 40 releases in 2011 to 700 per year now

use DeviceAnywhere for mobile, but moving to something like appium or "calabash"?

overall: went from 235 testing hours to 4.5 testing hours for all products... 98.2% test cycle savings

How?

robust automation framework
 selenium / webdriver managed by maven

 java based selenium

 smoke tests and core run daily; regression tests are run when code pushed to "IT"

 testers participate in planning, determine automation necessesities, create automation tasks, etc

 6 months to build automation framework

 they use BuildForge for CI, maven, TestNG, Compuware APM for performance testing, selenium grid 2 with vmware for spinning up nodes

 sql lite to store temp data; blown away at end of suite run;

 sikuli 10 to interact withthings like flash

 hp quality center for humans to write test cases

 on failure, screenshot is takena nd goes to test output

 product teams notified of any issues after tests run

 find performance issues without having ot rerun multiple times

 the compuware APM tool
  - runs in any environment
  - gathers data from automation suite runs, monitors JVMs as well
  - dynatrace is a browser plugin that captures data as the tests run and sends to dynatrace server


Best Practices

 - start early
 - break in pieces
 - test on every build

 Create Focus
  - decide what automation to skip
  - focus on high priority parts of teh site

 Define KPIs
  - throughput, response time, memory consumption, etc

 Lessons Learned

  - all of this takes time to accomplish
  - clear and concise naming conventions
  - use data to gain buy in
  - have examples you can explain in detail that show the benefits of this kind of automation


