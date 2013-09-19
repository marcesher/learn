Martin Odersky

The problem with types


# Why static?

 - more efficient,
 - better tooling
 - fewer tests needed
 - better docs
 - safety net for maintenance

# Why dynamic?
 - tend to be simpler
   - types add incredibly to the footprint of a language, because they are the things that confer assurance
 - fewer puzzling compiler errors
   - types catch errors early, but sometimes the errors from the compiler are inscrutable
   - sometimes easier to figure out what went wrong at runtime when you just let it crash
 - less boilerplate (think Java)
 - easier for exploration (think python!)
 - no type-imposed limits to expressiveness


# What is a good language for design?

 - one that helps discover great designs
 - we want patterns, which derive from abstractions
 - we need constraints, and odersky believes Types help us express constraints

## Example

 - functional collections, monads, applicatives
   - you're basically led to a good design
   - "powerful patterns made safe by types"

**But**

- Type systems are hairy, otherwise there wouldn't be so many different ones
- they're a pain


- Odersky shows some comparisons between weak/strong and dynamic/static
- Then, for static, compares detailed vs coarse type systems

# My way or the highway language

 - Go, Java 4, Pascal
 - simple type systems
 - no generics (java 4)
 - not that extensible

 - leads to simpler tooling (faster, simpler tooling b/c type checker isn't complex)
 - highly normative
   - everyone writes the same java b/c there's only one way to express yourself
   - essentially, the language designers did the job of design for you and now you just apply it

# Type it to the max languages

 - haskell, scala, ocaml, f#
 - rich language to write types
 - type combination forms, including generics
 - type systems often inspired by logic

 - these languages tried to address the advantages of dynamic languages head on (see his slides)
 - some of these advantages are well-addressed, such as expressiveness (in scala, anyways, according to Odersky)
 - some aren't, eg simpler languages and inscrutable compiler errors



# We want

 - precision
 - soundness
 - simplicity

 - Take any two?

# Abstractions

 - how can we get the best of all worlds?

 - Two fundamental forms
   - parameters (positional, functional)
   - abstract members (name based, object oriented (i.e. modular))


 He shows some types in Scala, such as:

 - BitSet -- named type
 - Channel with Logged -- Compound Type
 - and so on, through Refined, Parameterized, Existential, and Higher-kinded types
 - these are a mix of modular and functional types, and they are orthogonal... you can use them all in combination with one another
 - Because of this high dimensional space, you end up with the ability to do the same thing a lot of different ways (which people complain about)
 - Non-orthogonal designs don't have this problem to the same degree, btw


So, what can Scala do about this problem? How can it reduce dimensionality?


# "Projections"

 - proposes to have the compiler collapse all the functional types (existential, higher-kinded) into modular types
 - this may enable scala to remove certain of these functional types from the external representation
   - eg remove Existential types, and if you do need it, rewrite it in terms of its Projection
   - since Existential types are little used and only in dubious circumstances anyways


# Dot and Dotty

 - DOT: calculus for Dependent Object Types
 - DOTTY: new language based on DOT that compiles down to Scala (I think)
   - Still has named types, refined types, intersection types
   - existential and higher kinded go away
 - Generics
   - parameters modeled as abstract members
   - arguments modeled as refinements
   - see his slides for an example of this in action


# Additions to Scala

 - adding & and | (union and intersection) types to fix the compiler problem with no upper bound on joined types (this is wrong... see his slides)
 - SIP 18 already forces you to flag usages of existentials and higher kinded types
 - should give people an idea of the effort involved in bringing Dotty innovations to Scala


# Essence of Scala

 - harness the power of naming
 - a simple language struggling to get out
 - he's trying to address the criticisms of scala being too complex by targeting the things that actually *are* complex