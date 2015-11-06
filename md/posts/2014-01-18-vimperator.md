{:title "Vimperator: part - 1"
 :layout :post
 :tags  []
 :toc true}

Continuing with [this ](http://www.golb.in/kill-that-rat-28.html) and [this](http://www.golb.in/stumpwm-29.html), let me introduce yet another of my favorite tools to you: [vimperator](http://www.vimperator.org/vimperator). Vimperator is essentially a [firefox](http://www.mozilla.org/en-US/) plugin, but it is so awesome that it takes web browsing to a whole different level. And I am not exaggerating it at all; allow me to present the case in front of you.</p>

The most basic (but awesome, nonetheless) feature is mouseless browsing. Press the "f" key so that all links on the page get highlighted with a number.</p>

<img alt="Screenshot" src="../img/2015-11-05-153511\_958x1061\_scrot.png" width=600 />

Now you can press the number of the link you want to open, and that link will be opened in the current tab. Instead do the same with "F" and the link will be opened in a new tab. Similarly, the following keys can be used for navigation</p>

* h, j, k, l: moving left, down, up, right (similar to vim) on the page</li>
* gt: switch to next tab</li>
* gT: switch to previous tab</li>
* o: enter URL and open in current tab</li>
* O: edit current URL and open page in current tab</li>
* t: enter URL to open page in a new tab</li>
* T: edit current URL and open page in new tab</li>
* f: find on page</li>

Another feature that I use regularly (atleast 10-20 times in a single day) is dynamic bookmarks. I am sure that online search (google, bing, wikipedia, etc) is an extremely frequent usecase in any persons browsing session. Most browsers provide a dedicated search-bar next to the location bar. And also, this search-bar is customizable, that is the browser provides a dropdown of the various search engines that you want to search on. This is definitely more convenient than first going to the search engine page and then searching; you save 1 step. But:</p>

* see the above image again. Vimperator removes both the location bar and the search bar as well</li>
* more importantly, navigating the mouse to the search bar and optionally changing the search engine is not the best way to do it at all</li>

So how do we solve this problem efficiently using vimperator? This is where dynamic bookmarks come in. Lets take an example of using the google search engine. You need to do this only the 1st time:</p>

* go to google.com and search for "golb.in"</li>
* press "a" to see a "bmark" command at the bottom of the page</li>
* edit the URL to look similar to https://www.google.com/search?q=%s</li>
* leave a space after the URL and enter "-keyword google"</li>
* press enter</li>

And you are done! Now every time you want to search something on google, simply press "t google &amp;lt;your search query&amp;gt;" and you will be taken to the corresponding google search page. You can do similarly with other search engines, and create bookmarks like "bing", "wiki", etc. Heck, this technique can be used on any website that gives you a search functionality. Who needs browser supported search engines anymore? Ain't that cool?</p>

I hope this (and my previous [post](http://www.golb.in/kill-that-rat-28.html) on going mouseless) has convinced you to atleast give vimperator a try. If not, don't worry. I still have a few more, advanced but even more awesome, features of vimperator. I will leave them for the next post ;)</p>

But I won't leave you before telling you that you can reach the locally available help via the ":help" and ":helpall" commands</p>

If you did give vimperator a try, do let me know your experience using it, via comments. And don't feel shy or afraid to ask for help if you find it difficult</p>
