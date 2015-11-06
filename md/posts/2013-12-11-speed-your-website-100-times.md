{:title "Speed up your website 100x"
 :layout :post
 :tags  []
 :toc true}

If you remember, we had mentioned in one of our recent posts that we increased the speed of our editorial site by 100 times. That's right, 100 times! So what is the secret? How did we do it? Well, actually there's the short answer and the long answer.

For all you impatient folks out there, the short answer first: We put extremely long processes (like sending email) into the background and returned the page without waiting for its result!

However, in reality things are not so simple. As [Donald Knuth](http://www-cs-faculty.stanford.edu/~knuth/) put it:

> Premature optimization is the root of all evil

So we did what was correct: measure. We performed the following steps:

* measure page speed (as perceived by end users) using tools like [yslow](http://yslow.org/)], [pagespeed](https://developers.google.com/speed/pagespeed/)], etc
* figure out which requests are taking time
* split the above requests into frontend (network and client-side) and backend (server-side) categories (explanation of these categories is for another post ;). for now, lets concentrate only on backend issues)
* during our measurements, we found that the article create/update page was the slowest
* this was mainly due to activities like sending emails and submitting pages to web-archive.com took the most times. but, we realized that the user need not wait for these activities to finish. thus, by simply putting these activities into a separate thread (and not waiting for the thread to finish execution), we were able to bring down the page load time from 3 seconds to about 30 milliseconds; a whopping gain of 100x

The lessons that we learned from the above exercise were

* don't do premature optimization
* measure before starting to optimize
* go for the low hanging fruits (find the thing that will give the maximum ROI)
* don't optimize parts that will not have any impact (for eg, improving the performance of some rarely called function from 5ms to 4ms by spending 2 hours is pretty much useless)

We would like to hear about your optimization experiences!
