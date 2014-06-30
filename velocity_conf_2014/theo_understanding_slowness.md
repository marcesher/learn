# Undestanding slowness

Theo Schlossnagle

"slow is the new down"

"when shit goes wrong, the gloves come off"

@postwait

CEO Circonus

His experience: the time to remediate failures was directly linked to the skill of the engineering team


## high level map

- architectural components, connectedness, data flow

The maps are important b/c they make it easy to see when something's wrong with the map

## Low level map

- component versions, component languages, etc
- important that you don't have to log into a system to actually understand something, eg what version and patch level of teh JVM are you running on server X
- expected latency between data centers, etc
- connected service details
- you need to understand what you're running at every single level
- this detailed map is not for zooming out, but for zooming in. the high level map is for zooming out



## Responsibility

 - you need to be clear about who is responsible for each component in its context
 - know who gets the ball next if that person is not available
 - game day scenarios really help here

## Expectations

 - set expectations for breakages and slowdowns
 - what you build will break, understanding under what stress is your job as an engineer

 - think about bridges: designers know exactly how bridges will fail
 - you need to know how much stress your system can take

## 0 tech loyalty

 - do not have loyalty to the technologies that you run
 - don't lock yourself in to a tech... tech shifts too rapidly
 - have a list of replacement vendors of part alternatives
 - build a system from replaceable parts

## When things are broken or slow: Logistics matter

 - observability, tool parity, safety harnesses
 - need different plans for different failure scenarios
 - and the failures you encounter will probably be different from what you expect
 - eg, 1919 mollasses incident in boston harbor
   - they didn't plan for a mollasses flood, but they prepared for lots of other things, so they could look at how they dealt
   with other scenarios that had similar characteristics
 - Understand the scope of a change... what are the risks of this change?

### Observability

  - tells the grace hopper story of giving people nanoseconds
  - the one beast you can't slay: latency
  - you must subdue it, but first you must understand it
  - how you visualize latency matters a lot

  - "Averages are for chumps"
  - Histograms over aggregations
  - to really understand latencies, you need to look at all of them, not averages
  - as soon as you go to averages, you get loss, and it means you don't know anything about your latency

  - look at quantiles
  - histograms are a lot of info to digest
  - so looking at 10, 25, 50, 90, etc quantiles can give a lot of insight
  - a lot of times, the quantiles are encoded in the software you're using. think: JMeter
  - you need to know what quantiles are right for you, but:
  - the 0 and 100 quantiles (min, max) are really useful
  - these can often show you errors in measurement... where your data is wrong

### Tools

1. An observational tool
  - for taking measurements
  - it inspects state, but it does not change it
  - you don't want heisenbergs

1. Synthesis tools
  - for testing hypothesis

  - dtrace, truss/ktrace/strace
  - tcpdump/snoop
  - mdb/gdb/dbx/lldb
  - sar/mpstat/iostat/vmstat

  - curl

  - vi/echo
  - sysctl/mdb -w
  - DTrace -w

  He likes mdb and dtrace so much b/c they're observational only. the "-w" flag lets them write into memory, which also
  lets them change state

  "The most important thing here is that man is not listed". You don't want to be reading the man pages fo these tools
  while you're figuring out the problem. As an engineer, you need to know those tools well enough to leverage them
  as if they're second nature


  "Scrub in or go home"

  - they use ZFS, and they scrub it all the time
  - they realized they had tons of bit errors, which zfs scrub corrects
  - but that zfs scrub, when it ran, caused all their charts to go crazy b/c it was doing a lot of work
  - now, they do it all the time after they saw the problems the bit errors were causing


  When looking at big errors, look not just at the few minutes leading up to it, but rewind hours, even weeks.