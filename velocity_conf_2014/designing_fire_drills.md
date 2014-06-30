# The Practical Gamemaster: Design and Execution of IT Emergency Operations Drills

Adele Shakal (Metacloud, Inc.)

**This is a dense topic**... go get her slides afterwards at http://adeleshakal.com/

The goal of emergency planning and drills is to bring all the people and processes from earlier stuff (business continuity, disaster recovery, etc)

IF you've never done an emergency drill, drill for the most likely, not for the worst (at least, not to start)

Identify leaders.... these can be anywhere... doesn't  need to map to org chart

## Designing a drill

Decide whether the drill will be service specific, whole org, a team drill, etc
- note the purposes of the drill
  - technical purposes... is this service designed to be resilient?
  - nontechnical purposes... if we have an emergency, and the people who normally use a communications channel have that channel go down, do people know how to communicate in alternate ways?
    - if you all call into a conference bridge, is there a limit to the number of people who can call in, eg
- be very clear/transparent about whether you're actually bringing down a service, or whether they're just thought experiments ("tabletop exercise")
- Her first drills weren't about services at all, but about communication
  - do you knwo where your people are (if a building has caught on fire, or blown up, etc)
  - which people were there? which are remote?

## Design a communications hub / warroom / command center / incident headquarters

  - learn from the experts here

  - for disasters, it's important to identify what you know from the people/orgs who have checked in and also
  from those who haven't checked in


## Unknown terrain

 Your org might not have:

 - list of key people's contact info
 - publicized, prioritized list of top critical business functions
 - mapping of it services and infrastructure to critical business functions and who can provide status updates about their recovery
   - or people might not agree on what the critical business functions are


 - So: don't try to create a comprehensive service catalog for drill purposes if your org lacks one
 - But do identify org leaders to determine top critical business functions, recovery point objectives, recovery time objectives, and get it documented
 - Don't try to solve all the problems
 - Do identify the IT infra and/or services, manual workarounds, and processes which comprise the top critical business functions


## Designing a theoretical IT emergency

- Create "secret notes" for participants to open at set times

- Start and end drills on time... else, people might not show up for the next ones

- she has a slide with examples of these secret notes

- when getting feedback, try to get it in as few characters as possible

 - she says to have them give feedback afterwards, but limit it to tweet length
 - otherwise, you get novels

- consider simulating lack of personnel or facilities availability... you may need to randomize this
- she doesn't recommend simulating people being dead

- She makes a great point about keeping these fun and creative

- when you design brokenness, make sure it's consistent. EG the web team's secret note can't say the website is up if the network team's secret notes says all of DNS is down

