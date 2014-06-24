# Battle Tested Code (without the battle)

Gareth Rushgrove, @garethr (works for UK gov digital services)
  - he does devops weekly newsletter

James Wickett @wickett

- conflict between delivering secure code and what everyone else wants (shipping features)

- Ratio problem: high number of devs to lower number of ops to really low number of security people

- Out of band problem: when security tools are run out of band (when audits occur, monthly, yearly, etc)
  - sec tools run on code that's been in prod for a long time


## Security testing in the CI pipeline

"You don't need a fort knox style house if everyone around you is easy to burgle"

 - If you're at least better than the other guys, attackers will target them b/c it's easier

-  **Passive scanning**

  - static analysis

-  **Active Scanning**

  - testing the running application
  - think: nessus webapp scanner

- **Insecure Dependencies**

  - libs we're pulling from the net
  - tough to secure your supply chain
  - think: npm, maven, etc

- **Source code integrity**

  - guaranteeing that the code you wrote and think is secure is indeed the code going into production

James Wickett

  - Ruggeddev.org podcast


### TravisCI

- bit.ly/secure-pipeline-lab0
- github.com/secure-pipeline

- gauntlt: "be mean to your code"
  - built on top of cucumber
  - can hook into existing security testing tools, but does not install tools
  - book@gauntlt.org for a free book that's in the works


**Testing Lessons**

  - prefer fast over thorough for stuff that's part of the CI pipeline
  - check out sslyze for analyzing ssl stuff (such as heartbleed)
  - arachni for doing stuff like XSS Testing
    - I wonder if this could replace nessus
    - arachni-scanner.com
    - beefproject.com
      - for XSS payloads you can use for testing... Very cool!
  - He mentions code climate for static analysis of ruby/rails apps
        - I wonder what else is out there for python  and javascript

### Jenkins

 - domains.secure-pipeline.com

 - example jenkins: http://desperatefeynman.secure-pipeline.com/

 - ci.openstack.com - jenkins job builder
   - http://ci.openstack.org/jenkins-job-builder/
   - I MUST check this out!

 - check out github.com/OWASP for different GOAT apps for testing against

 - CLAMAV
   - virus scanning
   - Jenkins ClamAV plugin
   - Clam is open source (gpl)
     - this is particularly useful for when you're using installed dependencies (npm, maven, etc)

 - GIT Signing
   - not implemented in this example
   - git -S (signs commits with your pgp key)

 - OWASP ZAP
   - attack proxy project
   - run your test suite through this proxy, and it gets recorded
   - you can then replay the attacks
   - "zapr" is a cmd tool to help with this (check github)

 - Other scanners
   github.com/garethr/pentesting-playground


## Conclusions

 - iterate... add one thing at a time... don't need to do all the things right away
 - get involved at github.com/secure-pipeline
 - office hours: wednesday, 11:30 am, table 3