{:title "ml-102: Supervised Learning"
 :layout :post
 :tags  []
 :toc true}

Hi! I hope you enjoyed the last [post](http://www.golb.in/ml-101-introduction-to-machine-learning-33.html) on introduction to ML. Today we will dig just a little bit deeper and understand the various types of ML algorithms. Although not complete, some of the different types of ML algorithms are:

* Supervised learning
* Unsupervised learning
* Recommender systems

The first 2, viz supervised and unsupervised techniques are related to each other and are differentiated based on the input data and the problem statement. If the (training) data contains both the features and the output (value to be found), then algorithms that work on such data are called supervised learning algorithms. Let me explain with the help of an example.

Lets say we have some data about houses like "size in feet-square" and "price". We want our ML algorithm to observe this data and if we give it size data about some new house, then we want it to be able to predict the price for that new house. In this problem, then thing we want to predict (that is the output of the program) is the "price". However, do notice that the training data contains both the "size" feature and the "price" parameter. Hence in this problem, we call the technique as a supervised learning algorithm. To put another way, the training dataset contains "right answers".

Some other examples of supervised learning are datasets like

* [Bike Sharing Dataset Data Set](http://archive.ics.uci.edu/ml/datasets/Bike+Sharing+Dataset): From this dataset, if we want to predict how many bikes would be rented during the next month, then that problem would use a supervised learning ML algorithm
* [Thoracic Surgery Data Data Set](http://archive.ics.uci.edu/ml/datasets/Thoracic+Surgery+Data): Using this dataset we might want to predict whether the post-operative life expectancy of a certain patient

In both of the above examples, the dataset contains the "right answers" for the data provided. Based on this information, our program needs to learn the mapping between the features and the output. Then given a new problem instance (set of feature values), we need to predict the output value.

Supervised learning can be further divided into 2 broad categories based on the problem statement:

* **Regression**: This is the case when the output value to be predicted can take a wide range (mostly continuous) values. For example, in the "house price prediction" problem the predicted value is "price" which can take on a very wide range of values. Similarly, in the "bike sharing" problem, the value to be predicted is "number of bikes rented" which will also have a numerical value
* **Classification**: On the other hand, when the value to be predicted can have a value from within a fixed set of numbers, then it is called as a classification problem. For example, if our objective in the "Thoracic Surgery" dataset above would have been to find whether a patient died within the first year after surgery, then the output can have only 2 valid values "yes" or "no"; thus it would be a classification problem. The values are generally called "class" and it can be 2 or more. For example, in a handwriting recognition dataset, using the english alphabet, we would have 62 classes (A-Z, a-z, 0-9)

That's it for today. In the next post we will look at the remaining 2 ML algorithm types; so stay tuned :)
