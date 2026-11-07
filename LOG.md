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

## 2026-11-06 track_b1 (Track B)
- changed: nothing, train_b.py as it is (ResNet18 at 224, 4 epochs, starter training photos)
- why: this run is the requested from step 8, train track b as it is.
- validation: 0.4933 (Track A baseline seed 0: 0.4961)
- what it means: It's slighltly different from the track A baseline, but still somewhat similar, where Tokyo has highest score, seoul is slightly higher than the baseline, and the same is for Busan, and Osaka.

## What I notice comparing the mistakes of balanced and baseline (mistakes_balanced_seed0 and mistakes_baseline_seed0 sheets)
For Busan the balanced mistake still have some in commons as baseline mistakes, I notice some photos of roads with cars and outside.

For Osaka as well some few photos are the same, in the balanced mistakes there are a few more photos of inside, compared to the baseline mistakes. 
For Seoul it maintains some photos of vehicles, and food. 
For Taipei as well, some mistake changed. Less nature but still some outside photos
Tokyo mistakes are also still colorful.

Overall, the mistakes from balanced are not the exact same as the baseline, even if some photos are still the same. I think in general the type of photos in the mistake is sort of the same as baseline (apart from the difference in Osaka). This can be understandable since the only change in balanced is that the photos are drawn equally, but I haven’t made other changes to it, or removed photos.

## 2026-11-06 balanced_zoom (Track A)
- changed: on top of balanced, RandomResizedCrop scale from (0.35, 1.0) to (0.1, 1.0)
- why: I think for the next change it would be good to work on balanced to maintain the improvement achieved with it and see the effects of next changes when cities are equally drawn. I think I want to try the zoom in the photos since some mistake photos in balanced are still from afar so I would still want to try since it was one of the first thing I noticed at the beginning.
- validation: 0.5089 (before: 0.5117, balanced)
- what it means: The results tell me that adding the zoom to the balanced didn't improve the model overall, although there are some improvements for Busan and Taipei, but Seoul and Tokyo went down a bit. So the zoom was useful for some city but not for others, meaning it's not an overall change that works for all the cities. It could be kept into consideration to combine in a second moment with other changes.

## 2026-11-06 balanced_brightness (Track A)
- changed: back to balanced (balanced_zoom undone), then ColorJitter brightness from 0.2 to 0.5 (each training photo made between 0.5 and 1.5 times as bright); contrast and saturation stay 0.2
- why: for the next change I would start from balanced again, in order to check the change without zoom. I think at this point I should address another element I noticed in the mistake sheets, which is that some photos in the mistake are darker. So it could be interesting to make some photos lighter for the training, perhaps by making the light vary like for the zoom / let's use both, darker and lighter 0.5, - 1.5 , since in the mistakes for some cities the photos were darker, while in other not.
- validation: 0.5064 (before: 0.5117, balanced)
- what it means: this results tell me that change in brightness were less useful than zoom, but it still was slighly good for Busan Osaka and Taipei. For Osaka it was more effective than zoom. It shows a differnet situation for Seoul and Tokyo, which makes me think I should consider these two city in similar way since both went down and up together with changes.

## Step 7: what I see on the suspects of balanced (suspects_balanced_seed0 sheets)
Suspect balanced Busan: I notice photos that are closeup or focus on object or things such as food, vase, flowers, books and vehicles. 

Suspect balanced Osaka: similarly photos closeup or focus of animal, food

Suspect balanced Seoul: closeups on objects, food. but also outside buildings and people 

Suspect balanced Taipei: here similarly photos of objects, animal, food, 

Suspect balanced Tokyo: I notice photos of food, cars, people

My rule (written before dropping): I think overall I notice that there als also many outside photos, but I also think that ouside photos usually have a lot of elements into them that can be useful for the model, so I wouldn't drop them. I think finding one specific only rule is not easy as the images a various, so I think the rule I want to make follows what I noticed, meaning photos that are closeups/focus on only one object or thing, that doesn't give much other element in the photo.

My requests to the agent (Step 7, word for word):
Drop 3, 16, 17, 20, 26, 28, 30, 32, 34, 44, 48, from suspects_balanced_seed0_busan_00.png because “closeup or focus on one thing” 

Drop 5, 6, 9, 10, 11, 16, 20, 34, 36, 48 from suspects_balanced_seed0_osaka_00.png  because “closeup or focus on one thing” 

Drop 1, 3,4, 7, 8, 18, 20, 22, 23, 26, 30, 33, 41, 43, from suspects_balanced_seed0_seoul_00.png because “closeup or focus on one thing” 

Drop 4, 5, 12, 15, 17, 26, 30, 31, 33, 36, 42, from suspects_balanced_seed0_taipei_00.png because “closeup or focus on one thing” 

Drop 6, 9, 10, 14, 17, 18, 22, 23, 25, 31, 36, 39, 41, 42, 43, from suspects_balanced_seed0_tokyo_00.png because “closeup or focus on one thing”

## 2026-11-07 balanced_rule_drop (Track A)
- changed: recipe back to balanced (balanced_brightness undone); 61 training photos dropped by my Step 7 rule (busan 11, osaka 10, seoul 14, taipei 11, tokyo 15), reason "closeup or focus on one thing"
- why: my Step 7 rule above
- validation: 0.4952 (before: 0.5117, balanced)
- what it means: the validation on this training was lower than the normal balanced so it makes me think that perhaps what I decided to drop and my rule was not the best choice.
- afterwards: the 61 photos were put back (selection.csv removed, so training uses all training photos again); track_a/dropped.csv stays as the record of what was dropped and why

## 2026-11-07 balanced_smaller_lr (Track A)
- changed: on top of balanced (all training photos again), peak learning rate from 3e-4 to 2e-4 (lr in make_optimizer and max_lr in make_scheduler); schedule, warm-up and weight decay unchanged
- why: I think I want to try to change the learning rate on balanced. I remember from assignment 1 that a larger learning rate was not necessarily better so in this case I would make it a bit smaller. / I wouldn't go too much lower so 2e-4 for now
- validation: 0.5065 (before: 0.5117, balanced)
- what it means: the results of this training are lower than the balanced one, it was good for Seoul but not for Taipei. It seems like the changes I made after balanced, were less effective or were only effective for some cities but not for the overall validation.

## 2026-11-07 balanced_zoom_small_lr (Track A)
- changed: balanced with two earlier changes combined: RandomResizedCrop scale (0.1, 1.0) as in balanced_zoom, and peak learning rate 2e-4 as in balanced_smaller_lr; nothing else
- why: At this point I think it could be interesting to try and combine previous changes since after balanced, the other changes were positive for some cities and negative for others. Perhaps combining the change in zoom (which previously was positive for Busan and Taipei especially) with smaller lr (positive for seoul), could create an overall better validation than balanced by itself. The risk is that the two changes cancel each other and the validation ends up still lower, but in that case it would tell me that it's not the best way to combine.
- validation: 0.5138 (before: 0.5117, balanced)
- what it means: combining zoom and smaller lr was useful, especially for Busan and Taipei. I expected Seoul to have a higher score since with the learning rate it increased. I also thought tokyo would stay around the scores of zoom and small lr, but didn't, meaning I still have to find what makes Tokyo score go up.
- released as track-a-3 "balanced zoom+lr" (7 November)

## Leaderboard
- track-a-1 "starter recipe" (released 30 October): leaderboard score 0.400 (0.395–0.403), grader's validation 0.497
  - leaderboard per city: seoul 0.62, busan 0.19 tokyo 0.70 osaka 0.25 taipei 0.23
- track-a-2 "balanced" (released 5 November): leaderboard score 0.410 (0.402–0.419), grader's validation 0.502
  - leaderboard per city: Seoul 0.57	Busan 0.26	Tokyo 0.61	Osaka 0.33	Taipei 0.28
- track-b-1 "Track_B_1" (released 6 November): leaderboard score 0.389, Track_B_1 1.81 GMACs @ 224
  - leaderboard per city: seoul 0.60	busan 0.16	tokyo 0.68	osaka 0.23	taipei 0.28
- why validation and leaderboard differ (first thought): it is different because the images are different, not the ones on which the starter recipe trained on
- why validation and leaderboard differ (after talking about it): the reason why the valiadation on leader board is different might be because the images are not similar to the one in validation
