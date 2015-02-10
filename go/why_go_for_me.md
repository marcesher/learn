The story of why I got into Go bears telling, and it starts in 2004, 5 years or so before Go was even born.

During my first professional programming job, I somehow turned into the go-to person for building fast, reliable, scalable backend systems.
I am not sure why, but it happened. I ended up rewriting a number of systems that were written in ColdFusion and writing them in Java
because we needed speed, and one way to achieve it was through concurrency. So from about 2004 to 2009, I wrote a lot of
code using Java's concurrency mechanisms, starting out with plain old threading and moving on to the Executor framework introduced
in Java 5 and which seems continual improvements to this day.

So: I've been interested in concurrent programming for a long time.


Now then: I've been listening to the java posse podcast for a long time as well, and back in 2008/9 or so, a few of the posse
members were getting geeked about scala, big time.

They talked about concurrency in Scala, the Actor model, and so forth, and

So I investigated, bought a book, did some coding, etc.

I eventually dropped learning scala, but the language has exploded since then. From that, I thought: these guys have their finger on the pulse.

A few years pass, and Bruce Eckel from "Thinking in C" and "Thinking in Java" fame was on the show, and they were talking
about Google's new Go language. I liked what I heard, and I thought to myself: these guys were right about Scala. I need to keep an eye on Go.
They also talked a fair amount about Go and the fact that it was originally built to solve Google problems, and that meant scale.
And one of the ways they did that was by creating a really great, sane concurrency model. I was intrigued by this.

But I didn't do anything about it for a year or two.

Fast forward a bit more, and one night I found myself reading the Go FAQ.  This was March 14, 2013. Just a few days after immersion ended.
Stefan Fox is responsible.

I hit this: http://golang.org/doc/faq#Does_Go_have_a_ternary_form

Does Go have the ?: operator?

There is no ternary form in Go. You may use the following to achieve the same result:

if expr {
    n = trueVal
} else {
    n = falseVal
}

And this really caught me. It showed me a few things:

1. They are opinionated and snarky (is that good?)
2. They prefer readability at the expense of brevity
3. I bet if I keep reading, I'll see more of the same.

Sure enough, when I got to the section on testing

http://golang.org/doc/faq#testing_framework

I read that the language doesn't even have assert in its testing framework.

No asserts! what kind of crazy language is this.


So in December 2013, while on a long Christmas break, I finally started to learn Go, and here's what I knew at the time:

1. It's a typed language, but it's not annoying to read Go code like it is Java due to type inference
1. It has a concurrency mechanism called Channels based on C.A.R. Hoare's Communicating Sequential Processes paper from the 70s
1. it's a C style language, so its syntax should be pretty familiar to me, unlike, say, Clojure which is a lisp
1. It compiles to a single binary which contains its own runtime, which I assume means it's going to have a really simple deployment model.



And here's what I sought to find out:

1. Could Go actually be used as a replacement for python as a daily scripting language?
1. Could I use Go to build web applications, and would that be joyful?

I had a few other questions that I intended to answer while getting at the first 2:

1. What's it like to actually distribute or deploy a go application?
1. What's the community like?
1. What's the learning experience like... documentation, examples, etc?
1. All programming is tradeoffs... what tradeoffs will I make frequently when using Go?


## Getting Started

 - show https://github.com/marcesher/learn/blob/master/go/getting-started.md

 - show installation instructions

 - show tour: http://tour.golang.org

 - show my local setup

 - Show hello.go
   - run it
   - build it
   - run hello binary


 - Show gemmer in action

 - Show lyricfetcher.go

   - Type
   - XML unmarshalling

 - Show Sumday

 - Show goconvey with sumday

 - time permitting, show local web dev with greenramp