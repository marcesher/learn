# Source of Truth: Using Open Source Tools to Manage and Monitor Large Deployments in Multiple Datacenters

Dale Hamel (Shopify)

Note: this is a presentation about managing your baremetal datacenter

## Source of truth

truth in infrastructure: information that matches reality

in context: does version X of a software match what you think it does

False truth is a bad thing. worse than no information at all

example: if you think the IP address of a thing is X, and you reboot that, but in reality it was Y... you hosed Y
and didn't fix X

What is a source of truth?

 - place where state information can be accessed (puppetdb?)
 - any useful information about assets or service
   - what's in it? where is it? how to reach it? what's it doing? is it healthy? is it new? decomissioned?


- Truth Sink
  - anything that uses truth
  - apps take advantage of sources of truth for automation

- Can get complicated if a system is both a source and a sink for the same kind of information

Example: they have 3 different sources of truth for DNS: chef, collins, DynECT


**Why do we need a central source of truth?**

- Easier to create automation / tooling
- eliminate human error and boring tasks
- define clear, repeatable processes

- for maintenance and emergencies: what's connected to this thing that failed? eg


**Downsides to CM tools**

Puppet, Chef, etc are good at provisioning but have downsides with respect to source of truth

(see his slide)

**The goal**

- automate everything
- find all the things: one place to see the state of our infrastructure; reduce work and erroneous data, object oriented views of resources and how they interact


## Genesis Stack

- based on tumblr's stack using collins, phil, iPXE, and Invisible Touch

- Collins is the source of truth

- for tumblr, they had Phil + Visioner for iPXE render and provisioning, and Invisible Touch for job running

- Genesis uses Alchemy Transmuter for iPXE render and Provision, and Alchemy linux for job runner

### Collins

  - Play 2.0 app written in scala, by tumblr
  - render assets as html or json
  - restful json api
  - extensible api and plugins


### iPXE (pronounced eyepixie)

 - pxe is the protocol for a network booting a server, as opposed to usb or physical media


### Asset Tagging

 - servers themselves are the source of truth
 - they get the info from the SMBios
 - note: this is all for managing their baremetal datacenter