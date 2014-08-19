
# Positioning Agile and Continuous delivery for auditors and examiners

Simon Storm

Director of Enterprise Apps at Promontory Interfinancial Network

Slides will be on slideshare


Promontory Interfinancial Network builds software for banks

Check out the linkedin continuous delivery group

## Auditor's Shoes

It dawned on him that auditing is in place for a reason. He tried to stop dreading it and start enjoying it.
If it's hard, do it more often

 - Does this entity have sound dev practice?
 - are processes repeatable and ensure consistent results?
 - does management really understand the risks they're exposed to?
   - auditors don't tell you how to run the business
 - are appropriate controls in place?


## Tips and tricks for audits and exams

### Agile education

Auditors and examiners are increasingly "getting" agile... even seeing auditors who are certified scrum masters

1. Socialize your plans
  - Don't surprise the auditor with a major change to your process
  - don't automate something without discussing it ahead of time
  - you may need to demonstrate that you're not the first one doing this type of automation; show that what you're doing is tried and true
  - point them to books, articles, etc

2. Don't risk the crown jewels

  - don't start continuously delivery on your biggest, most important app (the one that brings in all the money, for example)
  - demonstrate new tech on lower risk apps
  - if you do need to do a major app, find a way to segment the implementation to minimize up front risk

3. Demonstrate your expertise

  - show to the auditors that you're experts in the field
  - you have the qualifications to do this type of process

4. Map Agile SDLC to Waterfall SDLC

  - show auditors how the phases in waterfall are accomplished in agile
  - Design, Design Review, Design Signoff, etc. See the slide

5. Explain benefits of shorter cycle time

  - when a vulnerability is found, how quickly can you address it?
  - when a enw os patch is released, how long until it is on all of your servers?

6. Explain how small batches reduces risk

  - schedule risk, quality risk, business risk

7. A more auditable process

  - an automated process is far more auditable
  - everything you do should generate a log file

8. Correct version of the application

  - "environment sprawl"
  - local dev, dev, qa, staging, prod ... multiple of each
  - auditor will ask: how do you keep them all in sync? How do you know they're all in sync?
  -

9. Infrastructure as code

  - this really helps with #8, because the tools guarantee it
  - requires really good habits... putting every single thing in source control, not making changes directly on servers, etc

  -  want to get to a point where it's easier to stand up a new server than it is to troubleshoot a problem on an existing server
  - with IAC, you can then do diffing / beyondcompare to see what changes are made to an environment

10. Static code analysis

  - Sonar, etc
  - Gives you some measurements around complexity, technical debt, etc
  - Sonar does have some security tests built in... not much, but a few
  - Sonar has a changelog, so you can see what config changes happen to it to demonstrate that people aren't turning off things in sonar without others knowing, etc


11. Automated testing

  - probably the biggest component of CD... without it, you're hosed

  - but this is very frustrating for him from an audit perspective
    - "who validated that the automated test worked correctly?"
    - "how do you know the test worked?"
    - "how can you be sure you have sufficient coverage?"
    - "where are the tests for specific user stories?"
    - it's actually useful to be able to show failures, to show that the tests did fail when something unexpected happened

12. Repository management

  - they use nexus
  - single spot for software, binaries, and libraries
  - single auditable repository of external resources
  - consistency across environments

  - QUESTION: with dependency management, how do you keep up to date if you're always using specific versions?

"Maturity is not when we start speaking big things, it is when we start understanding small things"


13. Go digital

- Online agile boards (Jira, versionone, etc)
- "an auditor once pulled a sticky off our physical board that was in 'Ready for Test'. He asked "If I don't put this back, how do you know this was tested?"
  - they lived and died by the stickies

14. Automating sign-offs

  - Jira: Group sign off plugin

15. Automating Documentation

  - generate docs from all stories in a sprint
  - "xporter" by xpandit
  - grabs the data from jira (I think) and then does a "mail merge" and sticks it into their template
  - he says that no one else uses this documentation, that it's only for auditors
  - they generate and save these reports and then save the reports (it's part of their documented process)

16. Logging Pipeline activity

  - this is his favorite thing
  - document that shows the entire deployment, along with the changelog from git

17. metrics

18. add one more meeting

 - sprint planning review meeting
 - stakeholders are invited
 - catch-all for interested stakeholders


20. don't ignore ops

  - a build pipeline has gates that ensure no one single person can move something the whole way into production
    - involves a lot of teams

22. Demonstrate permissions

  - make sure you have appropriate controls in place for things such as git

23. Code reviews with pull requests

  - stash can be set up to require X number of reviewers, and can even suggest reviewers (neat!)

24. Secure your pull requests

  - custom git hook (think: clouseau)


25. Outstanding risks: (see his slides)

  - lots about permissions

