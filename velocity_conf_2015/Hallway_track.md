Notes from conversations I had at Velocity

- Teams having Office Hours
  - every team in this guy's company (?) has office hours
  - time where the team is open for interruption and they're not heads down on work... interruption is welcome and expected

- Asked a guy about who in their team "writes the puppets".
  - he says it's a mix; it might be there devops team, but it also might be the app devs themselves if they're sufficiently advanced and interested
  - re: their devs and ops, he says devs own their stuff in prod; the devops team is there to help them, to build platforms, etc, but the devs operate their software
  - (note to self: I was fuzzy headed and kinda checked out of this conversation... i mostly listened but wasn't as engaged as I should have been; it was over lunch)
  - he said most of the work in puppetizing is in creating the initial manifests; changing them over time isn't that big of a deal
  - standardizing is key, otherwise you're always just building new stuff

- Code freezes at Intuit before tax crunch... can't touch a system even if it has nothing to do with turbotax
  - because the cost of downtime is so friggin' high... knowing that "you can cost us $XYZ/sec of downtime" gives everyone pause about change
  - (these guys were funny)
  - but this doesn't jive with the stuff gene kim talked about re: intuit in 2013 and experiments... that they run a lot of experiments in production during tax time because that's when the users are on the site

- "Tank": intuit's open source load testing platform
  - I asked, when do you need it as opposed to something like jmeter
  - he says when you exceed probably 70 concurrent users or so

- kids and music
  - really fun conversation with a guy about kids and their musical preferences, how they figure out what they like, etc
  - also fun talking about kids and cartoons
  - "fuck you Caillou. You don't know shit"

- Mike Loukides, o'reilly
  - putting on the "Cultivate" conference again, right before oscon (Monday and Tuesday; oscon is m-f, with tutorials on m-t)
    - http://www.oscon.com/open-source-2015/public/content/cultivate#speaker-row
  - "Team Geek": book by oreilly about managing teams (?) or maybe it's just being a better teammate, how teams work. Need to investigate.
    - cool... check it out on safari b/c we get a 3-month subscription with velocity admission
  - he has a phd in literature and taught freshman english... cool!
  - Talked about the challenges of editing certain authors, and the cost of challenging authors not just being in the first book, but in subsequent books... you did a ton of editing work on the first version, and you know the second edition will require the same... A really interesting point I hadn't considered.


- Go BoF at lunch
  - talked about how all of us got into Go
  - Jason (Burberell?; forgot to write it down), new product manager for Go
  - told us they're actively working with JetBrains on the go plugin
  - talking to Yourkit about what kind of interest would be required for them to add Go support
  - I told him that I thought IDE and Profiling were huge gaps right now and improving those stories would help drive adoption
  - talking to another dude at the table about pitfalls of Go. He said he spent a lot of time fighting with mutability (in channels, I think), and that go let him get away with mutating things from different threads. Wish I had prodded him on this more to better understand. It sounds like a case of "yer doin it wrong", but I think his point is that the language didn't prevent him from doing something dumb... not sure
  

