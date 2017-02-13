Oliver Gould
formerly at twitter

Microservices: constraining scope to make things easier to think about and operate

"Microservices are hard. Do not do them if you do not have to"

If he could run twitter on a gigantic mainframe, blah blah, he would

microservices are necessary for organizations that are growing, and running on commodity datacenter hardware that is bound to fail

you will not be able to use the tools you're used to to operate microservices... no more ssh into server, run some commands, etc

with microservices: where you used to have library calls, now you have network calls

Layer 5 dispatches requests onto layer 4 connections

finagle: rpc library for the jvm
  - built on netty
  

microservices: your server is a function

Because all (?) services user finagle, that consistency makes operating these services a lot easier
   - get a whole bunch of common things in each services
   - know how to monitor it, ask it questions about itself, etc
   
Per-request routing... use cookies, or whatever, to route requests to different versions of a service
  - eg, to a v3 version, a debug version, a version that will inject failure, etc
  

The complexity of all this leads to tools like **zipkin**... tracing / debugging tool
  - for watching requests flow through the system end to end; observe the call graph
  
- finagle also has different built-in load balancing algorithms, because connection-oriented algorighms (round robbin, etc) didn't scale for them

He talks about deadlines vs timeouts/retries; built into finagle
  - this lets them make tradeoffs; accept higher latency on "who to follow", lower latency on timeline, etc
  
retries: can actually do much damage because the more retries you allow, the more load you throw at a system

finagle has "budgets" instead



linkerd:

- built on finagle and netty
- has all the stuff he's been talking about with finagle

github.com/buoyantio/linkerd-examples


He gives a neat demo of linkerd in action

@olix0r

linkerd.io