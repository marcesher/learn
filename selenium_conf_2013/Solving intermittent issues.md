Trish Khoo
Google, test engineer

@hogfish

trishkoo.com

Talking about:

- test design
- logging
- tolerance

test design
 - I didn't understand what her point was here, other than that there are a lot of things that can cause tests to fail
   - daylight savings time
   - external parties and their stuff in your app (ads, etc)

logging

 - screenshots on failure are simple, effective logging
 - she tries to correlate test failures with app logs.... try to match up the times and see if patterns occur
 - build logging into the tests... simple things like time it failed, last url it was looking at, screenshots, detecting javascript errors that happened at the time
   - try to screenshot the entire desktop, not just the browser
   - this shows you things like antivirus popups and such


 tolerance

  - sometimes, they'll tag a failing tag with a suppression tag b/c they can't fix it right away
    - mandatory to add an "expiration" tag, such that a suppressed failure doesn't stay suppressed forever
  -
