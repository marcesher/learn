using selenium to test not just UI behavior, but also LAF

When behavior works, but appearance is off, how do you fail the test?

## Pain
  - each new test must run on multiple configurations
  - spin up new vms for all this
  - layout analysis is not commonly automated

- Comparing layout is deceptively taxing
- humans can do it but it doesn't scale well
- we can test behavior across browsers, why not presentation?

## Methods of layout analysis automation

 - Positional data from the dom
 - computer vision anlaysis on screenshots
 - heuristics / rules

 - often can't rely on the dom alone due to differences in browsers and even different versions of same browser