{:title "Git week: part - 5"
 :layout :post
 :tags  []
 :toc true}

Hello again. Welcome to the 5th post in the "git week" series; visit the previous 4 posts [here](http://www.golb.in/git-week-part-1-13.html), [here](http://www.golb.in/git-week-part-2-14.html), [here](http://www.golb.in/git-week-part-3-15.html) and [here](http://www.golb.in/git-week-part-4-16.html). Today I will share another extremely helpful git feature with you all: "git rebase -i".

If you remember, We have already used git-rebase once in the [svn unmerge](http://www.golb.in/svn-unmerge-10.html) post. In that post I already showed how one could use git-rebase to easily handle things that are either too difficult or, at times, impossible to do in SVN. Today we will see an advanced use of git-rebase, that is "git rebase -i". This command allows us to reorder commits. Yes, you read that right! One can actually reorder commits in git. Ain't that cool?

One can easily imagine certain obvious uses of this feature. For example, lets say I always push to central repository from my master branch, but locally use feature branches. Also, I may be working in parallel on 1 or more features and may also fixing bugs directly in the master branch. And I may be merging (after feature completion) from some feature branch into master. In this case, I would want to reorder the commits in a more meaningful order (one that makes more sense and shows a well thought flow to an outsider) on the master before pushing it to the central repository.

In fact, this use case happened to me last week. I was working on a certain feature, and had merged the incomplete feature to master (I know, bad boy ;) ); but, fortunately, not pushed it. Then I noticed a critical bug in the production system which had to be fixed immediately. So now this bug fix is at HEAD of master, and the unfinished feature is at "HEAD~1" location. Obviously I cannot push this state to production. This is where "git rebase -i" saves the day!

I do the following

```
git rebase -i HEAD~1
```

Here, git opens up an editor asking you to change the order of the commits (newest is at bottom). So I swap the last and one-but-last commit and save and quit the editor. Then I did

```
git log
```

to see that the last 2 commits (incomplete-feature and critical-bug-fix) placed in the correct (as desired) order! Now I pushed the critical-bug-fix to central repository and created a build and deployed to my production server. This time, I took the care to not push the HEAD of master, but HEAD~1 to central repository.

As an added bonus, I am going to tell you a special feature of "git rebase -i". That is once git opens the editor for you to reorder your commits, you will notice the following statements at the end of the editor

```
# Rebase 3a40bd2..ba8573d onto 3a40bd2
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

If you read these statements carefully, you will notice that "git rebase -i" is allowing you to not only reorder your commits, but to delete, edit, etc your existing commits. This is awesome knowledge and will surely come in handy in the future. Yay!

**WARNING**: Do remember, that this command makes very low level modifications to your repository and you can easily screw things up. So you should always make changes like these to a cloned repository. Also, as always, do NOT make these changes to the part of history that you have already published.

I am going to keep this git-week series like a 5 day work-week and end this series here. I hope you found this (and previous posts [here](http://www.golb.in/git-week-part-1-13.html), [here](http://www.golb.in/git-week-part-2-14.html), [here](http://www.golb.in/git-week-part-3-15.html) and [here](http://www.golb.in/git-week-part-4-16.html)) useful.

Do let me know if they did, and how. Also let me know if you like my writing and would like me to write more such articles on other topics as well. Your comments will give me the confidence and motivation to "not break the chain" (see my previous article [don't break the chain](http://www.golb.in/dont-break-the-chain-12.html))
