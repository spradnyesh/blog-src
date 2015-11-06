{:title "ml-103: Unsupervised learning and Recommender systems"
 :layout :post
 :tags  []
 :toc true}

Hello :) In the last 2 posts [here](http://www.golb.in/ml-101-introduction-to-machine-learning-33.html) and <a target="_blank"href="http://www.golb.in/ml-102-supervised-learning-34.html">here</a>, we got a general overview of what Machine learning is and also looked at a particular category ML algorithms, viz the "supervised learning" type.

Today we will briefly look at 2 more types of ML algorithms, viz the "unsupervised learning" and "recommender systems". I hope you remember that in the supervised learning types of ML algorithms, we get the "right answers" embedded in the training data. As against this, in the "unsupervised learning" algorithms, we do **not** get the right answers in the training data. In fact sometimes, there is no right answer at all, as I will show below.

The above explanation seems to be very vague, so lets dig deeper with the help of an example.

<iframe allowfullscreen="" frameborder="0" height="461" mozallowfullscreen="" msallowfullscreen="" oallowfullscreen="" src="https://www.flickr.com/photos/giladlotan/5151742603/player/0c0134107b" webkitallowfullscreen="" width="500"></iframe>

The above image is a snippet of the facebook social graph; it's a graph of how a user is connected to other users. It also shows clusters of users; groups of users who are very strongly/closely connected to each other. In such a dataset, as you would rightly guess, there is no "right answer". Basically the objective is to find this cluster/closeness attribute.

Similarly, if you see [this](http://archive.ics.uci.edu/ml/datasets/3D+Road+Network+(North+Jutland,+Denmark)) dataset, it's about the road network in North Jutland, Denmark in 3d (longitude, latitude, altitude). If the dataset is used to find information/knowledge which will be used to perform accurate routing for eco-routing, cyclist routes, etc, then there is no right answer which is present inside the dataset. The task is for the program to learn the structure of the data itself and find out interesting knowledge from it.

Some other examples of unsupervised learning are:

* google news: it puts similar news, from various channels/websites, into similar (correct) sections
* organizing computer clusters in a data-center: based on network activity between them, for example
* market segmentation
* social network analysis
* astronomical data analysis
* etc

Lets move on to the next type of ML algorithm, which is "recommender systems". The easiest way to imagine this algorithm is to understand an example that we have all experienced at some time or the other &amp;ndash; e-commerce websites. I am sure you all would have noticed that when we buy something online, we are recommended other objects, for which there is a higher probability of us buying; for example, books from same author or on same topic, or movies from same genre, etc.

In ML, there are certain ways in which these systems are implemented. But don't you worry. We will be looking into all of these algorithms in much more depth in the forthcoming posts. So keep tuned :)
