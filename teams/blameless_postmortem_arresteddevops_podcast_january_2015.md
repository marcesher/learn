

Mike Rembetsy: orgs understimate the stress caused by surprise

- service disruptions are not a chicken-running-around thing. it's calm. the focus is on fixing the problem
- after the problem is fixed, that's when the learning starts
- the point of the postmortem is to learn
- the point of a postmortem isn't to do the whole "how can we ensure this never happens again"
- the benefit is on the human / learning side
- yes, technical remediations will arise; but that's secondary to the human bits

- during the post mortem, trying to figure out what the human's context was at the time
- this is all straight outta dekker

Matt Stratton: we assume, as an industry, that if we break something (bring site down) we're going to get in trouble

- asks: how do you help people through that cultural change?

Dave Zwieback:

- his problem with 5 whys is that it's arbitrary. Falsely think you can get to a root cause.
- he says: root causes don't really exist
- someone changed something, and shit broke. "someone moved my cheese"
- the fact that systems can change is the cause of this. He disagrees with allspaw
a bit on this 5 whys thing in that he says the root cause does exist... it's the mutability of systems
- but that mutability is necessary

Mike seems to say this is bullshit

- example: hard drive dies. did some change cause it to die?

- IMO: this is a rabbit hole. Not useful, for this topic right now. Move on, please


Mike:

- no hard/fast rules on when to have post mortem
- definitely for high-severity stuff
- if it wasn't public facing, maybe, maybe not. but if there's stuff to learn, sure

Trevor Hess:

 - how long after the event should a post mortem happen?

Dave says not more than 2 weeks or so

Matt Stratton worries that doing it right away will be too early... maybe people still have feels

Mike says: when you have an emotional hijacking, that's not the time

At etsy, they ask: "are you triggered?" to determine whether people are OK to think clearly

Mike's example: you spent a ton of time developing a feature, and it crapped out in prod in the morning, that afternoon isn't the time for a post mortem b/c one comment might set you off

Dave: at start of postmortem, they recite a list of things:

  - this is about learning, not blame, these are complex systems
  - we're looking back in time, so we'll have all these biases in play
  - at the beginning of a highly charged post mortem, what works well is empathy and humor. "Congratulations on really fucking this one up!".. levity
  - "I've done this too. No biggie. Relax"


Mike doesn't like notion of a "moderator" on a postmortem. Facilitator, OK.

Dave says you want a lot of diverse opinions in the room. A facilitator can help pull all those opinions together


You can do postmortems for all kinds of things

- if you have a problem and construct a timeline, you can do it

- this is why they created "morgue"


Mike:

"Operability Review"

- this is pre- Go Live
- go/no-go call


Dave:

- "What could possibly go wrong?"
- but people tend to be overly optimistic here
- people think generally things will go well
- mentions a "pre-mortem", which structures the question differently

- imagine we deploy this feature, and things go really badly. We end up on front page of new york times bad. Imagine that scenario in advance, and then...

- then ask: what went wrong?

- he says the answers that come from this end up being a lot different.
- He says it harnesses hindsight biases, but in the future


Mike:

- they started their post mortems on a wiki page
- wikis are wehre docs go to die
- it kept getting longer adn longer adn longer

- so they built "Morgue"
