# Adam Auerbach, Capital One

- this is about both their agile and devops transformation
- they were very good at waterfall

- moving to agile, they adopted "SAFe": Scaled Agile Framework

- even with agile, much of their work happened late in the process... integration and hardening

- part of SAFe is concept of a "System Team"

- it's a team dedicated to supporting an agile train
  - release mgmt, config mgmt, testing practices
  - purpose is to provide these capabilities to feature teams so they can have unimpeded flow to production
  - but big problem: it poached the doers from other teams
  - (holy shit... he's describing our Delivery team)
  - initially they focused just on CI
    - standard template around where is source code, where are artifacts, what tools are you using
    - they tried to get everything at least running in CI, automatically on commits

- lessons learned with system teams
  - treat as a new agile team
  - leverage sprint 0 for grooming backlog and undestanding of platform they're supporting
  - scrum works OK, but kanban is more sustaining
  - teams will be large initially and reduce as maturity is achieved
    - people will eventually go back onto feature teams
    - as the system teams get better, they can start managing multiple platforms
  - focus on early outcomes to develop credibility and gain momentum
    - going into a hole and spending a year building config management will not demonstrate your value
  -

- Continuous testing
  - shift left... find those hardening and integration things they were doing at the end, and do them earlier
  - move toward TDD and ATDD

- ATDD
  - gherkin
  - this is difficult stuff... big barrier on long-standing dev teams
  - need to train the team on how to do this
  - set expectations that this will have an initial 20-50% velocity hit
  - adoption takes 6-9 months
  - socialize, train, coach
  - successful adoption based on collaboration and communication vs automation


- collaboration is key
- fast feedback
- andon cord: stop the line when something's wrong so you can fix quickly and keep going
-

- Hygieia: open source DevOps Dashboard
- Capital One's first venture into open source
- pretty slick looking dashboard to show realtime view of health of platforms


- Service Virtualization
  - when they started doing continuous testing, they ran into a wall
  - SV was a key enabler for them
  - saucelabs, for example... had to add ability to spin up environments so they could run all the tests quickly

- Release Management

  - documentation about the pipeline
  - traceability from testing perspective
  - used BPM tool that they hook into version one, udeploy, etc so that part of the pipeline is to throw stuff into the BPM tool
  - they can put all their stuff into production, dark
  - and release management can turn it on



- Secret Sauce

  - to drive adoption, created specialize teams to own the implementation
  - started grass roots; got success; went to CTO, got people from CTO staff to be on these teams to be accountable to making it happen
  - specialized swat teams, "walking decks" for socialization, Line-of-business champions, then System Teams
  - recognition for teams doing this stuff encouraged other teams to do it

  - Shared Service teams are learning hubs
    - they help minimize the upfront costs to getting started
  - these teams do demos, curate discussion boards and documentation
  - they feed the engine
  - they had to grow these skills and teams internally and organically

  - value stream analysis
    - great tool to communicate ROI for leadership hesitant to invest
    - helped surface things where teams thought they were great but in fact were not
      - great story here... VSM showing how a team of 6 is doing so much rework that they're really working like a team of 3

  - evangelists at every level and discipline... he says this was critical
  - be ready to educate everyone on everything
  - be prepared for additional costs (training, consulting, etc)