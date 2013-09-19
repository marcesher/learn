# Graph computing at scale

- Matthias Broecheler, Aurelius

- Humans are very good at associative memory

- Human Brain and Computer are better at different things

- Recalling the name and highest degree of the current US president is trivial and fast for a human

- Doing the same for a machine, i.e. relational database, is harder and represented by multiple joins

- computing the avg term length of a US president since 1980 is trivial for a relational DB... much harder for a human

Why this impedance mismatch?


- This is where graph DBs come in

-  A Graph consists of:

  - vertices (cirles)
  - edges (arcs between circles)

 - properties decorate the vertices and edges
  - name of president, term dates, etc

# Query language: Gremlin

 - on a graph, the query operates associatively
 - starting at a vertex, start to traverse the graph
 - the language mirrors the way you would internally think about it
   - if you "trace your steps" about how you actually arrived at the answer, it'd look something like this query language


# Network science

 - desire to understand a seemingly hopelessly complex system (in the mathematical sense)
 - system made of **many** nonidentical elements connected by diverse **interactions**


 - social networks, financial systems, biological systems... all are complex

 - can't solve cancer by looking at one specific part of the body... requires a holistic view

 - Broecheler's interest was in trying to give human's an easyish way to analyze complex systems

# Titan

 - distributed graph computing at scale
 - he wants graphs to become part of our every day problem solving, kinda like a hashmap
 - they should be an important datatype to us
 - titan.thinkaurelius.com

 - inspired by the most amazing graph computer he knows of: the human brain
 - tries to get around the problem of sequentiality that current computer architectures impose

## Our Brain

  - highly concurrent distributed system, though we're not aware of it
  - typically, most of our brain is not active

## NoSQL

  - titan built on top of cassandra and hbase
  - question: how do you assign vertices to individual machines? IOW, how do you partition the data?

  - the brain is amazing at this
  - research shows how the brain reallocates different centers if it needs to
    - blind people... the brain reallocates the visual cortext for other senses, for example

  - titan tries to avoid hotspots in the system by reallocating resources
    - not a solved problem, however

  -
