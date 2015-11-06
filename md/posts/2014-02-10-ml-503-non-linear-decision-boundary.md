{:title "ml-503: Non Linear Decision Boundary"
 :layout :post
 :tags  []
 :toc true}

Hi there! Welcome back to this series of posts on ML algorithms. In the last [post](http://www.golb.in/ml-502-hypothesis-representation-and-decision-boundary-52.html) we looked at the hypothesis representation and decision boundary concepts in the logistic regression ML algorithm. Today we will look at some more examples of decision boundaries and get a deeper understanding regarding them.

But, let's do a quick review of what we learned last time so that we can continue from there. We defined our hypothesis function as:

> h<sub>&theta;</sub>(x) = g(&theta;' * x)

where,

> g(z) = 1 / (1 + e<sup>-z</sup>)

is the sigmoid function. We also saw an important result that:

> "y = 1" if (&theta;' \*x) &gt;= 0

and

> "y = 0" if (&theta;' \*x) &lt; 0

The decision boundary we saw last time was a simple straight line. But what if our dataset is like below?

![]()

If you remember what we discussed in one of the previous [posts](http://www.golb.in/ml-404-feature-choice-and-polynomial-regression-48.html), then the solution is simple. We should use higher order polynomials. Let us define our hypothesis function as:

> h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub> x1 + &theta;<sub>2</sub> x2 + &theta;<sub>3</sub> x1<sup>2</sup> + &theta;<sub>4</sub> x2<sup>2</sup>

And, furthermore, let us say that we have somehow found the correct values for &theta; already as:

> &theta; = [-1 0 0 1 1]'

I know that we have not yet looked at how to find the optimal values of &theta; for logistic regression. But fear not, we will get there.

Coming back to the problem at hand. When we use the above &theta;, we get the following hypothesis function output:

![]()

You see that the decision boundary is now a circle, and

> "y = 1" if x1<sup>2</sup> + x2<sup>2</sup> &gt;= 1

and

> "y = 0" if x1<sup>2</sup> + x2<sup>2</sup> &lt; 1

Similarly, if we take more complex higher order polynomials like,

> h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub> x1 + &theta;<sub>2</sub> x2 + &theta;<sub>3</sub> x1<sup>2</sup> + &theta;<sub>4</sub> x2<sup>2</sup> + &theta;<sub>5</sub> x1x2 + &theta;<sub>5</sub> x1<sup>2</sup> + &hellip;

then we can get even more complex forms of the decision boundary which will help us correctly classify our dataset.

I hope you are with me till here, and are loving reading about these algorithms as much as I am loving writing about them. In the next post we will take a look at the methods to compute the optimal values of &theta;. So keep watching this space!
