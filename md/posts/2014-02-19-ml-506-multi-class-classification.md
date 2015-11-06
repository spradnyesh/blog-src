{:title "ml-506: Multi-class Classification"
 :layout :post
 :tags  []
 :toc true}

Hello and welcome back! Previously, we have discussed the various aspects in much detail in these posts [here](http://www.golb.in/ml-501-logistic-regression-51.html), [here](http://www.golb.in/ml-502-hypothesis-representation-and-decision-boundary-52.html), [here](http://www.golb.in/ml-503-non-linear-decision-boundary-53.html), [here](http://www.golb.in/ml-504-cost-function-for-logistic-regression-54.html) and [here](http://www.golb.in/ml-505-simplified-cost-function-and-gradient-descent-for-logistic-regression-55.html). Today we will look at the final topic in classification ML algorithms, viz multi-class classification.

Before starting with the actual algorithm, let us first take a look at some examples of multi-classes to ensure that our understanding about them is correct:

* email foldering/tagging: work (y = 1), friends (y = 2), family (y = 3), hobby (y = 4)
* medical diagnosis: not ill (y = 1), cold (y = 2), flu (y = 3)
* weather: sunny (y = 1), cloudy (y = 2), rain (y = 3), snow (y = 4)

![]()

In all of the above examples, the output variable "y" takes on values from a discrete set (size greater than 2), instead of just "0" and "1" (as in binary classification). This is the problem statement multi-class classification. Note that it does not matter whether the class index starts from 0 or 1.

The technique that is used to solve multi-class classification problems is known as the "one vs all" (or "one vs rest") algorithm. Let us say that our multi-class classification problem has "k" classes (where, k &gt; 2). Then, in "one vs all" classification technique, we take only one class at a time and combine all the other classes into a single class; thus turning the k-class classification problem into k binary classification problems as shown in below graphs

![]()

![]()

![]()

Then we will get k hypothesis functions as below:

> h<sub>&theta;</sub><sup>(i)</sup>(x) = p(y = i|x; &theta;), where i = 1, 2, &hellip;, k

The actual prediction (finding y) is done as follows:

> y = i, where class i is one that maximizes h<sub>&theta;</sub><sup>(i)</sup>(x)

This completes our [50x](http://www.golb.in/tag/50x/) series of ML algorithms which dealt with the topic of classification or logistic regression. I hope you have been following me till now and have enjoyed reading and learning as much as I have writing it and learning from it too :) Do share your thoughts on how I can improve this series further by leaving comments below.

From the next time we will move onto more complex topics and delve much deeper into the realm of ML algorithms. So do come back and enjoy :)
