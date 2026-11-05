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

## 2026-11-05 more_often_outside (Track A)
- changed: in sample_weights, photos whose file name starts with osv5m_ or youtube_ are drawn twice as often as the others (commons_); no photo removed
- why: For the first change I think it's good to start from what I noticed in the mistake sheets. The first element was that it was outside photos, second was photos with no closeups. I would do one change at a time. Since the model got wrong many outside photos it could be useful to train it on a set of data where the outside images are many and appear more times. I think I wouldn't delete the inside photos but it would be good to make the outside photos appear more often during the training. / yes, let's use the name of the file since doing it by checking each photo is not possible. This way it should be mostly outside pictures. So let's do it for both youtube and osv5m, twice as often for now.
- validation: 0.4876 (before: 0.4961, baseline seed 0)
- what it means: I think this results tells me that the outside photo are perhaps a problem. i thought that training the model on more photos of the outside would be useful but the validation was lower than the starting recipe, only Osaka had a higher validation.

## 2026-11-05 balanced (Track A)
- changed: back to the starter recipe (more_often_outside undone), then in sample_weights every city drawn equally often: each photo gets one over the number of photos of its city
- why: let's try to make the model train on the same amount of photo for each city. It could be useful for the model to train equally on each city photos, and it could be a good point for then observing changes and what mistakes it makes in that condition
- validation: 0.5117 (before: 0.4961, baseline seed 0)
- what it means: This results tells me that it's good for the model to train on equal variety of photos from each city, even if it means that Seoul and Tokyo got lower score.
  (what I mean by equal variety is that the photos of the cities are drawn equally so  the model trains on a variety of photos that is equal between the 5 cities)

## Leaderboard
- track-a-1 "starter recipe" (released 30 October): leaderboard score 0.400 (0.395–0.403), grader's validation 0.497
- why validation and leaderboard differ (first thought): it is different because the images are different, not the ones on which the starter recipe trained on
- why validation and leaderboard differ (after talking about it): the reason why the valiadation on leader board is different might be because the images are not similar to the one in validation
