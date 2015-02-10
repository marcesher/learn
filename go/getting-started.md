# Learning Go

- Started here: http://golang.org/doc/install

  - installed Go into /usr/local, as described
  - created $proj/go/go-play
  - created activate.sh to set some env vars, then ran `source activate.sh`. Seems to me though that unlike, say, python and virtualenv, Go prefers a single workspace and inside of that you have all the things, so probably I'll just add those things to my main $path inside bash_profile and be done with it

- Then, worked through this page in its entirety: http://golang.org/doc/code.html

  - noticed that testing has no assertions (http://golang.org/doc/faq#testing_framework) but does have an inbuilt benchmark package.
  - also has "Quick", which looks pretty cool for maybe fuzz testing and throwing a lot of random values at a function

- `go get` is pretty slick. had to `brew install mercurial` to get it to work, though, since the example in the doc uses a googlecode hg repo
  - note that this set the just-downloaded `hello` as the bin, and so I had to `go install` my own hello again to set that as current


## Questions after getting started



## Next up

  1. [x] Go tour: I'm going to do this locally with `go tool tour`.
  1. [x] Read FAQs: http://golang.org/doc/faq
  1. Read the language spec. No need to go super deep just yet... this is a first date. http://golang.org/ref/spec
  1. Effective Go: http://golang.org/doc/effective_go.html
  1. Work through the Go / Angular preso again: http://blog.campoy.cat/2013/12/writing-moder-web-app-with-go-tdd-rest.html
  1. Create a sample REST API for something dumb
  1. Read through some of the code recommended by Jeff Hodges: http://www.somethingsimilar.com/2013/12/27/code-to-read-when-learning-go/
  1. Found this, too: http://www.golang-book.com/

## Learning from the Tour

1. I *really* like go's implementation of multiple returns as well as naming those return values in the function signature:

```
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return
}
```

1. The var initialization syntax for multiple vars is kinda weird, though perhaps it discourages getting out of control (i.e. incents simplicity)

```
var x, y, z int = 1, 2, 3
var c, python, java = true, false, "no!"
```

1. I like the formatters, eg %T for type:

```
const f = "%T(%v)\n"
fmt.Printf(f, ToBe, ToBe)
fmt.Printf(f, MaxInt, MaxInt)
```

1. I love that Go requires {} for `for` loops and `if` statements

```
for i := 0; i < 10; i++ {
  fmt.Println(i)
}
```

1. Go's while loop is a simplified for loop. Makes sense:

```
sum := 1
for sum < 1000 {
    sum += sum
}
```

To infinitely loop, simply:

```
for {
}
```

1. assignments in if statements is pretty slick:

```
if v := math.Pow(x, n); v < lim {
        return v
    }
```

But be careful: those vars are only in scope for the duration of the `if` / `if/else` statement (You'd get `undefined: v` if you try to use it after the if)

1. I like the explicitness of pointers with structs. If you want a pointer, use &. Otherwise, it's a copy.
There's zero confusion about reference/value semantics. I also like that when you `fmt.Println` a referenced var, it prints the `&`



1. I like the idiom of using `()` for grouping:

```
import ()
var (
  x, y int
  b, c string
)
```

and so forth


1. Slices remind me of groovy

```
p := []int{2, 3, 5, 7, 11, 13}
fmt.Println(p[:4])
fmt.Println(p[2:5])
fmt.Println(p[1:])
```

**Note**: Creating a new slice variable, such as with `q := p[2:5]`, is a reference to the same underlying array. It is not a copy.


**Be Careful**: range semantics might seem weird: Subtract 1 from the right hand to get the true slice;
eg q[lo:lo] would actually be empty, q[lo:lo+1] would be a 1-element slice, and q[1:5] will get you elements from 1-4.

From the tour:

```
s[lo:hi]
evaluates to a slice of the elements from lo through hi-1, inclusive.
```

1. `make()`, len, and capacity: might not be what you might think it might be (how's that for hedging)

`q := make(int[], 3, 10)` will give you the 3-element slice, but you'll get `index out of range` if you try to set a value after element 3
I'm guessing there's an `Append` or some such thing, b/c otherwise I can't see the point of a slice with a different `len` and `cap`

Docs link to this:  http://blog.golang.org/go-slices-usage-and-internals, so go read that eventually


1. range in a for loop requires index and value variables

` for i, v := range some_slice {}`

if you do this, you need to use both the index and the value, not just the value, else you get 'i declared but not used'.
I wonder how you iterate a range and just access the value


1. Slice exercise

My simple solution is here: https://gist.github.com/marcesher/8170295


1. Use `make` to make maps

of the form: make(map[key-type]Value-type)

eg:

`m = make(map[string]Vertex)`

1. Map literals are still strongly typed:

```
var p = map[string]Vertex{
    "marc": Vertex{20,20},
    "heather": Vertex{15,15},
}
```

Holy hell that looks redundant. Why not just "marc": {20,20} since we've already declared the type of the Map?

Oh, look... you can!

```
var p = map[string]Vertex{
    "marc": {20,20},
    "heather": {15,15},
}
```

1. map delete and test

`delete(map, key)` to remove a map element. Test for existence with 2-value assignment: `elem, ok = m[key]`


1. Wordcount exercise... my solution is hideous

https://gist.github.com/marcesher/8171076

Surely there's a more elegant solution. Upside: this led me to learn how to use the blank identifier in range loops

1. Functions are values and can be declared and also used as closures

```
func main(){

  doit := func(x int, y float64) float64 { ... return blah }
...
}

func add(x, y int) func(int) int{
  return func(x int) int {...}
}
```

**Notice how the return type of add() specifies the closure signature**

1. Switch can use the same assignment semantics as `if`

switch os := runtime.GOOS; os {...

1. Switch does not require a `break`

Sensible! It simply stops on the first matched case

1. Switch without a condition can be used for cleaner long if/else statements:

http://127.0.0.1:3999/#46

I like this!


1. Go has no classes

- You can define methods on any custom type, however.
- can only define methods on types in current package; can't define methods on simple types

```
type MyThing float64

func (t MyThing) Abs() float64 {
...
}
a := MyThing(5)
a.Abs()
```

The first arg-looking thing in that `func` is the *method receiver*... it's the type that's receiving the function

1. Method receivers that are pointers are a way to achieve state

Given a method with a pointer method receiver:

```
func (v *Vector) Scale(f float64) float64 {
  v.X = ...
  v.Y = ...
}

v := &Vector{3, 4}
v.Scale(5)
fmt.Println(v, v.Abs())
```

the method receiver needs to be a pointer for `Scale()` to mutate the values on `v`. Otherwise, if the receiver is a value type instead of a pointer, Scale is effectively noop

1. "An interface type is defined by a set of methods"

Syntax:

```
type Abser interface {
    Abs() float64
}
```

Now, one thing in the Tour example that I need to beat into my brain is that if you define a method on a type, **the method receiver type determines whether a type satisfies an interface**

For example, given the above interface

```
func (v *Vector) Abs() {

}
```

**will not satisfy** the interface because the method is defined  with a pointer receiver type, not the value type (i.e. v *Vector, not v Vector)

1. A type doesn't declare its intent to implement an interface

Unlike Java, with an explicit `implements`, a type implements an interface if it implements the interface's methods. i.e. show, don't tell


1. I **think** interfaces are composable

```
type Reader interface {
    Read(b []byte) (n int, err error)
}

type Writer interface {
    Write(b []byte) (n int, err error)
}

type ReadWriter interface {
    Reader
    Writer
}
```

reads to me that a ReadWriter interface is an interface defined by having all the methods of Reader and Writer, in this case Read() and Write()


1. To provide error reporting capability to a type, simply implement Error():

```
type MyError struct {...}
func (err *MyError) Error() string {
  return "Whoops"
}

```

1. For http, when you add handlers, just pass `nil` to ListenAndServe

`http.ListenAndServe("localhost:4000", nil)`

simple http handler exercise here: https://gist.github.com/marcesher/8315820

1. rot13 Exercise

https://gist.github.com/marcesher/8316237

I did it the easy way first, which is simply comparing the byte to the upper and lowercase versions of the letters

Then I experimented with lower-casing the byte (http://golang.org/pkg/strings/#ToLower)

Doing this, I learned from https://groups.google.com/forum/#!topic/golang-nuts/84GCvDBhpbg that to convert variable v to type T, use `T(v)`


1. Concurrency: Go Routines

`go someFunc(x, y, z)`

Nice!

Seems semantically equivalent to Java's `new SomeRunnable(x, y, z).start()`, with the obvious difference that we can use functions as first class citizens and don't require a class


1. Channels

you can do

```
c := make(chan int)
go someFunc(x, y, z, c)

and then someFunc will do what it does and send a result to the channel:

func someFunc(x, y, z int, c chan int) {
    sum := 0
    ...
    c <- sum // send sum to c
}
```

To send to a channel: `ch <- v`

To receive from a channel and assign the result to a var: `v := <-ch`

I like the syntax here... same operator, and the operation is determined by `ch`'s position. Visually it makes sense to me

On Slide #66, if I change the buffer size to 1, I get the `all goroutines are asleep` error. Why is that? I need to understand these more clearly


1. Channels: Range and Close

To pull values off of a channel until it closes:

```
for i := range c {
...
```

and then the sender can close the channel with `close(c)`

Tour says that the sender should only ever close the channel, not the receiver, and that `close()` is typically not needed unless you need to terminate a range loop. I guess here's a case where the tight coupling between sender and receiver -- that the receiver expects the sender to close the channel -- is appropriate


1. Select

"lets a goroutine wait on multiple communication operations".

In the tour example, they use multiple channels passed to the function, and then an endless loop (`for {}`) with a `select` inside of it with cases

For the first case, it pulls off the first channel

For the second case, it pulls off the `quit` channel.

I think what this means is that if it can pull off the first channel, it will. And then once that case no longer applies, it drops down to the next case, which looks for the quit having a value.

When that condition is satisfied, the `return` statement kicks in and the function completes.

**Is this equivalent to scala's actors, with `receive` and case classes?** I don't think so. I think it looks like it, but channel semantics seem to be much different from actor semantics, and I'm getting head-faked by the loop/case idiom

1. Select can have a default

Makes sense. See Slide #69

Now, when I first looked at this slide, I was confused. But the semantics all looked like channels, so I figured that time.Tick() must return a channel. It does: http://golang.org/pkg/time/#Tick


Wrapping up:

```
select {
        case <-tick:
            fmt.Println("tick.")
        case <-boom:
            fmt.Println("BOOM!")
            return
        default:
            fmt.Println("    .")
            time.Sleep(50 * time.Millisecond)
        }
```

In the above, if something can be retrieved from the tick channel, that case trips. If something can be retrieved from the boom channel, that case trips and return ends the function. otherwise, if nothing can be pulled from those channels, the loop continues


1. Headless functions

Go's headless, built-in functions are documented in package `builtin`: http://golang.org/pkg/builtin/#cap



## Learning from the FAQ

- The theme here is simple, easy, correct, small. No ceremony. Example: http://golang.org/doc/faq#Does_Go_have_a_ternary_form
- Check out this sample test http://golang.org/src/pkg/fmt/fmt_test.go for an example of how they do it internally... data-driven tests
- There's a good trick in there for using the _ identifier for dealing with debug statements
- here's a long writeup on profiling go programs: http://blog.golang.org/2011/06/profiling-go-programs.html
- Goven (https://github.com/kr/goven) is a tool for copying dependencies locally if you don't want your build system, etc to be pulling from master on public repos
- http://golang.org/doc/faq#methods_on_values_or_pointers has a clear explanation on pointers vs values
    - **Pointer types behave in the same manner as Java**... it's value types that are different. Think: in Java, if you pass a map instance and update it, that update is visible outside the method context. In Go, that's what happens with pointer types. Go **always** passes a copy of the argument; so if the copy is a value type, any updates to it will not be visible outside the function context because you're updating a copy of a value, not a copy of a pointer and consequently you're interacting with different memory space
- Structs in go are crazy and awesome. They are pretty much like Maps in other language. But they're also used as the receiver of functions. The FAQ, one time, referred to structs parenthetically as "classes". So they're like this cut-the-bullshit approach to classes... we all know that classes are just data and methods (ignoring hierarchy for the moment), and so Go seems to implement that as simply as possible. I like it.


## Questions after taking the Go tour

1. In a range for loop, can you iterate without needing the index? (i.e. for x in range some_slice)


Answer: use `_`, which is the *blank identifier* (http://golang.org/doc/effective_go.html#for):

```
for _, v := range some_slice {}
```


1. What simple hacks are people using to auto-build go, such that you can effectively use it as a scripting language?

  - seems like `go run my_file.go` gets it done

1. Does go have something like list comprehensions? Kickass operators ala groovy? (http://groovy.codehaus.org/Operators)

  - haha. After reading the FAQ, the message on that is loud and clear. FU. Sugar is not this language's deal.

1. For channels, how do you deal with errors?

1. What are go architectural idioms for dealing with backpressure in distributed systems?

1. I need to learn more about buffered channels. I don't understand why Go tour #66 gives the `all routines are asleep` error message when changing the buffer size to 1

1. what is * in function signatures, such as TestSqrt(t *Testing)?

  - it indicates that the function expects a pointer argument of type Testing. Presumably the test framework passes this in

1. do other test frameworks exist? I wonder what niceties people are using on top of `testing`

  - Lots! http://code.google.com/p/go-wiki/wiki/Projects#Testing
  - note there are libs for xunit output and also coverage, as well.

1. I'm (sadly) enamored with Intellij and use it for all my current coding... I wish I could get the Intellij Go plugin working (https://github.com/mtoader/google-go-lang-idea-plugin). Alas, it ain't happening

  - Got it. They released an update and it now works for me. However, I had to go through some hoops and it's still not working as I'd expect it to with respect to startup, but that's ok.

  Here's what I did (on a Mac):

  1. create ~/.profile
  1. Give it these contents:

  ```
  export GOPATH=~/dev/projects/go/go-play
  export GOROOT=/usr/local/go
  launchctl setenv GOPATH $GOPATH
  ```

  1. start idea from the command line: `source ~/.profile && ~/Applications/IntelliJ\ IDEA\ 13.app/Contents/MacOS/idea`
  1. Added that as a bash alias because screw that noise: `alias idea='source ~/.profile && ~/Applications/IntelliJ\ IDEA\ 13.app/Contents/MacOS/idea'`

  According to https://github.com/go-lang-plugin-org/go-lang-idea-plugin/issues/456, it seems that after setting ~/.profile I shouldn't have to do this. However, launching Intellij from Spotlight gives me the "undefined GOROOT" stuff

  1. Running tests from Intellij still doesn't work. No biggie... just annoying.
    - oh, wait, got it, though it's weird and perhaps my own dumb fault.
    - I had to go into the test configuration and change the package from "main" to the other value in the dropdown, which was the full package path.

1. How are typical go projects structured? (Will learn more as working through the Effective Go book)

  - Still need to learn this

1. For web apps, are people using straight up Go, a framework, something else? What about HTML templating?

  - Looks like you can do fairly well with straight Go: http://golang.org/doc/articles/wiki/
  - But there are a fair number of frameworks and toolkits: http://code.google.com/p/go-wiki/wiki/Projects#Frameworks_and_Toolkits
    - Revel seems to be popular, and Martini was recommended to me as the current hotness. Gorilla was also recommended, as it's a toolkit and not a framework.


1. How are people "watching" files have having them auto built / installinstalled? This manual reinstall bullshit is.... bullshit.

  - It looks like some of the web frameworks, such as Revel, handle this.
  - What else if you're working on non-web apps?

1. Can this be considered a suitable replacement for a scripting language such as Python for every-day scripty things?

  - Looks like `go run my_file.go` will do just fine



## Error messages

1. go install: no install location for directory [go-workspace]/src/github.com/marcesher/http outside GOPATH

I got this when I had set my GOPATH to a subdirectory of my go workspace instead of at the root. Stupid mistake.


1. Missing a return type. eg:

 ```
 ./compile21.go:10: too many arguments to return
 ./compile21.go:14: add2(42, 13, 0) used as value
 ```

 example:

 ```
 func add(x, y int) {
     return x + y
 }
 ```

Same ` too many arguments to return` goes for mismatch between declared multi return types and what you actually return:

```
func swap2(x, y string) (string, string, string) {
    return y, x, "hi", "bob"
}
```

`not enough arguments to return` for cases like:

```
func swap2(x, y string) (string, string) {
    return y
}
```

1. Not explicit about pointer

```
type Vertex struct {
    X, Y int
}

var t Vertex = new(Vertex)
```

will issue:

`cannot use new(Vertex) (type *Vertex) as type Vertex in assignment`

Instead, use:

`var t *Vertex = new(Vertex)`

1. goroutine doesn't add result to channel

`fatal error: all goroutines are asleep - deadlock!`

For example:

```
func sum(a []int, c chan int) {
    sum := 0
    ...
    //c <- sum // send sum to c
}
```

Since nothing's put on the channel, attempts to take results off the channel will issue the error above

Note that it comes from a line like this (in the go tour): `x, y := <-c, <-c // receive from c`