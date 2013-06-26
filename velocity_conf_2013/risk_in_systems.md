http://www.youtube.com/watch?v=Pb_zYs8G6Co&feature=youtu.be

"what, where, and when is risk in system design"

Keynote

- Johan Bergstrom

 - comes from risk and safety science, not web operations

 - related blog post: http://programming.oreilly.com/2013/05/what-is-the-risk-that-amazon-will-go-down-again.html

# Views of risk

 - risk as a product of unreliable system components
 - risk is a product of non-linear interactions and relations


## Product of Unreliable system components

 - imagine the workings of a machine, like a sewing machine
 - if you want to understand why the machine is or isn't working, is you analytically go "down and in"
  - you look at the individual comopnents and how they act linearly, and how they follow their design rules

-- when it's working, we say it's reliable
  - something is working reliably when the system sticks to the rules
  - the design "is reliable"
  - if the machine isn't working, it follows then that there must be an individual component that isn't working

- So, which is the most unreliable component of web operations?

 - so, is the most unreliable component Humans?

- We can then calculate risk if we know the causes of unreliability, based on probability and severity of a failure

And if we can identify the unreliable components, we can then try to mitigate them

 - put in multiple defense layers "defenses in depth"
 - protect systems from humans :-)
 - but you get the swiss cheese problem ... eventually a breach can poke through all the holes of the barriers
 - replace unreliable humans with reliable technology
 - control unreliable humans with reliable rules
 - ask the unreliable humans to try harder
 - ulimately, **reduce variability**


## Product of non-linear interactions and relations

 risk as a product of system complexity

The metaphor of a machine doesn't work here; need to think about it more like a living system

Things aren't linearly connected
 - diverse actors
 - shift between loose and tight coupling
 - shift between independent and interdependent
 - the system is so dynamically adapting, it's hard to describe it and therefore no single actor can grasp the complexity of the entire system
 - different actors will give you different descriptions of the system

In a system such as this, **more barriers might be a problem** because barriers might create more interactions and therefore create more risk

### Risk as a path-dependent process

To understand risk, we need to understand the history of that risk
- think: Technical Debt
- software and systems grow for so long that it becomes impossible to know where risk lies

- in safety science, the notion of "drifting into failure"

### A control problem
  - see his slide on "boundaries", and how not crossing those boundaries inevitably leads to optimizing locally

  - the only way to find a boundary is to cross it
  - the only way to find a boundary of acceptable risk is to have an accident

  - boundary of financially acceptable behavior creates pressure towards efficiency
  - boundary of unacceptable workload creates pressure towards least effort
  - and taken together these boundaries create pressure **toward** unacceptable risk!

 - it's also true that safety measures -- measures designed to mitigate risk -- can become risks themselves
  - think twitter's t.co link shortener; in part designed to protect users, but itself is a risk b/c it can go down, causing unreliability and difficulty archiving the internet

### Managing Risk

 1. keep the discussion on risk alive even when things look safe
 1. invite minority opinion and doubt
 1. constantly debate the location of the boundaries
   1. multiple perspectives (actors) are critical here
 1. constantly monitor the gap between work as prescribed and work as performed
   1. there will always be a gap
 1. focus on understanding how people make tradeoffs guaranteeing safety
  1. don't look at people as an inherent risk, but as a **guarantee** of safety
  1. "safety management is not about avoiding, it is about achieving" - eric hollnagel


## Conclusion

 - see risk as a game between different values and different frames of reference
 - the two competing views described above represent those different frames of reference
 - the frame of reference contains and expresses our values

 **final appeal**

 - make your values explicit; let them guide your perceptions of risk
