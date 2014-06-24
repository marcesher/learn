4/22/2014

jeff hodges

distributed systems in production

he's been with twitter since it was 120 people, now 2400

he's hoping these lessons apply at least as well to small companies and systems as to large


# What makes dist. systems different?

 - failure is more common; so common that you'll have to write software differently
   - eg tcp socket timeouts, GC spiralling a single machine causes requests to timeout, socket write succeeds locally, but fails on remote machine
   - master elections not working b/c overloaded, etc

 - what's interesting is that the failures are **partial**, unlike what you see on a non-dist. system

 - in a dist. system, things can be broken but still working

 - "It's slow" is the hardest porblem you'll ever debug
   - there's no one place where "it's slow" happens

 - **metrics** are the only way you can do this
 - and you need time correlation between metrics
 - key to have a standardized way of storing metrics and getting them out of the system

## the problem with profiling

  - it's a snapshot in time
  - but the problems that show up in a dist. system are not the problems that show up during profiling
  - the actual problem could've started way before the time you're actually profiling

## metrics, again

  - deploys should change a metric
  - metrics are how you cross the mental gap between what you think your code does and what it actually does

## logs are liars

  - free-form text logs are the devil in distributed systems
  - common "problems" are overlogged
    - on kernel boot: "I don't really give a fuck about the usb pci ...."
  - uncommon ones are hidden
  - uncommon ones are not logged


## Avoid coordination

  - paxos, gossip, etc are all designed to simply get computers to agree on numbers
  - getting computers to agree on things is very hard
  - avoiding coordination requires horizontal scalability
  - If your problem fits in memory, it's probably trivial (when you'er talking about systems with many machines, not about kernels)

## Back-pressure

 - idea comes from plumbing
 - big water pipes flowing into little pipes
 - when water gets too high pressure, it gets pushed back out
 - like the water pipes, our software has constrained resources it can use to deal with what's coming at it

 - examples:
   - drop new messages on the floor
     - make this a metric, and alert on it!
   - returning documented overload errors until the system clears
      - metrics apply here, too

   - timeouts and exponential back-offs (he says just google this)
     - it's better to fail early and maybe be able to recover than it is to try to keep on taking in work and then completely fail

## Create partial availability

  - search is a great example
  - even if a machine with XYZ indexes is down, you can still return slightly less good search results
  - search systems are also good cases for setting an SLA on how long it's willing to find a result
    - once timeout is reached, just return whatever you were able to find

  - The "Who to Follow" box
    - originally, it'd cause fail whales, even though it was just a little box on the top left
    - in a partially available system, this box simply has a low timeout, and if it doesn't return in time, just don't show the box

## Consider a private messaging database

  - in a messaging app, if enough machines go down, does that mean everyone loses some of their messages? Or do some subset of users lose all their messages and the system is unavailable to them? Or does it mean the user loses just certain conversations?
  - here's a case where you are choosing which partial availability you're shooting for


  - Separate deploys from release, via feature flags
  - you can even roll out infrastructure with feature flags, to slowly roll users to new subsystems
  - this gets you slow, dark rollouts

  - yes, this adds ugliness to the code, but
   - this trades local complexity for global resilience
   - yeah, these if statements... get over it. you're an engineer and you get paid to understand what code does

## Multiple versions are the norm

  - you will have multiple versions of code running. get over it.
  - do canary builds, etc

## Exploit data locality

  - try to work on data that's closer to the code
  - exploit locality in time, too
  - do batching
  - "collapsed forwarding" (google it)... this sounds awesome
    - attaching new requests to requests already in flight if they're seeking the same resource

## Computers are Fast

  - thousands of reqs/sec per machine in 100-ms latency is such a low bar in 2014. Easily.


## Extract services

  -




