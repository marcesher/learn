

# Problems

  - function chains make poor machines
  - real world concurrency is exposed via callback APIs

# The Premise

  - goood programs should be made out of processes and queues
  - conveyance must become first-class
  - comes a time in all good programs when components or subsystems must stop communicating directly with one another

  **BUT**

  - juc queues only coordinate via blocking thread control
  - you must block a real thread on the end
  - no threads and thus no queues in JS

## Thread overheads

  - stack size
    - a problem when very many threads
    - N.B. this is not a scalability problem, it is an efficiency problem
      - scalability is not about what happens inside one machine, but multiple machines
  - wake-up time

## Events / Callbacks

  - Listenable Futures / promises
  - a web of direct-connect relationships
  - difficult to reason about or control flow
  - fragmented logic, callback hell
  - "all the ick from long ago" -- HA!
  - and so on

  - bottom line: pain in the ass
  - breaking a thing into separate pieces, to stick them into handlers, breaks up that "one thing" which was at one time easy to reason about
  - and that's just an artifact of the programming language / system, not the actual problem domain
  - if you'er trying to make a state machine with multiple sources, you can't just get it out of filter/map composition primitives

## Call chains as machines

  - stuff comes from somewhere else (input)
  - some logic goes into a handler for the input
  - going to have to produce shared state to coordinate multiple event streams
  - Objects don't fix this, he says

## C# style async

 - attempts to reinvert control
 - turns linear code into callback / state machine for you
 - so your code looks ordinary, but the IOC happens under the hood
 - So, copying that isn't a bad idea
   - Scala did this, for example
 - shows an example of what this might look like in clojure

 **Problem**

 - This is just Sugar
 - promises / futures are the one-night stands of architectural constructs
 - can't model enduring relationships
 - not much help for external events

## Queues / channels

 - decouple producers and consumers
 - first class
 - enduring
 - monitorable
 - multi-reader / writer

 **This is not new**

 - CSP (Hoare, 1978)
 - CSP vs Actors, is basically the choice
 - core.async bet on CSP
 - blocking semantics by default
   - can also be used for coordination, not just conveyance (conveying something from producer to consumer)
 - Go is the most recent to make CSP first-class

 **More cool stuff**

 - support "choice" by "select" or "alt"
   - you can wait for one or more of a set of I/O operations on channels
   - including writes and timer


## The challenge

 - create a channels API for Clojure AND ClojureScript
 - similar calls support both
   - real threads, real blocking
   - macro-generated IOC... thread relinquishing, thread pools, callbacks)

## The opportunity

 - support reasonable model across spectrum
   - traditional threaded apps
   - high connection count servers
   - event-driven things such as vert.x

## core.async

 - A Library
 - independent 'threads' of activity
   - real threads and IOC
   - semantics of real vs ioc threads are the same
 - queue-like channels

### Threads and blocking

   (thread body ...)

   - real thread, real blocking
   - can get high throughput (if you know what you're doing)

   (go body....)

   - IOC thread, state machine, parking
   - parking relinquishes the thread and parks it for resumption later

### Channels

  - queue-like
  - put stuff on one end, take it off the other
  - blocking
  - multi-writer and multi-reader (block on both sides)


  - Channel API
    - just look at the API, not my notes
    -Put:
      - (>! ch val) is the parking variant
      - (>!! ch val); blocking equivalent, not in JS
    - Get:
      - (<! ...)
      - (<!! ...)

  **Buffers**

  - unbuffered == rendezvous
  - fixed will block puts when full
  - fixed variants (never block): (sliding-buffer), (dropping-buffer)
    - these let you provide a policy for what to do when full
    - maybe down the road there will be different policies
  - they will never provide unbounded buffers because that's a recipe for a broken program

  **Choice**

  - use alt()... (alts! ops), (alts!! ops)
  - One and only one op will complete
  - alt is a macro, not a function
  - alt supports priority
  - this is very cool! you basically pass it a number of different operations to run; it runs them in parallel,a nd whichever finishes first gets returned; can provide a default if none finish successfully otherwise it'll block till one of the operations succeed

  **Timeouts**

  - they're just channels (copied from Go)
  - (timeout msecs)
  - returns a channel that closes after msecs
  - include take of timeout in alt()
  - tieout channels can be shared

  **The Browser**

  - "friends don't let friends put logic in handlers"
  - clojurescript + core.async restores separation


# Direct vs Indirect
  - see his slide for the visual
  - indirect lets you keep your logic all together