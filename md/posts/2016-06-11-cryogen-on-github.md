{:title "cryogen based static site on github"
 :layout :post
 :tags  ["cryogen" "static-site" "github" "clojure"]
 :toc false}

[Github Pages](https://pages.github.com/) are a good way to host your own blog. [Jekylly](http://jekyllrb.com/) is the de-facto standard of achieving this. but being a [Clojure](http://clojure.org/) guy, i wanted to find something to achieve the same using Clojure. and find i did => [Cryogen](http://cryogenweb.org/index.html).

Cryogen does have a "[deploying-to-github-pages](http://cryogenweb.org/docs/deploying-to-github-pages.html)" documentation. the Cryogen docs suggest that you push the "public" directory to github gh-pages

however, i'd like to store both the source (.md files, images, etc) and the generated static content (.html files) on github. in order to do this, i have a different setup that i'd like to share with you

## one time setup steps ##

- create cryogen project as shown [here](http://cryogenweb.org/docs/getting-started.html)

    lein new cryogen my-blog
    cd my-blog
    ~/my-blog $ lein ring server

- add pages/posts to ~/my-blog/resources/templates/md/
- "lein ring server" will automatically generate static site whenever a new post/page is added/edited
- add the "resources/templates/public/" to github account as is suggested in the Cryogen docs [here](http://cryogenweb.org/docs/deploying-to-github-pages.html)
- add the "resources/templates/md/" to another github account as backup of your blog source

this approach has the following benefits

- backup blog source (that you can move easily from 1 machine to another)
- store generated static files that will be served by github pages
- upgrade cryogen without it conflicting w/ existing source
