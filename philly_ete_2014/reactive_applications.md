Go Reactive

the future of programming

Roland Kuhn (akka lead)

# Reactive traits

- responsive
- resilient
- event-driven
- scalable

see reactivemanifesto.org



# Starting Point: The User

The user motivates this whole journey. They're why the app exists

Typically, it's a human in front of web browser

We know that the browser is just the starting point, and that behind the browser is all manner of things
  - frontend servers talking to lots of other stuff... databases, internal service, external services, blah blah

Responsiveness:

  - always available, interactive, near-real-time
  - a service which does not respond is effectively unavailable, even if it does its job and you just can't see the result

  - HOW?

    - Bounded latency between request and response
    - How to reduce latency?
      - parallelize if possible
        - it's possible if A, B, and C do not depend on each other
        - typical fan-out/aggregate approach
        - on the JDK, this means Futures
        - in Java 8, we now have CompletableFuture
        - Note to self: I gotta check out all the new concurrency stuff in java 8!

      - however, you're bounded in the number of threads you can create
      - kuhn says the answer to all of this is event-driven programming

    - use circuit breakers for graceful degradation
      - between services, you need something like an SLA
        - if a service takes longer than its SLA, react (fail fast, don't keep waiting)
        - this is how you avoid cascading failures

    - use bounded queues, measure flow rates

      - latency = queue length * processing time (for reasonably stable average processing time)

      - what do you do when you hit the queue limit?
        - same thing as if a circuit breaker had tripped... respond with a failure, temporarily unavailable, etc
        - You can only do this if you make the queues explicit!
        - kuhn says you can only make them explicit if you design the system to be event-driven

Resilience: Responsive in the face of failure

 - software, hardware, and humans will fail
 - systems stil need to respond... this is resilience
 - the only way to achieve resilience is to distribute
 - distributed systems are the key to fault tolerance

 - compartmentalize failures... we don't want ripple effect failures by passing failure around to other components
   - compartmentalize systems so that they can fail in isolation
   - "distributed systems are systems where parts can fail individually"
   - he tells about the titanic, and how the bulkheads didn't go the whole way to the top and consequently the water spilled from one compartment to the next.. .this is cascading failure
   - consequently, compartmentalization needs to be complete

 - calls need timeouts... hanging forever is not good. it might not be clear exactly what went wrong, but something definitely needs to go wrong... something needs to "happen"
 - "somebody else's exception" ---> Supervision
   - he tells a vending machine example
     - if water is out of stock, it tells you
     - if you don't have the right money amount, it tells you
     - if someone sticks gum in the money slot, the machine won't tell you anything
     - if logic board on machine is broken, it can't tell you anything
     - i.e. when the machine is broken and can't operate, the user can't fix it... the machine's operator must

   - Failure doesn't go to the user of the system, but to the operator of the system
   - the system must now obey two different kinds of communications: request/response and failures

   - again, kuhn says the only way to do this is with event-driven systems
   - gives example of akka actors, which have location transparency, leading to seamless resilience

 Handling Load

   - need distributed nodes
   - this is why location transparency is important
     - your program doesn't know about the fact that actors are on different systems/cpus/whatever
   - tells about how netflix scales down during low-traffic hours, to save cost
   - the means exist right now to be really responsive to changing load, in the order of adding many many nodes in minutes


Consequences of going distributed

 - loss of strong consistency
 - he says CAP not as relevant as you think
   - he recommends reading Brewer's original article
   - also, read peter bailis Probabilistically bounded staleness (pbs.cs.berkeley.edu)
 - if you can tolerate even a little inconsistency, you can be perfectly available
 - eventual consistency: there's a time window in which you can see inconsistency, and eventually it will become fully consistent
   - gossip, heartbeans, dissemination of change
   - this is how akka clusters, dynamo, riak, etc are implemented
   - scales much better compared with distributed transactions
 - naturally, kuhn says this requires event-driven systems

Corollary

 - reactive needs to be applied all the way down
 - it'll be ruined by having one component that doesn't obey by the rules
 - he says we need more async APIs to help here. Apparently mysql and postgres now have async apis
 - polyglot deployments demand collaboration
   - for example, Reactive Streams (Kuhn is talking about reactive streams project tomorrow)

What about us, the developers?

  1. Take a leap of faith
    - we've been burned by thread-based models
    - example, Future.get() is so nice b/c we can handle the result in the same thread via blocking
    - going reactive means becoming comfortable with doing things async

    - **it's OK to write a method that returns a future!**

  2. Rethink the Architecture

    - break out of synch blocking prison
    - focus on communication and protocols
      - we think explicitly about how systems collaborate, rather than an imperative sequence of steps in a sync program
    - async program flow
      - no step-through debugging, though. step debuggers can also lead to heisen-behavior... simply attaching a debugger can slow a program down enough that the bug goes away
      - need tracing and monitoring in place of step debuggers
    - **loose coupling**

  3. Profit!
    - business logic can be clean b/c failures go to the supervisor, not the user. separates business logic from failure handling
      - failure handling is about restorign service after something's gone wrong

    - when units of work become compartmentalized and only communicate through messages, they become trivially distributable across cores, cpus, machines, etc
    - this leads to effortless parallelization
    -






