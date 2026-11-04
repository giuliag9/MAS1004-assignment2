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

## What the mistakes of the baseline have in common (Step 3, mistakes_baseline_seed0 sheets)
this is what i noticed by looking at the sheets. For Busan it seems like it makes mistake mostly on outside photos, mistaken them for other city. For Osaka I notice right away here the mistaken phots are also all outside, I would say they have higher contrast, and more darker color in the images. Interesting is that the majority are guessed to be Tokyo. Whereas for Busan the guess was not mostly Seoul but also Tokyo and Taipei. For Seoul the photo in this sheet are also on a first look all darker, with tones towards blue. I notice there are some vehicles, and a more mixed photos of outside and inside locations. For Taipei these mistaken photos have more nature in them than the other photos in other mistake sheets. Interesting is that image 34 has a text with “Taiwan’ written in it and still the model guessed it as Seoul. For Tokyo  images in this mistake sheets are much more colourful than the other sheets. A mix of city view streets, cars and people. I think overall the mistakes have in common two major elements: first it's mostly outside photos, second it is images taken from afar, not with a closeup or focus but of general surroundings.

## Leaderboard
- track-a-1 "starter recipe" (released 30 October): leaderboard score 0.400 (0.395–0.403), grader's validation 0.497
- why validation and leaderboard differ (first thought): it is different because the images are different, not the ones on which the starter recipe trained on
