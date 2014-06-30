# Performance and maintainability with continuous experimentation

Seth Walker, etsy

sethwalker.me/talks/continuous-experimentation

How to get confidence in making sweeping changes without being disruptive?

How do we make changes safely?

1. Feature Flags

  - deploy on production, just to etsy staff
  - start rolling out to small % of users
  - watch graphs, scale back if necessary
  - requires lots of metrics gathering

2. Lots of AB Testing

3. Catapult

  - self service framework for running experiments

  - have a hypothesis
  - design experiment
  - analyze results


## Side effects

  - always some number of inactive experiments, resulting in code paths that will need to be cleaned up (i.e. cruft)
  - since most of their experiments are on the frontend, this results in bloated js and css for them
  - plus the cognitive overhead of cruft... all those damned if statements

  - Lots of devs want to clean up the code, but there's an element of fear: "Will I hurt something?"

  - Design for throwaway-ability (looksgoodworkswell.com/the-experimentation-layer)

  - "Ranger" -- tool for finding unused selectors, etc in css

Their challenge is to build tools that deal with all the data they collect and present it to devs in a way that meaningfully describes their confidence in the ability to remove a particular piece of cruft

