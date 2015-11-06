{:title "Git week: part - 4"
 :layout :post
 :tags  []
 :toc true}

Hello again. Welcome back to the 4th post in the "git week" series; visit the previous 3 [here](http://www.golb.in/git-week-part-1-13.html), [here](http://www.golb.in/git-week-part-2-14.html) and [here](http://www.golb.in/git-week-part-3-15.html). Today I will share another extremely helpful git feature with you all: "git subtree".

But before i begin with the actual feature, let me give you the background story about how I came to discover it. I find it useful to explain something by first explaining the situation where I needed to use it. I hope that you find it helpful too :)

Anyways, back to the background story. As I have hinted in my previous stories, I am working on a [pet-project](http://en.wiktionary.org/wiki/pet_project) wherein i have to collect a lot of data. Currently I am storing these data files locally in the project git repository itself. However, since I collect this data from multiple machines, I get some pull conflicts. Note that I say "pull" conflicts, not "merge" conflicts. This is because, obviously, not the same file is updated from all these local repositories at the same time. But i mostly get "non-fast-forward" errors.

I think that this can be (almost) solved by first doing a pull before doing a commit, followed immediately by a push. Also, once I setup the cron jobs running on these different machines to run at non-overlapping times, I can remove these conflicts altogether.

However, my issue is not that. My issue is that since my code and data resides in the same git repository, and I don't pull/push my code changes from/to the central repository (due to reasons mentioned in the "[git week, part 1](http://www.golb.in/git-week-part-1-13.html)" story), I end up facing these "non-fast-forward" errors anyways. The obvious solution that comes to mind is to manage the source code and data in 2 separate repositories. Since the data repositories are setup in a sync-ed fashion (as mentioned in the previous paragraph), and the source repository will be changed explicitly by me (in a non automated manner (using cron jobs, for example), I can explicitly push/pull the changes to/from the central repository (even if I change the code from multiple locations); that is by following the steps mentioned in "[git week, part 1](http://www.golb.in/git-week-part-1-13.html)" story. This way I will get rid of all these "non-fast-forward" errors that git has been throwing at me previously. Yay!

Ok, now to get to the technical part. How to split the original repository into 2, one for the data and the other for the source. Before I proceed to that, I am going to describe my source folder setup.

```
~/my-projects/
    - project-A/
        - config/
        - src/
            - model/
            - view/
            - controller
        - data/
            - db/
            - static/
                - css/
                - js/
                - images/
```

I am sure that you would have guessed the project to be a web-based project following the MVC architecture. I would guess that your project directory structure would be somewhat similar too. Our objective in this exercise is to split out the project-A/data/db (let's call this <new-repo>) out from the current project repository (let's call this <big-repo>). Note, that the important goal of this exercise is to get the history of <new-repo> changes into the new repository. Simply doing the following

```
mv <new-repo> <big-repo>/..
git rm -rf <new-repo>
```

would be easy to do, but would not achieve anything, because we would have lost all the history. Fortunately, it turns out that this operation, of splitting <new-repo> out of <big-repo> is so common, that git has introduced a 1-step procedure to achieve our goal. The steps are as follows:

```
cd ~/my-projects/project-A
git subtree split -p data/db -b project-A-db
cd ~/my-projects/
mkdir project-A-db
cd project-A-db
git init
git pull ~/my-projects/project-A/ project-A-db
cd ~/my-projects/project-A
git rm -rf data/db
```

The above steps apply to my directory setup. But, generically, we would do the following steps:

```
cd <big-repo>
git subtree split -p <name-of-data-folder> -b <new-branch-name>
cd <big-repo>/..
mkdir <new-repo>
cd <new-repo>
git init
git pull <path-to-big-repo> <new-branch-name>
cd <big-repo>
git rm -rf <name-of-data-folder>
```

The most important step of this whole flow, which I am sure you must have guessed by now, is the "git subtree" command. This is the one that does all the magic!

For more details of how the "git subtree" command works, please see [this](http://stackoverflow.com/questions/359424/detach-subdirectory-into-separate-git-repository/17864475#17864475) and [this](http://blog.charlescy.com/blog/2013/08/17/git-subtree-tutorial/)

I hope that you have found this story as fun and informative to read as I have found it to write. Do share your thoughts about both git and my writing :)
