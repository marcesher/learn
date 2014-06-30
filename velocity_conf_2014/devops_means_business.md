# DevOps means business

gene kim, jez humble, nicole forsgren valasquez, nigel kersten

Talking abou the devops survey

9200 respondents this year

Firms with high performing it were 2x more likely to exceed profitability, market share, and productivity goals

50% higher market capitalization growth over 3 years

They used snowball sampling for this survey

It's hard to get at the analysis directly.... "statistically, 6 out of 7 dwarfs aren't happy"

it's hard to measure IT performance

Nicole says this is the first time anyone's been able to measure IT performance in a statistically valid way

Comes down to three measures:

1. deploy frequency
1. mean time to recover
1. lead time for changes

She uses cluster analysis to take these 3 components and group them

Gives them a way to show how high performing companies cluster together, mediums together, lows together


What types of practices correlate with IT performance metrics

Stability Metrics:

 - Mean time to recover
  - version controlling production artifacts and code
  - monitoring system and application health

 - Lead time for changes
   - version control
   - automated testing

 - deployment frequency

   - continuous delivery (small batch sizes, frequent deployments)
   - version control


 - Change fail rate

  - not strongly correlated with specific practices
  - significant differences between the lows, mediums, and highs


Top predictors of IT performance

 - peer review
 - version control of all prod artifacts
 - proactive monitoring
 - high trust culture
 - win-win relationship between dev, ops, and infosec
 - high job satisfaction


Organizational Culture

- they are measuring culture
- based on work from westrum, 2004 (typology of organizational culture)
- go get his slide on this (or read the 2014 state of devops report)

- pathological (power oriented) vs Bureaucratic (rule oriented) vs Generative (performance oriented)

- lists the traits of the three types
- high performers have a generative culture

- Job satisfaction was the highest predictor of a generative culture
- climate for learning
- win-win relationship between dev and ops
- version control
- automated testing

Jez says these last two are not obvious, but they keep showing up in their measurements.

Slides have some links for organizational culture resources
  - read up on nummi
  - read Toyota Kata by Mike Rother
  - the point is that it's not the people, it's the system.
  - the system determines the success of the people
  - go listen to the This American Life episode on nummi


If you can look at one thing to predict IT performance, look at job satisfaction:

  - Would you recommend working here?
  - Do you have the tools you need to do your job


## Surprises

 - whether or not you have an integration or stablization phase has zero impact on IT perf
 - peer review is more effective than CAB, not just for throughput but for stability
 - a CAB is not correlated with stability, but decreases throughput

 - version control of the environment is more important than version control of code
 - there's never been a better time to learn stats


Donnie Berkholz asked them: Can large orgs be high performers?

  - yes, but orgs with 10k+ employees are 40% less likely to be high performing vs 500 employee orgs

- Can large orgs adopt these practices?

  - Yes... they found the size of the org didn't affect the ability to adopt these practices, EXCEPT 1:

    - change approval processes were heavier and more ceremonious in larger orgs
    - Jez calls it "risk management theater"

- This finding is huge, I think

 - Deevops practices and IT performance impact organizational performance
 - change fail rate wasn't part of IT performance

 - Forming new devops teams and giving people devops titles is successful in practice
   - they want to learn what industries are adopting these titles
   - and if you're on a devops team, do you also have a dev team and an ops team

