# Log

One entry for each recipe, selection or Track B model you train, newest at
the bottom. The numbers come from `experiments.csv`. "Why" and "what it means"
are in your own words: your agent asks you for them and does not make them up.
End the log with your plan for what to try next.

<!-- The form of an entry:

## <date> <tag> (Track A or B)
- changed: what is different from the run before
- why: your reason
- validation: 0.000 (before: 0.000)
- what it means: what you think the result says
-->

## What tells the cities apart (Step 1, first look at the photos)
it seems like the outisde locations tells the city apart, however there are also many photos inside or of food
as well as photo of object. maybe the text present in the photo tell the city apart too

## 2026-10-30 baseline (Track A)
- changed: nothing, the starter recipe, trained with seeds 0 and 1
- why: I trained the starter recipe with seed 0 and 1 and the tag baseline as the step 2 said. After doing step 1 and looked at the photos I noted what could tell the cities apart, but decided to first train the starter recipe and later make changes. In step 3 I can look at the mistake ofthe starter recipe, and have a better idea for the changes.
- validation: 0.4961 (seed 0), 0.4922 (seed 1)
- what it means: From what I understood, a seed changes the random starting point, so it's telling me there is a slight difference based on where the starting point it, but i'm not sure is telling much else since it is a very small change.
