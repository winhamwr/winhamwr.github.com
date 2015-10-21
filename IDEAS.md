## Wages of Wins for movies

This might exist. Research.

Look at box office gross versus other factors and attempt to assign causality:

* Existing IP?
* actors, directors, screen writers, producers, EP, studio

## Summary of the Case For Mars plan

## Getting started on Paleo with lots of resources

## WP90 for soccer

P = avg number of passes leading to a shot
K = probability that SoG scores
How stable are P and K across leagues/years/teams?

* Tackles (plus)
* Turnovers (minus)
* cards (minus)
* offsides (minus)
* Fouls within some distance of the goal? (minus)
* Fouls suffered (plus)
* Shots on Goal (plus)
* Shots not on goal (minus)
* Passes that result in a shot (plus). How to distribute the credit?
* How do you factor out things that coaches decide like who takes corners/PKs/FKs? Maybe negative for turnovers and shots off frame account for this?

What about for keepers? (separate problem)

## Write about deployment and Neckbeard

## Django/Python Ideas

### Rules for non-brittle tests

* Never assert on text!
  * Use classes and IDs everywhere
  * Messages are the worst culprit
  * Tests benefit from DRY
  * But not too DRY (copy/pasting from the code under test is good)
  * Smaller tests are better
* Factories and fixtures, how to decide

### 3 tips for solving 80% of Django Performance Problems

* Use Johnny-cache
* Most of the benefits of a read slave without the fuss
* Be aware of weird things you do that require manual cache invalidation
* Adjust your default cache duration accordingly
* Watch out for pages with lots of queries
* Ruthlessly eliminate queries-per-row
* Use query count tests with fuzzy query ranges
* `select_related` and `prefetch_related`
* Don't do complex things in the DB: Never use sub-queries
* `values_list` of pks are what you should be passing around
* Embrace slightly more, much simpler queries
* Aggregates can and will destroy you
* For the other 20%, use New Relic and the "Apdex most dissatisfying" report

## Build Mobile Pacers Bikeshare Site

https://www.pacersbikeshare.org/header-nav/station-map/

* `LoadKiosks()` has the data and pushes objects to `kioskpoints` and `markers`
* [pjscrape](https://github.com/nrabinowitz/pjscrape)
* [zombie](http://zombie.labnotes.org/API)

## Cognitive advantages of neurodiverse folks

* Autism has [real costs](http://slatestarcodex.com/2015/10/12/against-against-autism-cures/). It's a big bundle of things that often comes with a big list of negatives. Most autistic folks suffer.
* Even if the big negatives are avoided and someone has a high enough IQ to compensate when dealing with normal humans, folks on the spectrum are at a disadvantage. Most humans default to assuming other humans think like them and are motivated like them, and for most folks, that's a good default. It's not good or spectrum folks, so they tend to be disadvantaged in social interactions. It's better to be good with people than to be good with things.
* For some percentage of folks on the spectrum (typically labeled with Aspergers),
  the condition typically comes with cognitive advantages relative to dealing with things
  (and, when properly trained, also dealing with humans in structured, practiced scenarios).
  * Humans love narratives, but narratives are misleading. Much of the Thinking, Fast and Slow-style biases to be corrected are because we use heuristics based on narratives instead of probabalistic thinking. Spectrum folks form fewer information-hiding narratives.
  * [Social Desirability Bias](http://econlog.econlib.org/archives/2015/10/social_undesira.html) leads people to the wrong answers whenever one is working on the frontier of knowledge. Spectrum folks are much less likely to fall prey (either because they don't notice, or have different preferences wrt knowledge versus positive social feedback).
  * Humans love consuming information about people, especially famous/influential people and people they know. This tribal gossip affinity makes evolutionary sense, but that love can crowd out information about things. It's information about things (of which psychology is a thing, but a specific person's psychology isn't) that change the world. 
