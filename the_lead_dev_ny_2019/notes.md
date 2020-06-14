engineering ladders

marco rogers

slide deck is full of tips

modular monoliths -- shopify

this was  a talk version of her blog post (we read that a while back and shared it... excellent)

- wanted to keep the number of deployable units small while enforcing boundaries between different functional parts of the codebase
  - originally codebase structured by software concepts (controllers, models, services)
  - moved to codebase structured by functional components (tax, shipping, blah blah... see the blog post)
- she talks about why microservices weren't right for them and that they quickly dismissed them, but does acknowledge that modular monolith is a pattern that will help in moving to microservices should that become desirable
- it's taken them years to transition their monolith to modular
- they built tooling to help them capture data on the state of their componentization (ruby-based) and plan to open source it at some point

taming complexity

- liz fong-jones

- Talks about the problem where complexity leads to broken shit and unplanned work and no time for projects
- Her perspective is that "we forgot who runs systems"... too much focus on tools and not enough on the people who run the systems
- Production excellence takes planning; how do you get to a state where people are happy to be on-call?
- service level objectives (NOT SLA): a good SLO barely keeps users happy. 
- and you can drive alerting with SLOs
- this gives a budget for errors, i.e. allowed unavailability
- thus response can be "page if you're going to run out of budget in hours, but ticket if it's days until running out of budget"
- this helps teams decide whether to work on feature backlog or reliability backlog
- any SLO that you're measuring is better than No SLO. Don't need to start with a perfect SLO. Even if you're just starting with measuring http 200s, then evolve to RUM and synthetics
- Question for me: can New Relic synthetics do this kind of thing? is that what Apdex is, really?

Debugging in production
- you can't predict all the types of bugs you'll see in prod
- need to develop techniques for debugging new types of bugs
- this is about testing hypotheses in prod
- dive into data to ask new questions... which means services must be observable
- this means: systems produce enough telemetry that they explain themselves to us without us having to add new stuff and redeploy to get the answers
- examining events in context
- Debugging is a shared activity, you don't do it alone in isolation
- not just devs, either... customer support, too, all collaborating on debugging
- Service ownership doesn't mean service selfishness... "don't ship your org chart"
- reward curiosity and teamwork... publicly thank people for asking questions and sharing knowledge
- "outages don't repeat, but they rhyme"
- Outages that are frequent and severe are probably your most significant risks, so use that as a guide for what to to fix
- think about reducing the impact of failures vs. the frequency of failures

Systemic Risks
- lack of observability is a systemic risk
- if every outage takes long to resolve because people can't find the right dashboards, can't find the docs, can't get the information they need, that is a systemic risks
- how do you make it easier for engineers to understand production?
- if people don't feel safe reporting problems to engineering, that's a systemic risk



Communicating and documenting architectural decisions

David Ayers

Lightweight architectural decision records

- "why did we decide to do it this way?"
- and socializing those decisions with the group, so that the reasons for your decisions extend beyond the team who made the decision
- ADRs... architectural decision records. See Michael Nygard. A way and a location for this type of documentation, as close to the code as possible
- Note: I am dubious about this idea that wikis are where stuff goes to die
- The important thing here is capturing the why of the decision, and the context around the decision... what our world was like at the time that led us to decide such and such
- this helps future people make different decisions if context changes

ADR
- text document, usually markdown
- one ADR per file; his website has links to examples of these, with format
- `adr` directory lives beside `src`
- short and to the point
- ThoughtWorks tech radar suggests adopting ADR

Broader decisions that apply to multiple projects
- they created a git repo called technical architecture
- i.e. "here's our pull request process", "here's why and how we use docker for deploys" 
- Re-uses existing code review process


Enterprise Architecture Guilds

- "guild": group of like-minded people who get together and talk about things... sounds like a community of practice, in our speak
- making decisions in a group like this. 3 different "sizes" of decision-making
  1. someone recommends a change; they write an ADR for it
  2. Form short-term special interest groups; they meet weekly or whatever for as long as they need; build reference implementations, show how to do the thing. then they dissolve
  3. long-running special interest groups
    - eg where he was (The Container Store), they had 3 different languages, so they had 3 language SIGs that talked about code standards, linting, etc
- The guild helped with socializing decisions, which is a very hard problem; so the people who were part of making the decision had skin in the game for socializing it
  - there's no one way that will socialize; requires a litany of ways
  - published a newsletter each month that published all the ADRs
- Meeting structure
  - reports from each sig
  - discuss whether short-term sigs have reached EOL
  - review open ADRs and make a decision to accept, reject, send back for more work
  - open discussion
- NOTE TO SELF: when this talk comes out, send to bill shelton... this sounds a lot like his idea of centers of excellence in a product-organized T&I

Reference Implementations

- RIs / Reference Applications bake in best practices
- need to be careful not to make it all seem like magic... this is helping people get started 
- helps bake in best practices around linting rules, integrating security, logging, apm, etc
- "everything you need to get started just writing code"
- there is an implicit commitment to maintain these things... ADRs, RIs, etc
- the Long-term SIG owned these things
- the RI also became a playground for trying new things


Tracer Bullets / Steel Thread

- as you begin to build something, you're building the simplest possible thing that exercises all these components
  - holy shit: this is basically what we're doing with the Intranet and Okta/sso stuff right now



Managing the burnout burndown

Anjuan Simmons and Dr. Aneika Simmons

- Go check out "lending privilege" talk from lead dev ny from a few years ago by anjuan simmons


Dimensions of Burnout

- Emotional exhaustion
  - sense your emotional resources are being fully consumed by the work you do. when you get home you have nothing left to give to the other people in your life
- Depersonalization
  - cynicism
- Reduced personal accomplishment
  - tendency to evaluate oneself negatively particularly with regard to your work

Engaged but burned out
- engagement is NOT the antonym to burned out
- it's possible to be engaged and love your job but also be burned out and looking to get out and find another job
- Why? "the wrath of workism"

Wrath of workism

- many people have work as the center of their lives, and everything else revolves around their work
- derive so much of our dignity from work
- problem is that people who are so wrapped up in deriving worth from work means that when something goes wrong at work, everything can feel like it's falling apart
- how to burn someone out: hire a motivated person and then don't give them the opportunity to feel valuable or doing the work they want to do. eventually they feel helpless, and the result is burnout



Managing burnout

- He talks about how tech companies design offices so that developers feel like royalty, and don't want to leave the office, b/c of all the goodies that are there

three-part framework for helping manage burnout 

the framing here is applying the agile burndown chart idea to managing burnout

As a manager, you have to burn down barriers, distraction, and illness

Burning down barriers

- "if you want to go fast, go alone; if you want to go far, go together"
- including teams in solving problems that affect the team

Burning down distractions
- attention is a finite thing, lots of competition for it
- know your values, and focus your attention on things in line with your values
- this is also about knowing what to say no to. What stuff that we do is aligned with what we really care about

Burning down illness

- "health is the true wealth"
- we often trade our health for productivity (in the short term)
- sleep, eat right, exercise, not overworking by enforcing no-work times

Practice over perfection
- you won't ever perfect the balance, but you can interrogate your life and practice balance
- help your team protect their hearts, minds, bodies
- healthy teams make healthy code



Being right is only half the battle

Rod Begbie

the secret to career growth is having an increasing amount of influence over people and direction

Three superpowers

1) ask questions

- you can only really influence people if you understand them
- repeat back what you heard to confirm you understood
- getting clarity on what success looks like, or what done looks like. "when you say done by end of day wednesday, what's that mean specifically?"
  - "what does ____ mean to you?"
- being iterative: not "how do I go from 4 to 10 on an increase in performance" but "how do we get from 4 to 5"
- asking questions gets people talking, and you start to build trust and rapport and understanding

2) Strategy, and tradeoffs, and getting clear on what matters most
- when done well and at the right level, strategies are your best friend for driving change
- the "even / over" statement. We will value "this" even over "that"
  - amazon's 1997 shareholder letter: "we're going to favor long term growth even over short term growth"
  - this empowers amazon's employees to evaluate tradeoffs
- the key to turning even-over into strategy, though, is to write it down and share it
- there are probably a ton of assumptions about what you and your team values
- when these things are explicit, the team can start to make decisions without your needing to micromanage


3) Socializing ideas early

- get feedback on ideas early; don't wait till it's perfect
- don't roll into a big meeting where you're trying to convince people of something without talking to them first or otherwise socializing your ideas
- "how would you react if i said..."; "what would worry you if I said...."
- don't limit yourself to allies. Go find the meanest scariest grumpiest people and get feedback from them
- don't just get feedback from peers; go up down sideways, even the stakeholders you're trying to convince
- this is how your idea can just become "the truth" by the time you get to that big meeting
- document decisions made and share them as widely as possible
- this is true for big and small stuff, even if it's an email after a meeting "Hey joe here's what I think we agreed to, did I capture that correctly"
- if you have a decision-making meeting, get your team in a huddle beforehand and agree to what you're going to talk about. you don't want your team falling into disarray in front of the stakeholder


Being glue

Tanya Reilly

This is based on her blog post (or slide deck, I can't remember) from a while back

this is a talk about fairness

This is such a great talk and I can't capture it.

I love the idea of asking an engineer who appears not to be coding much... what else is filling up the time. In Tanya's example, this is where you see how much "glue" work this person is doing

But this is also a communication breakdown on the part of the manager, for not being clear about what promotable looks like. in Tanya's example, the problem here is that the glue person thought they were doing the right thing, but the manager thought they weren't doing engineering work and therefore not promotable work. so it was an expectations gap


Question... who should do the glue work?

A large percentage of your owrk should be the thing you're evaluated on

non-promotable work will always be a thing.. make sure it's spread equitably

Choosing your future

- Shoot for jobs that have the skills you want to get better at, not what you're already good at

- You probably shouldn't be shooting for roles you're 100% qualified for. Most of what we learn is on the job
- on day one, we're probably only just-ok at the job

- what will you feel happy and proud to do?

- Project managers are routinely understimated by engineers... don't do that

- the three least useful words: you're "not technical enough". what does that even mean? 

- what doors are OK to close? (i.e. roles you leave that are hard to re-enter later)


what to do when you're glue

- this assumes you are in the specific situation this fictional eprson is in: not promoted b/c of doing glue work, but you want to stay an engineer 

1. have that career conversation
  - what does promotable look like in the org, based on the org's career ladder
2. get a useful title
  - if you're staying in this role and doing more glue work, get a title that matters and might open doors elsewhere. job titles are super important for non-privileged classes
3. tell the story
  - advocating for herself, and not being afraid to tell about that
  - manager should be telling the same story, and publicly giving credit... and not for "helping" but for making it happen
4. if you're not getting promoted for doing glue work, stop doing it, even if just for a while. "work to rule"... just do the promotable work. Do exactly the thing on the job ladder. 
  - "until that promotion is out of the way, declare all the glue work 'not my problem'". Stop helping. Crucially, don't catch things that are about to drop. Stop being the unofficial lead.

5. learn deliberately: you only get better at what you spend your time on
  - be deliberate about where you spend your learning time


Senior people / team norms: be transparent about how and what you're learning on the job; and also don't take learning opportunities away from other people

She brings this full circle about how the glue person at teh beginning of the talk, who did the communication work etc on the team, was letting those other devs (who did get promoted) get away with not building the skills they needed




Resilience engineering mythbusting

will gallego, fastly


I really enjoyed this lightning talk; didn't take notes though





Remote-first teams

Nassim Kammah, Mailchimp


HA. I interviewed with this dude a few years ago



Problem: "remotes" are seen as friction
- pain in the ass to deal with the remote people on calls, across time zones, etc


he's recommending solving this problem with a remote-first collaboration model

Frictions caused by remotes:

- meetings
- enabling deep work
- maintaining common ground



Meetings

- "caucus meeting" -- bit.ly/chelsea-troy-meetings
- no rules on who talks, in what order, for how long
- the caucus rule: the first person to utter something gets the floor
- high caucus score: impromptu speakers, high influence, think on their feet
- low caucus score: thoughtful about wors, gets interrupted, avoids devils advocate
- caucus rewards folks who jump in

- this style is really hard for a remote person especially if they're a rate remote on a co-located meeting
- he recommends that for this style of meeting, try room dialed in, but everyone on video
- also, have a moderator for the meeting... safeguards everyone's opportunities to speak and mitigates the problems with the caucus style
- no big deal.. can be a team member, just make it someone's job for that meeting

- summary: moderator + video dialed in... prevents meeting hijacks, lets everyone read body language


Time zones and deep work

- one of a manager's job is to shield the team from distractions
- you probably don't want to dictate slack/chat behavior for a team, but you can establish expectations around availability. this gives permission to turn slack off during not-those-hours, i.e. "slack quiet hours", and in this quiet hours idea you explicitly don't chat


Maintaining Common Ground


bit.ly/dan-slimmon -- troubleshooting on distributed teams

He talks about all the assumptions we have that let us use short cuts when we communicate
- mutual knowledge, beliefs, assumptions
- the slack changelog, and he talks about the mechanics for doing it
- it's basically a way of using reacji plugin and some additional writing for piping summaries of threads into a separate slack room for helping people catch up when they return to chat (when theyre away for hours or days)


takeaway: remote-first practices benefit everyone



Leading engineering teams through massive rapid change

Yvette Pasqua, CTO meetup

- grow your network and learn from others, for peer coaching, advice and support

Framework for leading teams through change

1. Time phase
2. Leadership qualities

Three time phases

1. acute phase
  - short period of time following an event that sparks rapid change
2. rapid change
3. new normal


Three leadership qualities

1. communication
2. motivation
3. focus

optimize for them differently depending on the time phase we're in and what the organization needs from us as leaders


Things you might need to optimize for / think about with communication

- 2-way vs 1-way
- written vs in person
- how transparent?
- how much empathy?
- how much context to share?


motivation

- inspiration, values, vision & strategy, empowerment vs direction, clear goal setting


focus

- investment in intiatives
- business model & revenu
- execution and delivery
- ruthless prioritization
- financial health metrics


She has a 9-quadrant tic-tac-toe looking box to visualize this framework

Her story here is after meetup got acquired by WeWork. So the acquisition is the rapid change event here

I took a picture



Crucial career conversations: a framework in practice

Adrienne Lowe - Director of Engineering - Juice Analytics  leadingwithspoons.com

Career conversations are a growth management tool to learn more about how your direct reports want to grow

you can use this to help them find the right spot on your team, unstick them if they're stuck

without care, these meetings can lack purpose and impact, if we treat them as a box checking exercise

Career conversations are crucial conversations... conversations that matter

this is kimball scott's framework from Radical Candor

But she is departing from it... she'll tell when that happens


This is a talk about how one team put a theory into practice


The Framework

- the life story
- the dreams conversation
- the 18 month plan

these are difficult conversations to have

one of the big goals of the life story is that you learn what motivates them... you hear what motivated the decisions they've made in the past

the dreams conversation can be very hard... it's not rooted in fact, just imagination. can be very hard especially if you're admitting you're not where you want to be


so after these very hard conversations, you start to work on the 18 month plan

building trust

- It's going to be very hard to have any of these conversations if you havent already been having 1:1s
- building a culture where it's safe to fail
- be aware of the power imbalance in these conversations, and try to soften it
- they can't be afraid that if they tell you something, they'll lose your favor... people need to feel safe to speak truth to you


She had the "life story" conversation and it went great

She tried having the dreams conversation, and it flopped

She asked herself what her goal was, and it was really to help her people figure out what they wanted to Start Doing, and Stop Doing


So, scenario: youre interviewing for your dream job:

"what's something you love doing at your current job that you still get to do here?" -- hiring manager at dream job

Stop doing..

talking to a friend, friend asks "what's really frustrating about your job right now?"

- acting like they were talking to a friend made it safer and easier


So all of that ^^^ replaced the "dreams" conversation

So, on to the 18 month plan... and then....

she threw it out. realized it wasn't useful for them. 

what she was hearing from her team was that they just wanted to work on a great team

She then created a 1:1 profile for each person, with 6 questions

She drafted it and got feedback from each person; i.e. she "workshopped" it with them, using the input from the previous conversations and previous 1:1s

Then, they shared them with the rest of the team

- she had them read aloud the "what excites me" section to the team, thought that was really special

You've got to put in the work, too. You have to model this to the team. this helps create psychological safety

You (the manager) should also write down your life story, write down your dreams, and email what you wrote to your direct reports

Also, answer the questions on the 1:1 profile, but be mindful of too much emphasize on this and having your biases out there so strongly b/c it can have such an influence on the team

Don't fall into the trap of using all of this to focus on some far off future. Stay in the present

