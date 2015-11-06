{:title "SVN unmerge"
 :layout :post
 :tags  []
 :toc true}

I recently came across the following scenario in my work-place. We use [SVN](http://en.wikipedia.org/wiki/Apache_Subversion) as our [version control](http://en.wikipedia.org/wiki/Revision_control) repository, and use a [trunk](http://en.wikipedia.org/wiki/Trunk_(software)) for production pushes and feature branch for feature development. However, this time we made the mistake of merging feature-branch into trunk-prematurely; because the client team wanted to test both trunk features/bug-fixes and feature-branch changes together before the next launch (a very valid ask).

Now the issue is that if we get an critical bug that needs to be fixed ASAP, then the trunk is no longer clean to do a bug-fix and re-deploy.

However, on the other hand, we could not have merged the trunk changes into the feature-branch, because merging back (into trunk, after feature-branch work is done and tested) would have been a nightmare. Basically we chose the easier merge (feature-branch -> trunk) now, in order to avoid the (super) messy merge (trunk -> feature-branch -> trunk) later on.

I think we faced this issue because how SVN handles merges. Basically, it takes the 2 copies of the same file at the HEAD of each branch and tries to do a intelligent merge; it does NOT take the history of the changes into consideration while merging. This causes conflicts

* less when we do feature-branch -> trunk, because (hopefully) the same files would not have been touched in both the branches (see part-1 of figure above)
* but (too) many when we do trunk -> feature-branch -> trunk, because every (merge) file is touched in both branches (see part-2 of figure above)

So how do we solve this situation? What do we do?

Enter git! In git, then branch and commit situation is extremely different (and easy). After creating a feature-branch, one should do "git rebase <trunk>" regularly to pull changes from trunk (known as "master" in git-land) into the feature-branch (see parts-3, 4 and 5 of figure above). This way, the conflicts, if any, will be very small and easily resolvable. Once the feature development and testing is complete, on simply does "git merge <feature-branch>".</feature-branch></trunk>

The benefit of this approach is:

* the feature-branch always has all trunk changes, so the client-team request can be easily fulfilled right from the feature-branch
* final merge (feature-branch -> trunk) is super easy, because no 2 files have changed simultaneously (if they had, then these merge-conflicts have already been resolved during the "rebase" step)

I don't know how to achieve the same in SVN; atleast not easily. Please share if you do!

Fortunately, for us, the issue turned out to be a false-positive, and we got spared.
ps: Read [this](http://paulhammant.com/2013/04/05/what-is-trunk-based-development/), [this](http://guides.beanstalkapp.com/version-control/branching-best-practices.html) and [this](http://svnbook.red-bean.com/en/1.7/svn.branchmerge.commonpatterns.html) for more info on common branching patterns
