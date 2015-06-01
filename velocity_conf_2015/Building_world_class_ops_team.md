# Charity Majors (parse/facebook)
# Building a world class ops team

- talk targeted at startups, small companies

1. Do you really need an ops team?
1. What makes a good startup ops hire?
1. how do you interview and sort for those qualities?



- When new and small, some devs get stuck doing infrastructure work
- this isn't what they want to do, doesn't bring them joy
- so they clamor: bring in the devops

- she says: "operations engineering at scale is a specialized skillset"
- it is not software engineering lite
- you're not hiring someone to take over the shitwork
- these are people who know things you don't about how to build reliable systems at scale

- You need an ops team if you have hard operational problems

- If you don't have hard ops problems, but your SWEs suck at ops... you might not need an ops team
- probably can't attrack top ops talent if you don't have hard problems

## hard problems

- extreme reliability
- extreme scalability
- extreme security requirements
- solving operational category probems for the whole internet (platforms, services)

- Congratulations: if you got to this point, you must be doing things right

## What makes a good startup ops hire?

- haha, great slide: you want someone who knows all the things, will work for snacks. YOu want a unicorn
- But you can't have that. You get a person instead and they have strengths and weaknesses
- you need to think really carefully about what strengths are most necessary for you
- one thing ops engineers are really good at is learning

### Qualities of great ops engineers

 - strong automation instincts
 - ownership over their systems
 - strong opinions, weakly held. not dogmatic. "nothing worse than a religious zealot"
 - simplify simplify simplify
   - "complexity exacts a staggering tax on your humans"
 - excellent communication skills, calm in a crisis
 - they value process
 - empathy

### things that do NOT predict great startup ops engineers

 - great at whiteboarding code
 - any particular technology or language
 - any particular degree
 - big company pedigree

 - the bigger the company, the less that those engineers live in the real world
   - they're relying on an enormous iceberg of tech that other teams are maintaining for them
   - learned helplessness can set in if you've been at a big co. for a long time

### differences between large and small co.s

 - succeeds at big co:
   - structured roadmap
   - executes well on small, coherent slices
   - classical cs backgrounds
   - value cleanliness and correctness
   - technical depth

## Interviewing for these small startup ops qualities

 - first, interviewing is really hard
 - we're much better at looking for reasons to say No to someone than to say Yes to someone and see and develop their potential

 - read "The hard things about hard things" by ben horowitz
 - figure out what strengths you really need and hire for those
 - **don't hire for lack of weaknesses**
 - If you're hiring a founding team member, look for people who are capable of growing a team, growing into a leadership role, and you may need to trade off on other skills to get that

### Interview questions

Good:

- establish technical range
- probe teh candidate's self reported strengths
- related to your real problems
- leading questions with many good answers
- ask culture questions, screen for learned helplessness
  - learned helplessness is like cryptonite for a startup

examples: what is the most catastrophic mistake you've ever caused, and what did you learn from it?
- your site is getting slower, and latency is twice what it was this time yesterday. where do you start?

- ask how they felt about former jobs and coworkers (best and worst things)
  - listen for lots of complaints
  - if they're complaining, and you ask "ok, how did you try to fix it", and they didn't, that's a sign

Bad:

- depend on a specific technology
- look for a reason to deny a candidate
- designed to trip them up
- deny candidates the resources they would use to solve something in the real world

## You've hired them. Now what?

- you don't just take your SWEs out of ops
- SWEs should still own their stuff in prod
- ops engineers should be resources for SWEs, but doesn't mean they maintain apps for SWEs
-


## How to spot bad ops engineers

- tweaking indefinitely and pointlessly
- walling off prod from developers
- adding complexity
  - "this is my #1 complaint about most people using docker right now" <-- hahaha
- won't admit they don't know things
- disconnected from customer experience

## How to lose good ops engineers

- all the responsibility, none of the authority
- all the tedious shitworks
- blameful culture
- no interesting operational problems
- not having the SWEs helping them

She ends with:

"Treat your people well"

- not talking about startupy stuff... foosball, snacks, etc
- work/life balance, vacation, good schedules, caring about them as people

- she tells a story about a startup CEO praising engineers for working late, heroism
- the patterns that you praise will become your culture

**Having people who want to work for you is a superpower**