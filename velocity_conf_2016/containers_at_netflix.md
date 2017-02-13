Mike McGarr / Andrew Spyker

their nebula build system emits a deb, which gets baked into an ami

Andrew -- runs container cloud

underserved users / apps: batch applications

what do batch users want:

- simple shared resources, run till done, job files
- NOT ec2 instance sizes, autoscaling, AMI OS's
- they just want to get their job done and move on
- they don't want to manage resources

What does he mean by batch?

- algorithm model training, with GPUs
  - for example, personalization requires models, and that model training runs in batch jobs
- media encoding
- digital watermarking
- all kinds of reporting

titus == netflix's container cloud


Lessons learned from batch
  - docker helped generalize use cases
  - advanced scheduling required... as work comes and goes, they scale up/down the underlying resource pool
  - initially ignored failures, with retries
     - really needed to get oprationally mature, reliable
  - time-sensitive batch came later... people needed it not tomorrow morning, but within the next hour
  
  Usage:
    - currently 100s of containers per hour, peaks of 1000s
    
   
  Why services in containers?
  
  - they initially thought it'd make life easier, make ti more scalable, etc. 
  in reality, this isn't that big a deal for them b/c they already have a rock solid VM system
  
  - the big benefit was the "underserved communities"... teamd who didn't want to use apache and tomcat
  - so for example, a nodejs app just didn't have an on-ramp into production
  - i.e. their whole stack was java-centric
  - another use case: I want an instance with a single core to run my lightweight server
    - problem: aws small are not reliable
    
  Enter Docker:
    - you have a language and build tool? use them
    - want to resource isolate easily? 
    
  Services more complex than batch
   - constantly resizing
   - need autoscaling
   - run forever
   - hard to upgrade underlying hosts when services are sitting on them running forever
   - services have more state... is this service ready for traffic
   - all the existing tooling they had are built around VMs
   
  The real problem though is networking:
  
   - multi-tenant networking is hard
   - they needed an IP per container in a VPC
   - security groups are at the IP level
   - IAM roles are at the instance level
   - isolating tenants... how do you keep them from stamping on each other
   
 Solutions:
 
  - vpc networking driver; ENI: elastic network interface -- full IP functionality
  - scheduled security groups
  - support traffic control (isolation)
  
  - EC2 metadata proxy
   - adds container "node" identity
   - Delivers IAM roles, because it's a bad thing if all containers on a host think they have identical IAM roles
   
 Big lesson learned:
 
 - almost all of the tools they use/built uses the "node" as the Identifier
 - but with containers, if you have 4 tenants on a node, it'd report in as being the same thing
 - so they had to add multi-tenant support into their tools
 
 
 Deployment
 
 - pipelines start based on an image showing up in the docker registry, not on a jenkins pipeline
 
- they've enabled chaos monkey in their container cloud, as well
- a lot of their tools -- deployment, telemetry -- try to retain the same UX as the existing stuff, so it's not wildly different when running a container vs a VM


Developer experience

- consistent mac setup: wanted to provide an easy way for all devs to use docker on their macs
- consistent workflows: b/c there are a number of different ways to do git... gitflow, pull requests, etc
- Netflix integration: make it easy to go from laptop to prod

- NEWT: network workflow toolkit
  - golang
  - command line toolkit to make it easier to run docker on macs
  - dev machine bootstrap: `newt setup --app-type=docker`
  - project scaffolding: `newt init --app-type node-beta --name velocity-ny-app`
  - then it asks questions... do you want a stash repo, do you want a spinnaker pipeline, do you want jenkins jobs?
  - run locally: `newt deploy` ... deals with the weird mac networking
  - get jenkins history right from cmd: `newt ci history`
  
  
  Dependencies at scale
  
  - when I publish a new version of my library and it has a breaking change, I don't know who I might have just broke
  - so they wanted to provide feedback to developers so they could see who was using their libraries, so they could see who am I about to break
  
  - so they solved this by using Titus, called Niagra
  - Mike thinks they couldn't have made as much progress as they had without Titus
  - b/c when a library author wants to put out a new version, they do that and run regression tests against all downstream users within netflix; all that happens in containers
  
  
  Future
  
  - looking to use docker for local integration test environments
  - next generation CI experience for engineers at netflix (presumably this means replacing jenkins?)
  - Internal Reserved Instance spot market of trough
    - b/c they already use reserved instances to run a kind of internal spot instance market