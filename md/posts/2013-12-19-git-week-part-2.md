{:title "Git week: part - 2"
 :layout :post
 :tags  []
 :toc true}

Hello again! Today we will see some more git magic. (Click [here](http://www.golb.in/git-week-part-1-13.html) to see my previous post on git.)

This time we are going to learn about the "filter-branch" functionality which proved immensely helpful to me in 2 different scenarios, both unrelated, but both of which happened yesterday at different times of the day.

The 1st was that i use 2 different aliases for different projects. Unfortunately, in one recently started project, I used the default (wrong, in this project) user.name/user.email combination. Fortunately, I had not published it into any online repository (see my previous post as to why ;)). So I still had the opportunity to change this information. I knew that it could be done, but did not know how. So I learned it and will share it with you:

```
git filter-branch --commit-filter 'GIT_COMMITTER_NAME="<new-name>"; GIT_AUTHOR_NAME="<new-name>"; GIT_COMMITTER_EMAIL="<new-email>"; GIT_AUTHOR_EMAIL="<new-email>"; git commit-tree "$@";' HEAD
```

Of course, your case might not be as simple. That is, unlike me, you might need to change based on some condition, or only change a few particular commits. You can find a good example [here](http://stackoverflow.com/a/870367).

The second case where filter-branch turned out to be extremely life-saving was in the same recently started project. I have been scraping some info from the Internet and storing these (separate) files in the local repository. It was big data; largest that I have worked on personally, growing at a rate of about 23Mb everyday. Now it turned out that if I would concatenate the contents of these files into a single file then it would keep my directory structure more manageable and also better for the analysis tool that I would use.

But the problem was that I had already scraped data for 3 days (70Mb of data), and even if I removed the original files, they would still be in the history. This would mean that my repository would simple double the moment I moved to the new file format. The solution was to remove these files (I did not really need them in the history since I was still retaining the "data" in the new format) from history. This is where "filter-branch" feature of git came in handy again. The commands to achieve this are:

```
git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch $files" HEAD
rm -rf .git/refs/original/ && git reflog expire --all &&&amp;nbsp; git gc --aggressive --prune</blockquote>
```

Fortunately, even though I had hundreds of (small) files, I had created the filenames in the <date-in-yyyymmdd-format>-<source> format, so it was very easy for me to invoke the commands like so:</source></date-in-yyyymmdd-format>

```
git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch <yyyymm>-*" HEAD
rm -rf .git/refs/original/ && git reflog expire --all &&&amp;nbsp; git gc --aggressive --prune</yyyymm></blockquote>
```

The 2nd "rm -rf" command is needed to remove temporary files that git maintains for a long time even after asking it to clear everything.

With this technique, I was able to reduce the repository size (after adding the new format files) to about 60%, a good saving :)

Remember, both the above actions are destructive and may mess up your repository, so it's best to try them out on a clone first. Also, do NOT do them if you have already published your changes to prevent others from facing non-fast-forward pull errors.
