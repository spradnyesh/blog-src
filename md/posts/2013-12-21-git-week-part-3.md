{:title "Git week: part - 3"
 :layout :post
 :tags  []
 :toc true}

Hi there. Welcome back to the 3rd post in the "git week" series; visit the previous 2 [here](http://www.golb.in/git-week-part-1-13.html) and [here](http://www.golb.in/git-week-part-2-14.html). Today I will share another extremely helpful git feature with you all: "git bisect".

I am sure you, like me, have faced situations when a feature, which you were sure was working previously, is found to have stopped working correctly. Obviously something changed in the recent past that broke this feature. If we have automated tests, one of which caught this breakage, then it should be pretty easy to fix. But what we are interested in, in this post, is not "how" to fix, but to understand "what" broke this feature, and "when". Maybe, if you are like my manager, you are also looking out for the "who", to put some blame on.

Anyways, coming back to the issue at hand. So basically, we want to find out that particular fix which broke this feature. This is surprisingly easy to do with "git-bisect". I am sure, that by this time, based on my description above, and based on the name "bisect", you would have guessed what this git feature really does. Well, if you have guessed that this feature will do some kind of a "binary search" or a "divide-and-conquer" strategy to find the bad commit, you are absolutely correct.

So how this works is that you find 2 commit hashes, G and B, which stand for "good" and "bad" respectively. Basically, G is where you know that the feature was working correctly (maybe a commit from a few days ago, or from your last QA certified stable build), and B is where the feature is not working (maybe as simple as the HEAD).

The steps are as follows:

```
git bisect start
git bisect bad <B>
git bisect good <G>
```

Once you have given atleast 1 good and 1 bad commit hashes, git goes to work. It will successively give you the middle commit between good and bad and ask you to test. Once git has checked out a particular commit, you should (depending on your development environment) build, deploy and test. Then you know whether this particular commit (the one that git gave you just now) is good or bad. That is whether the feature you are interested in works correctly in this commit or not. Accordingly, you need to tell this to git as follows

```
git bisect good
```

OR

```
git bisect bad
```

respectively.

Continuing this binary search algorithm, you would have eventually reached the particular commit that introduced the bug. Now you can analyze what went wrong and why and come out of the exercise a learned man :)

After you have finished this bisection exercise, run the following command

```
git bisect reset
```

to come out of the bisect session back to where you started from.

One interesting situation you can also use git bisect is the other side of the coin. That is when you knew that there was a (hopefully minor) bug that was never getting fixed for a long time (because it was minor in priority, but was (maybe) difficult to fix) and you find out suddenly that it has been fixed (as a side effect of some recent commit). You can repeat the above exercise in this scenario to find out how the bug got fixed. And be an even more learned man ;)

For more details (advanced usage of git-bisect), RTFM and/or visit [here](http://git-scm.com/docs/git-bisect). Do share with us about if you have used git bisect before and how did it help you
