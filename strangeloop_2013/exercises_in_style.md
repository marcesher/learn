Exercises in Style

- Christa Lopes

- Professor and developer


How do you write what you want to express?

You look at a piece of code and know immediately who wrote it... how is that?

Look at art: modernism, impressionism, abstract expressionism

- You might not know the particulars, but once you have a basic understanding of a style, you could categorize a painting as this style vs that style
  - it's about rules and constraints
  - How do they teach that in art school?
    - they teach the constraints, then you the artist go apply those constraints in your own artwork, eg


She starts thinking about programming style, goes to wikipedia
  - wikipedia "programming style" page...
  - "set of rules or guidelines", but it all goes downhill from there, eg:
    - following a particular programming style will help others read the code
    - equates style with appearance (aesthetics)

# Programming Styles

  - ways of expressing tasks
  - Exist at all scales
  - Recur in multiple scales
    - from writing code to designing systems
    - many times, the style at the microscale also applies at the macro, because the same concepts recur at different scales
  - codified in programming languages
    -

## Why are styles important?

 - Provide common vocabularies
 - basic frame of reference
 - some styles are better than others
   - depends on many things
   - no "best"... styles don't necessarily apply to all projects.... each is its own special snowflake

## How do you teach style?

 - She came across the French writer Raymond Queneau, "Exercises in Style"

# Exercises in Style

 - Term Frequency
   - given a text file,
   - output a list of the 25 most frequently occurring words, ordered by decreasing frequency

 - She shows multiple implementations of this problem
 - she tried to name them but it was too hard, so she calls them 'style #1'
 - asks to tweet her at @cristalopes to give names to these styles

## Style 1
   - very triangular
   - one big blob of code
   - no abstractions
   - heavy control flow
   - she calls this "brain dump"

## Style 2
   - 5 lines of code
   - people wondering "what is going on here?"
     - 'yeah, that is one of the characteristics of this style'
   - each line is full of stuff... doing a lot, trying really hard
   - takes about 4 minutes to run this code, however
     - the unique_words.sort() line is super slow
   - if you add 2 more lines of code, you make it efficient again
   - also, this is not completely correct... there's a little bug in it
     - it opens a file but doesn't close, and depending on the python runtime in use it might eventually run out of file descriptors if run a lot

   **characteristics**

   - no named abstractions
   - very few long lines of code
   - advanced libraries / constructs
   - "code golf" style... trying to code something in as few lines as possible
   - "try hard" style (ala die hard)

## Style 3

   - page and a half of code
   - divides the problem into separate procedures representing a procedural abstraction
   - main method just calls those functions

   **characteristics**

   - procedural abstractions, may take input, may produce output
   - shared state
   - commands
   - break it down into separate procedures, then call one procedure at a time
   - name: "cookbook style"

## Style 4

 - break down into functions (not procedures)
   - they all receive input and return output
 - in main, the output of one function is the input to the next, basically chaining together

 **characteristics**

 - divide into function abstractions
 - no shared state
 - mathematical function composition
 - name: "chocolate factory style"... pipeline of inputs and outputs


## Style 5

 - page and a half again
 - functions take input, but they return the result of another function call
 - the constraint is that there's always one extra parameter, the "func", which is called at the end
 - ` def normalize(data, func): ... return func(...., ....)`
 - name: "crochet style"... a loop that goes and gets the next thing

## Style 6

 - 2 pages
 - abstracted as Classes
 - tries to emulate the world
 - Classes such as StopWordManager, DataStorageManager, WordFreqController
 - never interacts with the data directly, only via the operations that the classes expose
 - Ostensibly should provide reuse

 **characteristics**

 - things things and more things! (ha)
 - capsules of dta and procedures
 - capsules say "I do the same things as that one, and more"
 - name: "Kingdom of nouns" style

She's running out of time, so she skips ahead to Style 8

## Style 8

 - 2 pages
 - functions within functions
 - tries to do it in parallel by chunking the file
 - 2 key abstractions: map and reduce
 - name: "iMux Style"


We're at the end, so she can't complete the styles and has to jump to end of the talk

She's writing a book about all of this "Exercises in Programming", in bookstores spring 2014

- code should be on github soon

No conclusions are drawn at the end of the talk

- go find her slides to see the later examples