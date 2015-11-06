{:title "ml-501: Logistic Regression"
 :layout :post
 :tags  []
 :toc true}

Hello :) I have a good news today! If you have not noticed, we have moved from the 40x series into the 50x series of ML posts today. Yay! This means that we will start learning a new section, or type of ML algorithms. But wait, isn't that logistic "regression" there in the title? Haven't we been learning regression algorithms already in the 40x series [here](http://www.golb.in/ml-306-multivariate-linear-regression-44.html), [here](http://www.golb.in/ml-402-multivariate-linear-regression-in-octave-45.html), [here](http://www.golb.in/ml-403-feature-scaling-47.html), [here](http://www.golb.in/ml-404-feature-choice-and-polynomial-regression-48.html), [here](http://www.golb.in/ml-405-normal-equation-part-1-49.html) and [here](http://www.golb.in/ml-406-normal-equation-part-2-50.html). The reason this is so is because we will look at a different type of ML problem, viz "classification" in this 50x series, but for historical reasons these algorithms are called logistic regression. Note the "logistic" part, which means "logical", or "classes". Ready to start? Here we go!

Today we will be learning the "classification" type of ML problem, where the output variable "y" is a set of "discrete" values. If you remember, we had given a brief introduction to these problems in this 10x introductory [post](http://www.golb.in/ml-102-supervised-learning-34.html). But now, let's take a deeper look using some examples:

* email spam: In the email spam classification, we have a spam classifier ML implementation which, given a text of email, classifies it as either "yes" (spam), or "no" (not-spam)
* online transactions: In this case, the problem statement is to classify a particular online transaction as either "fraudulent" or "not-fraudulent"
* tumor: In this problem, the ML implementation should tell whether a given tumor is "benign" (not-harmful), or malignant (harmful)

In all of the above cases, the output variable "y" can take one of 2 values, "yes" or "no". Traditionally, this has been represented as "class-1" (presence of something), or "class-0" (absence of something), but this assignment is mostly arbitrary. Also, in the above cases, there are only 2 values, and hence the classification is also known as a binary-class classification; whereas when there are more than 2 values, then the algorithm is known as a multi-class classification.

Since this is the first post in the "classification" domain, we will keep it simple and look at only the binary-class classification type of problems today. So let's move onto the problem statement for today's example.

![]()

In this example:

* X: tumor size
* y: 1 (malignant), 0 (benign)

That is, given just the tumor size, we need to predict whether the tumor is malignant or benign. The sample data looks like shown above. Notice that all data points are either at "y = 0", or "y = 1", signifying that this is a classification problem.

![]()

Let's say that, since we have not learnt the logistic regression ML algorithm yet, we will apply the linear regression ML algorithm, that we already know, and see how it performs. After running linear regression, we get our hypothesis line as shown in the above figure. In this case, if we define a threshold as:

> if h<sub>&theta;</sub>(x) &gt;= 0.5, predict "y = 1"

> if h<sub>&theta;</sub>(x) &lt; 0.5, predict "y = 0"

then it looks like our linear regression implementation has done a pretty good job of classifying the benign and malignant examples correctly, and is in fact working as a logistic regression algorithm.

![]()

However, if we get another data point, an outlier actually, then we get a different hypothesis function as shown in the above figure. But this time, we see that our new hypothesis function performs terribly on the data, and is in fact mis-classifying the malignant examples as benign. What really happened is that the first time, our linear regression implementation turned out to be lucky. In general, the linear regression does not work well for classification problems.

In the next post we will look at the linear regression algorithm itself and how it is used to solve a classification ML problem. So stay tuned!
