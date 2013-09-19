Jenny Finkel (sp?)

Prismatic

# Stack

 - clojure backend, clojurescript frontend
 - very open-source (check out their github)


# Discovery Problem

 - Figuring out what's relevant
 - finding content you don't see, but which you'd probably enjoy
 - Finding "interesting content you *should* see, but which you'd otherwise miss out on"
 - "this is what serendipity is all about... finding you these gems"

# How do they do it?

 - crawl social and open web for content being shared
 - analyze and categorize content being crawled
 - real time personalization for users based on their network and interests

 - Goal: build a ranker to find a small number of great articles for a user from a large document index
 - How: use machine learning

 - There is no "secret sauce"
 - It's about attention to details, assembling components thoughtfully

The rest of the talk is a dive into how they do it. I'm just taking notes on the highlights for me (as a person with zero machine learning experience)


- Dates were a problem for them: lots of articles have many different dates... date published, date updated, comment dates, even current date/time.
  - so they wrote a date extractor that's imperfect but still highly accurate

- social verbs matter: they know what actions other prismatic users make on an article: like, share, remove, click, etc

- the text: look for terms to identify a "fingerprint" for what the story is about

- for each user, they maintain long term summary stats for every topic / interest a user has interacted with. Think of it as a summary score

- every user session is snapshotted
 - articles shown, their order
 - actions a user took
 - user's state at beginning of a session vs the end (favorites, interest scores)

**Constraints**

- rankings computed on the fly, so this must be fast
- "so many documents, so little computation time"

- what users like, and what they claim to like, are quite different.
- user's likes are often aspirational (I want to like hiking, but I really like trash tv)

- different users are different... you're all unique snowflakes


**Evaluation**

- how do we know if we've done a good job?

- Real goal: improved user engagement

- but it takes long to change user behavior, and even longer to measure changes in user behavior
  -- consequently, you can't do machine learning on it

- SO: use a surrogate goal: "More user interactions"
  - must believe this is a good surrogate for improved user engagement
- easy to measure from test data
- data divided into training data and test data
- build model using training data
- use the model to reorder the articles in the sessions from the test data
- then evaluate on the reordered articles


**Architecture**

- Formula for a ML problem:

1. collect data
1. featurize the data
1. train the model
1. Deploy

## Collect data

 - save session info (see earlier stuff)
 - transform data into an article/user pair
   - then, whether it was a positive or negative interaction

## Featurize data

 - represent the user/article pairs as a vector
 - each feature gets a value (1, 0, 2, etc)
 - things like "num of times a user previously clicked on this publisher", "article has a picture", etc
 - then, each feature gets a weight
   - this is the "learn" part of machine learning... feature weights are learned
 - then, take the product of the feature value and feature weight, to arrive at a total score for the user/article pair
 - the goal is to find the best possible model for these weights
 -

## Training the model

 - this is numeric optimization
 - try to find the mathematical optimum


## Classify new data

 - straightforward ranking is simple
   - use learned weights to score articles for current user
   - sort articles by score

 - But: it's too slow!
   - instead, they use algebraic manipulation
   - weight vector is user specific, but features are universal

## Deployment cycle

 - train the model, evaluate on saved user session data, deploy to prod
   - this part is fast

 - after deployed, it's evaluated on live users
 - this part is much slower, and it's where they continue to learn and refine models
 - then, repeat the training cycle


# problems they encountered

 - Data bugs (are the worst)
   -  there was a bug in the bits that saved user session data
   - it was saving something at the incorrect time
   - this goosed the user's interest score for the doc's publisher
   - consequently, the optimization process exploited this bug and learned a really high feature weight for doc publisher
   - so it placed way too much value on the publisher
   - **Very important** - they discovered this basically based on a smell test... something seemed wrong with the data

 - Presentation bias
   - users more likely to click earlier articles
   - adds noise to the training data
   - model assumes user clicked b/c of interest, not location
   - makes live rankers look better than they are

- Ranking vs Normal ML

  - tells the story of the Daily Mail
  - became a circular problem for them
  - daily mail kept getting bumped up and down, based on conflict between user's click-through rate on daily mail articles vs. removals when the ranker showed them too much


- Statistical bleeding

  - "explorer" vs "exploiter" ranker


- Simpsons Paradox

 - check it out on wikipedia