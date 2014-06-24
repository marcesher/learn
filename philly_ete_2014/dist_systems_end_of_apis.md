Chas Emerick

Distributed systems and the end of APIs


Preface:

 - no turnkey solutions yet. His objective here is to lay out the problem, challenges, possible solutions

# Claims

1. networked application API is an unsalvageable anachronism
1. another that I didn't catch

# Definitions

- a dist system is a system comprising multiple processes that must communicate to perform work

- uniformly unintuitively semantics around causality, consistency, and availability
  - this has significant implications for how you architect apps for resiliency

# API

 - strictly nominal description of classes/module/methods. no formalism of operations' semantics... "what's supposed to happen during a network partition", for example

most APIs are: imperative, synchronous, point-to-point, request-response

- primarily focused on programmer convenience
- trying to create an isomorphism to method calls: api.create(arg1, arg2) == post http://blah/create[arg1,arg2]
- ironic that providers of HTTP APIs often offer client libraries for various languages that restore the classic RPC programming interface
  - think python github api, for example
- continues to lull us into thinking we're just making plain old method calls, except it's remote: "don't worry, it's all magic and will just work"

He says: The API is an anachronism

  - intense coupling between client and server and the point to point topology
  - forces 2-party client/server architecture, despise reality of multiple-node distributed system
  - many network failure modes and common computation tasks necessitate asynchrony, yet our APIs try to cover that up
  - disavows the fundamental complexities of distributed systems
   - failure modes, availability considerations / guarantees, consistency choices, data model characteristics
  

# Acknowledge the network... or fail

- You are **not** calling methods locally.
- you have a network in between your client and the target system

- networks have lots of different failure modes
  - partitions
     - complete loss of interconnection
     - offline operations
     - variable latency
  - reordered messages
  - repeated messages

- Your network's problems are your system's problems. 
- this ultimately results in: "My network's problems are your system's problems", or "their network problems are my system's problems"


# Consistency decisions affect everything

- degrees of consensus yield degrees of consistency
  - consensus, roughly, is the agreement of different actors with regards to the state of your application

  - "strict linearizability", sometimes called "single node" consistency, sometimes referred to as "serializability" (think JDBC transaction level)
   - each actor in teh system must acknowledge each write before the system progresses
   - extremely expensive, but it yields consistency semantics we think we're working with intuitively. "I've told this thing to do X, and htis thing to do Y, so I expect X to happen then Y to happen"
  
 - "causal consistency": track temporal relationships between dependent data. "X depends on ABC and X must happen after ABC"... write to database, then a query should see the effect of that write, i.e. read your own writes

 - "eventual consistency": concurrent writes will converge eventually, and eventually different readers will all see the same results

**The choices made here will dictate your system's availability characteristics**


# What do we want?

1. Communication
  - send data between actors in a system

1. Computation
  - act on that data

Everything else is incidental


He says we've been here before, with the move from low-level languages and abstractions (C, assembly) to higher level (python, java) to even higher level now (APIs)

- much of the challenge is identifying what not to do, in identifying proper constraints

- must "rise above the metal" and stop puking shit out over sockets 

- Leslie Lamport describes the distributed systems problem as essentially a physics problem. Certain characteristics of time and the speed of light constrain our options

# Sound approaches

1. consistency as logical monotonicity (CALM theorem)
1. conflict-free replicated data types (CRDTs)

They constrain the types of operations your systems can perform in order to ensure convergence of changes to shared data by uncoordinated concurrent actors

They eliminate network failure modes as a source of error

Based in math... this is not clever implementation details

Semilattices: data structures that are immune to messages being lost, reordered, or delivered multiple times

- he shows a set semilattice as an example (bounded-join semilattice)
- semilattices only accumulate information

semilattices must demonstrate associativity, commutativity, idempotence. 

# Data models are everything

- semilattices expand the set of data structures you can use in a distributed context

- it's much preferable to use these data structures for passing around data in a distributed system, compared with the "impoverished" data structures we use now

- semilattices correlate perfectly with persistent data structures (the data structures behind clojure that share a lot of information)

- histories, rollbacks, consistent snapshots all come for free

  - note this is what David Nolan showed last night at the JS user group, with react and Om and clojurescript persistent data structures



How to use this?

- reify operations into data

instead of api.setName( personId, "chas")

merge {:person-id person-id :name "Chas"} to the CRDT

- operations then become computable, just like any other data: copy tehm, route them, reorder them freely, at any level of the system

- many of the advantages of queues flow from their forcing exactly the same transformation

  - this is the difference between tight coupling between client and api and a producer/consumer relationship with a queue in the middle that doesn't ahve an api but just has data going in and out


# Programming models

- event sourcing, other log structured approaches
- stream based computation (storm, etc)... scatter/gather
- Tuple spaces & other blackboard systems. This is what Chas is most interested in right now
  - "Linda" was the language that was the primary implementation back in the 70s/80s
  - reactive patterns brought to distributed computation
  - operations triggered in response to data arriving that matches a pattern / satisfies a query

- RPC if necessary, but reify operations into data
  - this should be an interop step, not the entire operation

- New languages that assume the semantics of semilattice data structures
  - Bloom
    - Ruby DSL where all the data structures are semilattices
    - all the expressions in the program have no guarantee of order. they all run concurrently


Finally: we want stateless services reactively manipulating a shared substrate of replicated data
  - this supersets all use cases for APIs as currently construed
  - no coordination or coupling between actors
