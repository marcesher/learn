# dave cliffe, arup chak


- Incident Response Framework

- FEMA wafflehouse index: a way of categorizing how bad an incident is
  - If the wafflehouse is closed, that's bad
  - if it's open and serving the full menu, things aren't bad
  - think: 1 alarm file vs 5 alarm fire
  - trying to determine what your response should be

- they look at severity, customer impact, how unknown the incident is... these are part of their framework
- they've landed on green, red, yellow, black

- black: black swan events

## Green / yellow

- smallest impact incidents
- green: 1 person can handle; yellow: 1 team
- green: no customer impact... yet
  - disk is getting close to full, eg
  - staging goes down at 4:30 am... not a big deal at that time; would be a big deal later
- one mistake he sees is companies constantly in yellow, because companies don't know what's important to them
  - the problem is alert design
  - too many canaries
- His rule is: aggressively get rid of the alert or fix the alert's threshold
- otherwise: alert fatigue

## Red

- transitioning to red
- what makes the incident red is that customers are now affected, not that the servers have gone away
- his point: use **business metrics** to determine incident level
- you have to be able to translate a business metric into an operational metric
  - Availability is **not a good enough** metric; you're there for more than just keeping the lights on
  -

## Roles

- Resolvers
  - provide concise info to others on the call
  - CAN report: condition, action, needs
  - answers questions for the Incident Commander

- Incident Commander
  - can be anyone
  - they just need to be a good leader and good at the process of leading an incident response; title not required
  - if an exec comes in and "swoop and poops"... ask the exec: "would you like to take over the call?"
  - good IC is asking a lot of questions: what's the customer response, what have we done so far, etc. Resolvers answer these questions
  - **silence is OK**... you don't always need to be talking during a response
  - Sets a timeline for resolvers to check in; don't have it open ended
  - bias for action: for simple, low risk stuff, just do it: restart servers, etc
    - for high risk items, you need to dig deeper and solicit feedback: "is there any pushback on us not doing XYZ"
  - you're not seeking consensus; you're seeing support for your decision
  - they've been practicing rotating the IC role to different engineers

- Deputy
  - ramp up new people who join the call
  - they can do this out of band... in chat, etc
  - they can do communications with other stakeholders; freeing the IC to keep working the incident
  - they remind the IC of certain actions; keep them aware of checkin times, etc
  - updating chat / IRC, etc


## Consistent communication

- single chat room; single bridge call
- keep internal stakeholders up to date; having a single location gives them the ability to stay up to date without you pushing info to them
  - can give them the conf. call info; but be prepared for the swoop and poop
  - set expectations: they're on the call to stay up to date, not to drive it
- customer communication: accurate status pages

## Black Swans

- you've tried all typical remediations, but nothing's working
- in a way, this is a comforting position, because it's such a different beast that you don't have any idea when this will resolve
- forces you to get creative
- let internal stakeholders know that you're in this territory; they may need to start formulate a business response
- these are terrifying moments

## Conclusion

- you need to understand business metrics and how you contribute to those
- have the right roles in place for incident response
  - cross train! don't create a single Incident Commander... this is a Single point of failure. Limit the bus factor
- practice (pagerduty has "Failure Friday")
- black happens