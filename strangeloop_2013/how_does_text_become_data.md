# Natural Language Processing

- github.com/rspeer/text-as-data

- first off, ipython is kick-ass

- people expect to interact with a computer in a more natural way

- problem: to the computer, text is gobbledygook

- know this: language is ambiguous, and you can't really fix it. So embrace the ambiguity

# What to do with nlp?

 - classification
   - remove spam comments, eg
   - classify an email as angry so you see it first

 - similarity between documents
 - search


# Examples

## Python: word splitting and normalizing

 - use nltk
 - check out morphy (?) for turning "wondering" into "wonder" when you tokenize

- N-gram models, sequences of words
- frequency of words over time

- Documents are "bags of words"

- Which n-grams are interesting

 - "vice president" is more interesting than "the vice" which is more interesting than "of the"

 - use a contingency table
 - find the probability that any two words are going to be vice president, eg

 - use nltk.bigrams() for this
 - text.collocations() show the statistically interesting parts

## Text classification

 - talks about machine learning and naive bayes classification b/c naive bayes works well on data structured like language



 - makes nltk to make a naive bayes classifier, using (scikit learn) sklearn which is used for making classifiers
 - this is the movie review example
 - he recommends naive bayes first b/c it's easyish and you get to iterate


 - TF-IDF normalization

 - go look at his slides... it makes total sense

 - shows the angles between alice in wonderland vs. shakespeare plays
   - see the narrow angle between hamlet, macbeth, etc compared with AIW

 - remove ubiquitous words b/c they convey no information
   - "death" appears in every text in the gutenberg corpus and consequently isn't helpful

 - "Dimensionality reduction"

  - vector spaces groups words and documents by meaning

  - "things on my desk" vs "things in my car"

  - holy fuck this dude talks fast

  - look at gensim python module

  - latent semantic inference model out of the bag of words
  - use this to measure similarity between documents
  - then you can query for similarity to a particular document

- Is this all there is to word meaning?

  - for example, what else can "alien" mean?
  - this is kind of a problem with training a model one one set of documents
  - can cause a model to fail with similar documents where the word meanings are different

  - Modeling word meanings

    - "wordnet"


    - "I bought groceries at the grocery store"
      - so much meaning in this one sentence
    - concepts can be connected via relations, such as "buy groceries" and "money"
    - each concept requires other contexts
    - ultimately, this results in many connections in a gigantic graph
    -  "conceptnet" is their research project
      - contrasts with wordnet
      - because it's a big complex mess, which is what you need
    - conceptnet as a vector space
      - things that are closer are more related


  - ConceptNet example
    - interact with the ConceptNet API
    - See his sample code
    - This is so cool!

# Luminoso

  - this is the company they started
  - free access to alpha/beta test
  - hub@luminoso.com



# Q & A

 - how do you improve sentiment analysis by looking at sequence of words?
   - "this is shit" vs "this is the shit"

   - this one is a very hard problem, in part because the word "the" is so frequent and often ignored

 - have they looked at unsupervised (deep) learning?

   -



