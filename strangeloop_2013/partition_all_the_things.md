Kyle Kingsbury

@aphyr

Network Partitions

"it's going to get weird"

github.com/aphyr/jepsen


**Partitions are real**

- MS says they see 40.8 link failures per day
- redundancy improves packet loss by only 43%
- Google says in a first year of a cluster, they get all kinds of loss (see slides)

Causes

- gc pauses, network maint, segfaults and crashes, faulty nics (broadcom notorious for dropping packets under high loads), bridge loops
- spanning tree problems, hosted networks, and so on and so on

- recently, many companies have written up post mortems about hwo they dealt with partitions

- distributed systems are going to fail, where parts work, parts don't


# Jepsen

  - named after carly rae
  - this project is his exploration into partitioning


MongoDB: ouch!
  - all consistency levels led to lost data
  -

Redis:
 - split brain upon partition
 - not even close to consistent

Riak

 - last write wins means dropping writes
 - use CRDTs


Zookeeper

  - detects partitions quickly
  - writes immediately fail
  - only partly available, which is what you expect from a CP system
  - very well behaved system for CP

  - use it, he says
  - use curator with it

NuoDB

 - "this is gonna be good"
 - distributed but not sharded
   - whole db lives on every node
 - complex design
 - claims to be any or none of c, a, and p
 - race conditions in join if you join nodes in wrong order
   - like split brain, but quiet
 - basically impossible to start reliably
 - can join a node to itself
 - difficult db to work with operationally

 - there is a silver lining
   - 55% acknowledged
   - 0 false positives
   - 0.1% false negatives

 - but the problem here is the latency
 - during a partition, nothing can take place
 - but, they are working on liveness detection and many of these bugs


Kafka

 - it's a messaging system
 - durable queues,  immutable logs of messages
 - now has replication
   -but it claims it's "CA"
   -wat?
 - in a shard, there's an in-sync replica
 - 50% false positives

 - long story short, use majorities
 - kafka is still early days, and Kyle thinks they're moving in the right direction and will get it right. He really likes this system and where it's going


Cassandra

 - 27% false positives
 - I gave up trying to take notes on this
 - he really digs into cassandra's claim to be isolated

 - says to use cassandra's "lightweight transactions"
 - not supported in java driver, just python and even then only in thrift interface

 - Strategies:

  - it's a very good and mature database
  - use as a strict AP store
  - no isolation guarantees for writes
  - avoid transactions for the foreseeable future
  - good for logging and storage


Takeaways:

- don't rely just on his numbers
- this is about a methodology for breaking your systems and determining how they'll respond
- "how do we rely on clocks?"
- "what if the network delivers a message late?"
- "what if there's no majority"?
- "what safety and liveness guarantees does this system need and provide?"
- data loss and inconsistency can be OK... depends on your system
- balance complexity with correctness
- Write a test program! make reads, make writes, log what happens, and measure that what you expect to happen actually does
