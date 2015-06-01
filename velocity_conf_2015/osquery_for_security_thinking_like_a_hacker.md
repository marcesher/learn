# Mike Arpaia

github.com/facebook/osquery

"information security is an engineering problem"

"secrecy is not the way forward"

he believes the future of information security will be "written in vim"

## osquery

- open platform for host instrumentation
- sql for your infrastructure
- use sql to explore OS state

osqueryi: interactive shell
query your OS just like you would mysql

--OK... this is friggin cool

osqueryd: daemon for low level host monitoring; where the magic is

- know how the results of a query change over time

- holy crap: this is what we've been looking for with our "sentia" project... this could solve the problem we have about getting more information about how nodes themselves change over time so that we don't have to write that stuff ourselves, as we have been a little bit

- host event pub/sub stream
- subscribe to OS events / APIs
- gets around the inherent problem of scheduled introspection
- so osqueryd is a mix of scheduled introspection and event listening

- file integrity monitoring
- use wildcards to monitor important files on your hosts
  - /bin/*
  - /Users/*/Downloads/**

- plugin system
- for config distribution and data infrastructure
- specify your plugins at runtime with a command-line flag
- "In production, our logs never hit disks" ("we use scribe, actually")


## working together to stay safe

- many different industries working together: offensive security researchers, defensive security professionals, entrepreneurs in infrastructure/security