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
