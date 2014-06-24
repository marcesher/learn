Carl Quinn, Riot Games

Building a cloud platform using netflix oss

# First cloud approach
  - lots of teams already using AWS; not a lot of sharing; separate teams with separate AWS accounts; no standards for build/deploy/etc

  - phase 1 was standardizing, getting build/deploy tools in place, etc

  - Bakery: Aminator + chef. Jenkins builds result in a base image
   - these base AMIs are then used throughout the pipeline.
   - an app can then be stuck on these base AMIs
   - there is definitely overhead here, so you need to be able to do it fast, manage cleanup, etc. Getting the tooling in place is the hard part
   - big benefit is no moving parts during deployment time
  - Asgard: basically an alternate AWS console
    - workflow for autoscaling groups, rolling pushes, red/black pushes, etc
  - Edda, simian army, and ice for other stuff

# Build pipeline: Bakery

 - added a chef-solo plugin to Aminator
   - see aminator-plugins on github
 - added Nexus auth
 - artifacts (rpms, etc) delivered to nexus / artifactory
 - Want to bake
   - base and App AMIs
   - Ubuntu, centos, and aws linux
 
 - other options now include packer, which can now do AMIs
  - so: consider packer as an alternative to aminator


 - When a bake happens, an Input AMI is selected, aminator mounts the volume, and that volume is basically chroot
   - at the end, aminator snapshots the volume and registers it, out comes the output AMI
 - all of this runs on a jenkins slave in ec2
 - all of this takes about 2-5 minutes


# Asgard

 - leverages user-data
   - new plugin to use templates from github
   - "repoSourcedUserDataProvider"
   - this thing emits user-data that's used in the build config
 - they do authentication using OneLogin support
 

# Management

## Simian Army
  - Janitor and Conformity monkeys keep things tidy
   - janitor monkey helps you learn what's junk and nobody's using
   - can even delete stuff for you that's not used
   - conformity monkey helps find amis that are special snowflakes that don't adhere to standards
   - chaos monkey helps knock things over; services should be stateless and resilient to failure

## Edda
  - tracks what changes in your aws account
  - one example they did was to create a client side scripting scans for security risk errors such as too-open security groups
  
## Ice

  - visibility into usage by account & resource
  - support for tag-based rollups

All of this led to good success at riot
  - worked well for smaller self-contained apps, etc

BUT

public clouds don't yet meet all of their needs
  - latency especially, and you need regional locality for that

- they still need and like datacenters

AND

- Some projects were not ready for the cloud
- if apps aren't architected for SOA, moving to the cloud can be tough
- maybe going to aws is not the best firs step
- SO: first step is cloudifying the app
  - this is just following good SOA principles: small, service-independent, stateless, REST interfaces


# Phase 2: The stack

  netflix OSS platform libraries and services

 - join forces with ongoing initiative to refactor the platform into SOA
 - since they didn't previously coordinate much, that was the first step... bringing people together

 - they created a kind of RFC (request for comment) system and agreed on some standards
  - REST, JSON, Swagger
 - they created a library called "Hermes"
   - jersey, jackson
   - dynamic swagger generation


 How's netflix tools fit in?

  - use Eureka for service discovery
   - this uses DNS to find a name for the discovery service, and then the discovery service can give them all the addresses for the other services that are registered
   - in the old model, these addresses would be done in chef, hoping they don't change much
   - discovery service is queried every 30 seconds for changes

  - use Archaius for configuration change detection
   - this incorporates properties from many different sources
   - this is a way to change values for feature flags, etc

  - So, from the top:
   - you have App AMIs, but they don't have much personality
   - Asgard injects some config at deployment time
   - and then when the App is up, it talks to Eureka and ARchaius to get available services and final configuration
   - Things that are fixed happen at bake time, things that aren't happen at runtime
   - machine image is immutable

## Eureka

  - typically deployed as a cluster
  - machines that publish or consume service talk to Eureka
  - push health state to eureka periodically, for example
  - netflix set it up so that the eureka cluster is triple redundant: 3 zones in 3 regions
  - services try to talk to the closest eureka, locality-wise
  - Riot's varation on Eureka is "Discoverous"
  - one lesson they learend at netflix: network partitioning, when the networking between zones would completely fail, would make it look like half the network had disappeared, and so eureka would drop it from memory. then, when the partition resolved, there was a stampede to add all the services back, which took down eureka.  So now, when a lot of machines drop off, eureka treats it like a network partition and preserves those machines rahter than treating them as dead

## Archaius: dynamic config library

 - aggregates multiple property sources, composites them, responds to updates
 - sources can be remote
 - you can also query an app over a port and ask it for a description of its configuration and the source of that config

 - "Configurous" is Riot's version of Archaius
 - works in their datacenters as well as aws
 - they have a JS UI built on top of swagger, uses metadata to describe the endpoints
 - they're planning on open sourcing Configurous

## The current stack

  - evolving all the time
  - "Hermes and rCloud App Kit"
    - dropwizard, eureka-client, hystrix, ribbon, archaius, blitzrj, servo, governator, Riot hermes libraries

  - dropwizard is great for new stuff, but not for retrofitting old stuff
  - so hermes extensions help glue hermes and dropwizard

# Phase 3: All Together Now... Deployment + Stack

 - basically a combination of the above 2
 - bakery, creates base and app amis
 - asguard pushes these instances out
 - services and configuration are discovered


## Achievements

  - deployable artifact for aws
  - deployment tool for aws
  - soa platform infrastructure for apps
  - soa platform libraries for Java

## Challenges
  - deployable artifact is only for aws, not universal
  - artifact is huge (10GB)
  - deployment tool (asgard) is only for aws, not universal

# What's next

 - universal system

 Grand unified future?

 - Docker
  - build application containers instead of whole machines
 
 - For deployment, they're not sure what they're going to use yet
  - fleet? flynn? mesos?
  - challenge now is figuring out which of these are going to be the most successful... lots happening in the docker space right now
 
 - Eureka and Archaius are ready to go

 - The result here is  in fact a much simplified build/deploy model

See his slides for links to other presentations and code



!!! yesterday, when I asked the docker presenter what the tradeoffs were, he couldn't answer. Carl was sititng in front of me, turned around, and whispered "none!".

   - Now I know why he said that
