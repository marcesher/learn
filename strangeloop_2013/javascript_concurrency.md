Concurrent JavaScript

# Event-driven async programming

## JS Execution Model

 - single event queue
 - events run to completion, no interleaving
   - you can rely on the fact that an event handler will complete before the next event handler starts
 - events can create new events
   - enables you to decompose big task into smaller tasks
 - ordering of events may be non-deterministic
   - this is a big drawback of this model
   - you never know when an event will run
   - much depends on external things.. user clicking, the network, etc
   - you have to live with this uncertainty

 - See his slides for a problem with the single thread execution queue, with the stackoverflow example
   - img.src = url, then attaching onload event handler, will not work! Because img.src will start loading the image immediately and will go to completion; consequently, the handler never gets called.
   - thus, the handlers must always be attached before the actual events occur (duh)
 - See his slides for a more complex scenario: a personalized website
   - look up a person's profile, and async load avatar, social status, recent activity, etc
   - thus you end up in callback hell
   - or, you define all the callbacks up front but consequently destroy the linearity of the code
   - a more fundamental problem with this is error handling
     - you really only want a single error handler, but b/c of the callback mess, you have to add error handlers to all the edges
     - how to solve? Promises (he says)

# Promises

 - enable direct encoding of async flow in data
 - promise objects encode state of async operation
 - errors propogate along the flow until caught (think of it like exceptions)
 - see his slides for code example
   - essentially, promise.then().then(); when.all(promises... ).then(create, handler)
   - when anything fails in this chain, it bubbles up to the handler
 - see github.com/promises-aplus
 - github.com/cujojs/when

# Long-running Scripts

 - only one event executes at a time, so:
 - no event is ever interrupted... they all run to completion
 - thus you get the "this script has been running for a long time..." alert
 - how to solve? Web Workers


# Web Workers

 - spawn a second instance of the JS engine
 - no shared state, so you have to communicate via messages -- actor model
 - own event (message) queue

# Modern parallel hardware

 - For the best experience on modern device, need to write code that works with all 3 of the below

# SIMD Units

 - Compute on small vectors, 4 or 8 elements
 - same operation on multiple elements
 - Single Instruction Multiple Data
 - conditional control flow has to be encoded by merging values (thus it's a restricted programming model)

```
 add [1,2,3,4] [2,3,4,5] = [3,5,7,9]
 shuffle [3,2,1,0] [1,2,3,4] = [4,3,2,1]
```

## Adding SIMD to JS

 - Proposal by John McCutchan
 - first, you need vectors
   - special vector-value types: float32x4 and int32x4
 - need something to store them in
   - Float32x4Array
 - need a SIMD object (similar to Math object) to provide a set of intrinsic operations
 - See his slides for code example of how this style programming in JS would compare to typical programming in JS via Math
   - also see slides for how to deal with conditionals, since you have to do the conditionals in data
   - He says SIMD programming isn't easy, there's some wizardry in figuring out whether something is faster, but typically it results in great speed advantages

 - see the SIMD prooposal doc at ECMA
 - implementation effort from Intel and Mozilla (search mozilla bug tracker)

## Parallel JS (formerly River Trail)
  - high-level data-parallel programming API
  - operates on n-dimensional arrays
  - proposal by Intel and Mozilla
  - extends JS array objects and upcoming typed objects
   - buildPar (factory)
   - mapPar
   - reducePar
   - scanPar
   - scatterPar
   - filterPar

```
var a = [1,2,3,4,5,6]
a.mapPar(function(v) {return v+1;});
```

Looks just like plain old javascript map

How do we enable this parallel execution?

- Temporal immutability: the global heap is immutable **during** parallel execution

- See his slides for Typed Object example (formerly Binary Data)

` var Pixel = new ArrayType(uint8, 4)`, eg
- very cool example of using this for computing grayscale on images using this approach

- **More on parallel javascript**
 - nightly.mozilla.org for implementation in firefox
 - see ecma proposal for typed object propsal

