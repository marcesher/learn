http://www.youtube.com/watch?v=wyWI3gLpB8o

http://flowcon.org/dl/flowcon-sanfran-2013/slides/AdrianCockcroft_VelocityAndVolumeorSpeedWins.pdf

Adrian Cockcroft (Netflix)

# Velocity and Volume (Speed Wins)

- I love his idea of "peril" in systems, as it relates to developers deploying
- Developers have self-service deploy, but they are responsible.
- metaphor of airbags in cars: if we had spikes that shot out of the steering wheel instead of airbags, that'd cause people to drive a lot safer (it's jokey, but effectively funny)

- basically, this means the dev is on pager duty: they get root access... so they can fix what they broke
- they see a net time reduction as a result of this... less time talking to ops b/c they can fix it themselves; less time fixing things b/c they're more careful

- netflix emphasizes DEVops... starts with developers and they teach them operations

- They removed the vendor cycle.... they either use open source software or write it themselves and open source it
- "Github is our vendor"


- His description of their canary builds is pretty slick.
- they do testing against their canaries and then perform signature analysis to determine whether it's OK to do a full push
- performance testing, median / 90%, etc. Looking to ensure that there are no performance outliers, etc
- they're working on open sourcing this

- Antifragility: continually attack a system to make it stronger
- likens it to going to the gym... the first times, it really hurts, but you keep doing it and you get stronger and stronger
- Always be stressing the system to make it stronger

- See his slides for book recommendations (lots of good looking stuff here)


1. Speed wins
1. Assume broken
  - Speed and scale break everything (hardware and software)
  - software must be written to assume that its endpoints will be unavailable
1. cloud native automation
1. github is your app store (and your resume as a company)