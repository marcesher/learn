# Achieving rapid response times in large online services

Jeff Dean, Google


YOu need to care about the 99%ile latency on all servers when a single request might talk to many many servers

How to reduce latency

- differentiated service classes
  - prioritized request queues in servers
  - prioritized network traffic

- break large request into sequence of small requests
  - gives a large file read as an example, where a large file read blocks downstream small file read requests

- manage expensive background activities
  - eg log compaction in distributed storage systems
  - Rate limit activity!
  - defer expensive activity until load is lower


## Tolerating faults vs tolerating variability

- tolerating faults
  - make a reliable whole out of unreliable parts
  - extra resources... disks, memory, dist. system components, etc

- tolerating variability
  - use these same extra resources
  - make a predictable whole out of unpredictable parts

- Variability is much harder, because you can have 1000s of disruptions / sec, scale of milliseconds
- whereas with hardware faults, you might only have 10s per day


## latency tolerating techniques

- Cross request adaptation

    - fine grained load balancing
      - move bits of work to different machines, alleviating load on another

    - When a machine becomes slow, remove it to improve latency (nonintuitive)
      - send shadow stream of requests to that server, and measure latency. return it to service when latency is acceptable


- Within request adaptation

  - goal: reduce overall latency, don't increase resource usage too much, keep systems safe
  - example is a large fanout system... single query comes in, sends to many leaves

  - Canary requests: they take a bit of latency hit to keep the seving systems safe
    - send the query to one leaf. If it succeeds, they send it to the rest
    - if that query never returns, they might send it to one more leaf, but not to the rest
    - record the request so they can figure out why the query is killing the backends

Crazy... he's talking about solving problems I've never experienced in my lame-ass career :-(
   - of course, the title of his talk was "achieving rapid response times isn large online services"

## Big Takeaway

  - pay a lot of attention to latency variability in the 99 and 99.9%ile


# Performance In Context – Is “Good” Good Enough?

Ben Rushlo (Keynote Systems Inc.)

"Rachael ray finds inspiration in cooking her family and her dog"

... Context matters... one missing comma changes everything

For performance, we need to ask: Is performance good enough given its context?

Define: what is good performance?

Let's face it: most of us work on systems that are designed to make money, so:

Performance is good enough when you've optimized the business outcome


What is the future of performance management?

- real user behavior and performance
  - seeing this come into a lot of RUM products

- Video capture / Pixel compare
  - think: webpagetest

- custom events / markers


Do the business owners believe that performance is a key business metric, and can the technology organization deliver on that metric

For great performance, you need the business owners to care about it

- Keynote can compare a site to its competitors, so that business owners can see where they compare

Performance people need to come out of the bat cave and learn to speak business

find and educate a business champion

leverage context: put performance in the context of the business outcome


# Exponential Load Testing: Multiply the Power, Multiply the Results

Saurabh Bajaj (Neustar)

Multicloud: use multiple clouds is like investing in stocks: you're diversifying

He sees a move from the Information Technology era to the Business Technology era


For load testing, internal testing worked for a while, but it wasn't good enough

Cloud based testing was a good step

  - spin up thousands of nodes to generate massive load
  - "operationally very easy for us". lol


Single cloud based solution wasn't enough

So they started using multiple clouds for load testing

Hypothesis was: you'd get increased reliability and reduced variability of answers if you used multiple clouds to generate load


A single lens means distortion and unreliability

Multicloud is like more lenses to achieve clarity

If you're spinning up thousands of nodes, work with the service provider to explain why
  - they got a lot of value talking with the cloud provider and even engineers on the cloud provider's team


# Lowering the Barrier to Programming

Pamela Fox (Khan Academy)

http://code.org/promote

There is going to be a huge gap between Computing jobs and software developers... many more jobs, no one to fill them

## Barrier #1: Access to a computer

 http://www.donorschoose.org, search for "computer science"

## Barrier #2: Local dev setup

 - many students struggle with setting up a local environment
 - it shouldn't be a badge of honor
 - many students don't have their own computers... they might not have install rights, etc

 !! We need more online programming environments

 - decent solutions exist for javascript, python, etc

 - But they need more.... online emulators for arduinos, robotics, etc. Other languages like objective-c, swift etc for iphone apps


## Barrier #3: CS Classes

 - in 28 of 50 states, CS does not count towards math/science graduation requirements
 - 9 out of 10 high schools don't offer CS classes

 code.org/promote

 code.org/learn/local

 - find local coding clubs, or start one

## Barrier #4: social encouragement

 - parental encouragement, familial encouragement, peer encouragement

 - don't pressure... encourage

## Barrier #5: Career misconceptions

 - people don't know what CS even means

 madewithcode.com/mentors

## Challenge

 - lower the barrier for one kid to learn to code



# How to innovate for 2018

Cheryl Ainoa, Intuit

Technologists have a critical role in helping our companies remain relevant

Keeping pace with technology disruptions

Think back to 1984: it was not obvious that the PC would drive the world forward like it has

Gives a lot of examples of 4 year cycles, eg 1994 netscape didn't exist, but by 1998 it was obvious that the internet would change everything

Gives examples of companies innovating and then missing the boat.... Franklin planner, palm pilot, blackberry


1. have deep customer empathy
2. Keep one eye on the future

## customer empathy

 - it's every engineer's responsibility to have customer empathy... it's not just the job of the product manager
 - the technologists need to understand the customer's problems
 - observe your customers in their environment and how they use their product... don't rely on what they tell you
