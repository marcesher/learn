# Kubernetes in Azure

I'm attending this mostly out of curiosity; I'm curious what the MS folks have to say about kubernetes and if they talk about its value in general, regardless of where it's hosted. I'm much less interested in the azure parts of this but, hey, open mind. Perhaps the stuff they talk about with the process of modernizing will be useful regardless of whether it's to azure or whatever

Go get his slides for details on these app modernization approaches

## App Modernization approaches

- rehost (lift-n-shift)
  - essentially duplicate your existing environment, but in the cloud
- replatform (lift-n-reshape) 
  - this one kind of fits in the middle here and is what theyr'e talking about today
  - basically, containerize and deploy to the cloud with an orchestration service such as kubernetes, which basically helps you get the most out of your server resources since the orchestration engine (like k8s) attempts to maximize for resource usage. You get a type of constrained elasticity that isn't as granular as "spin up a new server when we need more capacity". an orchestration engine lets you say "we need more cpu/ram" and the engine gets it from the cluster
  - you get more control over the resource knobs other than just spinning up a new instance
  - the orchestrator also does self-healing of the cluster, behaviors around what to do with your app when it goes down, etc
  - think about the problem of having a lot of apps, and thus a lot of containers to deploy/manage: how would you manage all of that? well... that's what orchestration engines are for
  - he says kubernetes has basically won the orchestration game
- refactor (PAAS approach)
  - I think he was talking about swapping out some services and start using more cloud services, but not rewriting the whole app
  - for example, in our case, lift-n-shift the app but use an RDS database and hosted elasticsearch
- reimagine (cloud-native)
  - complete rewrite; potentially replacing a bunch of stuff with serverless, blah blah blah
  - note he isn't talking about moving it from a custom built app into a third party services; his assumption for the purposes of this talk is custom software that's staying custom
  
  
## What is kubernetes?

- came from google
- donated to cncf in 2014
- most popular github project (really?)

- He has a good set of slides on WHY kubernetes

Now he's giving a demo and talking about containerizing windows apps. snooze. I mean, it's cool and all, but I don't care right now. My takeaway: it's a thing. Good, got it.


## Demo 

OK, now he's going to demo kubernetes

"if you're new to kubernetes, don't worry about the syntax. syntax is not important, concepts are" -- I love this.

demo of running an image from the google container registry and running it as a pod in kubernetes
- his demo is running on azure but he's told it to create a tunnel between it running on azure and his machine, and expose it as a port on localhost. OK, that's cool (I think this is kubectl port-forward)

He shows the yaml file that describes all this. Pretty simple looking. Looks a lot like doing this in DC/OS or even docker-compose

OK, so IMO this ended up being a fairly useful session, disregarding the windows stuff for now which took too damn much time

But it was a cool job of showing practical uses for packaging up legacy stuff and moving into an orchestration engine such as k8s, and actually validates the work we've been doing in d&d for our part of our cloud migration
