{:title "ml-504: Cost Function and Logistic Regression"
 :layout :post
 :tags  []
 :toc true}

Hello. In the previous few posts ([here](http://www.golb.in/ml-501-logistic-regression-51.html), [here](http://www.golb.in/ml-502-hypothesis-representation-and-decision-boundary-52.html) and [here](http://www.golb.in/ml-503-non-linear-decision-boundary-53.html) we learned about linear regression and also formulated its hypothesis function using the sigmoid function so that the output variable "y" always is either 0 or 1. Today we will move onto the next stage and learn about the cost function that shall be used in the logistic regression ML problem.

In [post](http://www.golb.in/ml-502-hypothesis-representation-and-decision-boundary-52.html) we defined our hypothesis function as

> h<sub>&theta;</sub>(x) = g(&theta;' * x) = 1 / (1 + e<sup>-(&theta;' * x)</sup>)

Also, in [post](http://www.golb.in/ml-301-linear-regression-with-one-variable-38.html), we had defined the cost function for linear regression as:

> J(&theta;) = (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)

Let's re-write it as:

> J(&theta;) = (&Sigma;<sub>i=1</sub><sup>m</sup> ((h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>) / 2) / m

or

> J(&theta;) = cost(h<sub>&theta;</sub>(x<sup>(i)</sup>), y<sup>(i)</sup>) / m

that is

> cost(h<sub>&theta;</sub>(x<sup>(i)</sup>), y<sup>(i)</sup>) = (&Sigma;<sub>i=1</sub><sup>m</sup> ((h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>) / 2)

But this cost-function is non-convex :( (unlike that of linear regression (see [post](http://www.golb.in/ml-302-intuition-for-univariate-linear-regression-39.html))). This is because the squared cost of sigmoid function is non-linear (remember that our hypothesis function is the sigmoid of (&theta;' * x)). Due to this finding the optimal (global) minimum is (mostly, unless by luck) impossible. Hence we need to define a new cost-function for our logistic regression problem.

Let us define the new cost-function as follows:

> cost(h<sub>&theta;</sub>(x), y) = -log(h<sub>&theta;</sub>(x)), if "y = 1"

> -log(1 = h<sub>&theta;</sub>(x)), if "y = 0"

Now we need to prove that the above cost-function is convex. To do this let us first consider the case when "y = 1"

![]()

The above graph is a plot for the function "-log(h<sub>&theta;</sub>(x))". As can bee seen from this graph, our newly defined cost function has interesting and desirable properties:

* for true-positive (hypothesis predicts y = 1, and really y = 1), then cost = 0
* but false-negative (hypothesis predicts y = 0, but really y = 1), then cost grows to infinity

Now see what happens when "y = 0"

![]()

The above graph is a plot for the function "-log(1 - h<sub>&theta;</sub>(x))". Similar to the previous graph, we have some interesting and desirable properties here too:

* for true-negative (hypothesis predicts y = 0, and really y = 0), then cost = 0
* but false-positive (hypothesis predicts y = 1, but really y = 0), then cost grows to infinity

These properties are good because when our implementation is working as expected the cost (error) is 0, but when it is not, then it gets penalized heavily. When, in later stages, we apply minimization algorithms to this cost function, we are sure it will work in the right direction and produce the correct values of &theta;. From there, we will follow the standards steps of defining the hypothesis function which will be used to predict "y" given "x".

Coming back to the point, our real cost function "J(&theta;)" will now be defined as

> J(&theta;) = cost(h<sub>&theta;</sub>(x<sup>(i)</sup>), y<sup>(i)</sup>) / m

where

> cost(h<sub>&theta;</sub>(x), y) = -log(h<sub>&theta;</sub>(x)), if "y = 1"

> -log(1 = h<sub>&theta;</sub>(x)), if "y = 0"

Keep watching this space until next time when we will move onto the next stage of the logistic regression ML algorithm and learn about minimization techniques for our new cost function!
