{:title "ml-505: Simplified Cost Function and Gradient Descent for Logistic Regression"
 :layout :post
 :tags  []
 :toc true}

Hello, welcome back! In the last [post](http://www.golb.in/ml-504-cost-function-for-logistic-regression-54.html) we defined the cost function for our logistic regression implementation. Today we will simplify it, and also move onto the next stage, viz minimization of the cost function.

As a short recap, in the last [post](http://www.golb.in/ml-504-cost-function-for-logistic-regression-54.html), we defined the cost function as

> cost(h<sub>&theta;</sub>(x), y) = -log(h<sub>&theta;</sub>(x)), if y = 1

> -log(1 = h<sub>&theta;</sub>(x)), if y = 0

The same can be rewritten simply as follows:

> cost(h<sub>&theta;</sub>(x), y) = -y log(h<sub>&theta;</sub>(x)) - (1 - y) log(1 - h<sub>&theta;</sub>(x))

To see how this is the same as the previous one, we need to remember that our output variable "y" can take only 1 of 2 possible values, viz "0" and "1". So let's try to substitute these values in our 2nd equation to see if we can get to the 1st

When "y = 1"

> cost(h<sub>&theta;</sub>(x), y) = -1 log(h<sub>&theta;</sub>(x)) - (1 - 1) log(1 - h<sub>&theta;</sub>(x))

> = -log(h<sub>&theta;</sub>(x)) - 0 * log(1 - h<sub>&theta;</sub>(x))

> = -log(h<sub>&theta;</sub>(x))

Similarly, when "y = 0"

> cost(h<sub>&theta;</sub>(x), y) = -0 * log(h<sub>&theta;</sub>(x)) - (1 - 0) log(1 - h<sub>&theta;</sub>(x))

> = -0 - 1 * log(1 - h<sub>&theta;</sub>(x))

> = -log(1 - h<sub>&theta;</sub>(x))

Combining the above 2 new equations, we get

> cost(h<sub>&theta;</sub>(x), y) = -log(h<sub>&theta;</sub>(x)), when "y = 1"

> = -log(1 - h<sub>&theta;</sub>(x)), when "y = 0"

which is exactly the same as our original cost function as defined in the 1st equation.

Using this new definition, our real cost function J(&theta;) becomes:

> J(&theta;) = -(y log(h<sub>&theta;</sub>(x)) + (1 - y) log(1 - h<sub>&theta;</sub>(x))) / m

With that out of the way, let us move onto the next step, viz minimization. For this, we will use our old friend which was introduced in these earlier posts [here](http://www.golb.in/ml-303-gradient-descent-41.html) and [here](http://www.golb.in/ml-306-multivariate-linear-regression-44.html), viz gradient descent. I hope you remember that the general template for gradient descent is:

> repeat until convergence {

> &theta;<sub>j</sub> = &theta;<sub>j</sub> - &alpha; * &delta;/&delta;&theta;<sub>j</sub> J(&theta;)

> update all &theta;<sub>j</sub> simultaneously

> }

Without going into the mathematical derivation, the partial derivative of J(&theta;) w.r.t &theta;<sub>j</sub> is:

> &delta;/&delta;&theta;<sub>j</sub> J(&theta;) = &Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>) x<sub>j</sub><sup>(i)</sup> / m

With this information, our gradient descent step becomes

> repeat until convergence {

> &theta;<sub>j</sub> = &theta;<sub>j</sub> - &alpha; * &Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>) x<sub>j</sub><sup>(i)</sup> / m

> update all &theta;<sub>j</sub> simultaneously

> }

You might notice that this gradient descent definition is exactly the same as that for linear regression as defined [here](http://www.golb.in/ml-306-multivariate-linear-regression-44.html). Does this mean that both instances of the gradient descent implementations (for linear and logistic regression) are the same? Close inspection will show that this is not the case. That is because the hypothesis function (h<sub>theta</sub>(x)) for linear and logistic are different. Thus the two gradient descent too are different, although they look the same superficially.

Once we have the optimized values of theta, it is trivial to substitute them in the definition for the hypothesis function which can be used for prediction of new values of y, given x. However, do remember, that the hypothesis function for logistic regression is actually a probability function (as mentioned in [this](http://www.golb.in/ml-502-hypothesis-representation-and-decision-boundary-52.html) post). Thus

> hypothesis function = h<sub>&theta;</sub>(x) = p(y = 1|x; &theta;)

> = probability that "y = 1" given "x" and parameterized by "&theta;"

Lastly, we had described a method for verifying that the gradient descent implementation is indeed working correctly and is minimizing the cost function in [this](http://www.golb.in/ml-304-gradient-descent-and-learning-rate-%CE%B1-42.html) post. Although that method was used for linear regression, the exact same method can be used for logistic regression too.

This almost completes the logistic regression part of ML algorithms. The only thing left is to look at cases when y can take a value from a predefined set of values, instead of just 2 values "0" and "1"; that is multi-class classification instead of binary classification. We will look at this last detail in the next post. So stay tuned!
