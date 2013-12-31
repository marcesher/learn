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

  - what is * in function signatures, such as TestSqrt(t *Testing)?
  - do other test frameworks exist? I wonder what niceties people are using on top of `testing`
  - I'm (sadly) enamored with Intellij and use it for all my current coding... I wish I could get the Intellij Go plugin working (https://github.com/mtoader/google-go-lang-idea-plugin). Alas, it ain't happening
  - How are typical go projects structured? (Will learn more as working through the Effective Go book)
  - For web apps, are people using straight up Go, a framework, something else? What about HTML templating? 
  - How are people "watching" files have having them auto built / installed? This manual reinstall bullshit is.... bullshit.
  - Can this be considered a suitable replacement for a scripting language such as Python for every-day scripty things?

## Next up

  1. Go tour: I'm going to do this locally with `go tool tour`. 
  1. Browse through some FAQs really fast to get a whirlwind: http://golang.org/doc/faq
  1. Read the language spec. No need to go super deep just yet... this is a first date. http://golang.org/ref/spec
  1. Effective Go: http://golang.org/doc/effective_go.html
  1. Work through the Go / Angular preso again: http://blog.campoy.cat/2013/12/writing-moder-web-app-with-go-tdd-rest.html
  1. Create a sample REST API for something dumb
  1. Read through some of the code recommended by Jeff Hodges: http://www.somethingsimilar.com/2013/12/27/code-to-read-when-learning-go/

## Some impressions

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

**Note**: Creating a new clice variable, such as with `q := p[2:5]`, is a reference to the same underlying array. It is not a copy.


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



## Questions after taking the Go tour

1. In a range for loop, can you iterate without needing the index? (i.e. for x in range some_slice)


Answer: use `_`, which is the *blank identifier* (http://golang.org/doc/effective_go.html#for):

```
for _, v := range some_slice {}
```


1. What simple hacks are people using to auto-build go, such that you can effectively use it as a scripting language?





## Error messages

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