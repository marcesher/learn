Riot Games -- tracking millions of ganks in near real time

- Garrett Eardley

- for last 1.5 years, he's been building a new stats platform

# Growing up

 - 2012

 - Sharded the db
 - But: this creates multiple single points of failure instead of a SPOF which they had previously
 -  key/blob tables to avoid schema changes
 - wider cache; keep more of the dataset hot (in  memory)
 - More regions ( 12 environments throughout the world)


# Today

 - vertical DB (as opposed to horizontal)
   - SSDs, FusionIO, etc
 - Wider cache ... "way way way wider"
 - 30 + regions around the world
 - Pain not solved
 - New Data heavy features is getting difficult

# Challenges to solve

  - remove SPOF
  - remove downtime for hardware / software upgrades
    - be able to remove a node without an outage

  - horizontal scaling
    - needed a persistence layer to let them keep going out and out and out
  - support data heavy features

# The New System

  - removed cache layer
  - still have app tier
  - using Riak as data store

# Riak

  - no single point of failure
  - no node is a special snowflake
  - rolling upgrades
  - each new version of riak is compatible with older version
  - can roll out upgrades to a single node, then go out to others once it looks good
  - hot rebalancing
    - add/remove nodes, riak will move its data around so that the load is evently distributed
  - this has enabled them to add data heavy features
  - multi datacenter replication
    - sort of a master/master situation
    - if a cluster goes down, or a datacenter goes down, the data are available in another location

# How Riak Works

  - key/value store

  - normal get/put cases and its challenges:

    - get/put comes into node
    - request is forwarded to nodes that have the data
    - waits for some number of those nodes to respond (not all)... this is tunable eventual consistency, btw

  - node failure

    - if a node goes down and comes back online, that node will start catching up

  - conflict resolution
    - what happens if two reads from 2 nodes result in 2 different values?

  - balancing # of gets vs object size
    - if aggregates are separate, it results in multiple gets
    - if aggregates are kept in single object, it results in fewer gets but larger objects
    - it's a balancing act

# Data Patterns

  - Raw Data: this is the statement of truth in the system
    - key / value, where value is json data
    - **last write wins**
    - just store it... no need to read/modify/write

  - Match History / 1:N index
    - harder case, mutable data
    - read/modify/write
      - but what about concurrent updates?
      - 2 deltas come in at the same time, and 2 siblings are created for the match history
      - on the next read, they resolve the conflict by doing a simple set union
        - because the matchlist is growing over time... matches aren't removed, for example

    - keep non-primary indexes in the record
      - adds a little overhead
      - speeds queries

    - aggregate stats / sets of counters
      - much more complicated
      - not resolvable without additional info
      - why not use a list of deltas and do a set union, like the other case?
        - problem is, this is very expensive considering the number of metrics they capture
        - so, they keep a truncated aggregate as well, effectively merging together the old games
        - combine this with a recent games list, and they do the set union on that list

        - read + modify, truncate based on age, then write
        - this is **not** a perfect solution
          - especially during a partition, the truncated value could get de-sync'd
          - should only happen during a long partition
          - should be able to rebuild the match history from the raw data if that does occur
            - however, this is expensive so they try to avoid it
  - What if I want to know how many times teemo dies?
    -- 100s of updates per second per node
    - each node keeps its counter in memory; inside of an individual app we know the increment doesn't double apply or lose data
    - every so often, those values write to riak (write-behind)
    - not perfect, but they don't need super accurate data so if a few kills get lost, no worries


# Where they're at

  - Live but dark
  - can't deploy it fully yet b/c it's worldwide, and they need to roll out worldwide
  - doing gameplay analysis with the data

  - Thunderdome
    - hackathon at riot, every few months
    - self-formed teams
    - choose their own project
    - use their new stats system to identify interesting games, pull down the replay file for those games, and then broadcast those replays
      - what if I want to watch teemo die over and over again?

# Q & A

  - they export this data from Riak into analytics system for deeper analysis


  - how did they decide to use riak?
    - started with mysql
    - realized they weren't using a lot of the good features of mysql
    - evaluated hbase, cassandra, couch, etc
    - needed a system with highest availability compared with consistency
    - really liked conflict resolution control in riak, rather than being forced into last-write wins

  - they store data as binary on disk, using LevelDB to store the json compressed

  - how big is the cluster?
    - 8 physical nodes
    - 45 TB of data comprising 3 replicas

  - conflict resolution is abstracted, at the DAO layer
    - everywhere else in the app doesn't know that the DAO layer handles the conflict resolution

