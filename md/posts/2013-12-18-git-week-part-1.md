{:title "Git week: part - 1"
:layout :post
:tags  []
:toc true}

[git](http://www.git-scm.com/) rocks! I have been using git for all my personal projects for at-least the last 2 years now. But what I have learned in this week is probably more than what I have learned in the last few months, and I am dying to share them with you!

**git-bundle**: Honestly, I learned this maybe in the last month, or the month before that. But then, I wasn't blogging actively at that time. So what the heck? I will share it with you as if I have learned it in this week ;)

Anyways, coming to the real issue that "git-bundle" solves. I work in a jail environment; well not really, but what's the fun in something if there is not even a little hint of exaggeration? The point is that we are not allowed access to git hosting sites like [github](https://github.com/), [bitbucket](https://bitbucket.org/), etc. So I was having trouble moving my personal projects (that I work on during my free/slack (see my article "don't break the chain" to see how to make productive use of slack time) time between home and office without access to a central repository to sync between my home and office repositories. I searched for other github-like sites (even paid) that I might have access to from my jail, but without success. I was very frustrated.

And then, instead of looking outward, I looked inward (wow, that came out very philosophical!). That is, instead of finding websites that could help me, I searched for whether git has any functionality that could liberate me. And voila, the thing that I found, "git-bundle", was exactly what I was searching for.

That's enough of history. Lets get to the details of how git-bundle helped me. For explaining the situation however, we need to set up some background first. Let's say the 2 repositories (home and office, in my case) that we want to keep in sync are A and B. We will cover 2 cases. case-1 is where we have created a new repository (A), and where B has not been setup yet. case-2 is where both A and B exist already (say before access to github was removed), and you have now made changes to one of them, say A. Lets start with the 1st case first. Perform the following steps at A:

```
cd <repo>
git bundle create <repo-name>.bdl master
git tag -f "bdl" master
```

Note that the ".bdl" extension is completely arbitrary, and git does not put any restrictions on it. Similarly you can decide on what tag you want to use. Tagging is useful when sending incremental patches (case-2), as we will show below.

Back to case-1. Transfer the <repo-name>.bdl file to B (via email, etc) and perform the following steps at B:</repo-name>

```
git clone -b master <repo-name>.bdl <repo><repo-name><repo></repo></repo-name>
git tag -f "bdl" master
```

Once the initial setup is done, we simplify our life to be the same as case-2, that is, incremental sync. For this case, lets assume that you have made some changes in B and want to move them to A. Perform the following steps at B:

```
git bundle create <repo-name>-<date>.bdl bdl..master<repo-name><date></date></repo-name>
git tag -f "bdl" master
```

Again, the <repo-name><repo-name>-<date><date>.bdl filename is completely arbitrary. I like putting the date part in there because that helps me avoid confusion when I am emailing multiple bundles everyday between my office and home. The part where we say "bdl..master" is the "tagging" part that i had mentioned earlier. Basically, what this tells git-bundle is to bundle only those commits that happened between when we had cloned (or "pull"-ed as explained below) earlier and where the HEAD of the master branch is now.</date></repo-name>

Then, we move the bundle file from B to A, and perform the following steps at A:

```
git pull <repo-name>-<date>.bdl master:master<repo-name><date></date></repo-name>
git tag -f "bdl" master
```

The steps are exactly the same when you want to sync from B to A. Now, lather, rinse, repeat!

ps:

* Read the beautifully written man page "man git-bundle" for more info
* Looks like this has become a long post. Well I will write about the other git magic stuff in the next post!
