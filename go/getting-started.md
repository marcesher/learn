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
  1. Effective Go: http://golang.org/doc/effective_go.html
  1. Work through the Go / Angular preso again: http://blog.campoy.cat/2013/12/writing-moder-web-app-with-go-tdd-rest.html
  1. Create a sample REST API for something dumb
  1. Read through some of the code recommended by Jeff Hodges: http://www.somethingsimilar.com/2013/12/27/code-to-read-when-learning-go/
