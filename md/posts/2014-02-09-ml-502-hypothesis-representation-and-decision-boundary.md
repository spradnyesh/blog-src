{:title "ml-502: Hypothesis Representation and Decision Boundary"
 :layout :post
 :tags  []
 :toc true}

<p>Hello! In the last [post](http://www.golb.in/ml-501-logistic-regression-51.html) we took an initial swing at a new type of ML problem, viz classification. We also looked at how the ML linear regression algorithm fails to work for this type of problem, and saw that there is another ML algorithm, logistic regression, that is used to solve them. Today we will do a deeper dive into various concepts surrounding the logistic regression ML algorithm.

We saw in the last [post](http://www.golb.in/ml-501-logistic-regression-51.html) that we want:

> 0 &lt;= h<sub>&theta;</sub>(x) &lt;= 1

In linear regression, we know that:

> h<sub>&theta;</sub>(x) = &theta;' * x

In logistic regression, we will define:

> h<sub>&theta;</sub>(x) = g(&theta;' * x)

where,

> g(z) = 1 / (1 + e<sup>-z</sup>)

g(z) is called the logistic or sigmoid function (hence the name "logistic" regression for this algorithm). The graph (z v/s g(z)) of the sigmoid function looks like:

![]() 

As you might notice, the sigmoid function has this interesting that it asymptotes at 0 as g(z) nears -infinity, and asymptotes at 1 as g(z) nears +infinity. This property makes this function extremely useful in our logistic regression implementation. Also, notice in the above graph that

> g(z) &gt;= 0.5 when z &gt;= 0

and

> g(z) &lt; 0.5 when z &lt; 0

that is

> h<sub>&theta;</sub>(x) = g(&theta;' * x) &gt;= 0.5, whenever (&theta;' * x) &gt;= 0

and

> h<sub>&theta;</sub>(x) = g(&theta;' * x) &lt; 0.5, whenever (&theta;' * x) &lt; 0

We would define our threshold such that

> y = 1 if h<sub>&theta;</sub>(x) &gt;= 0.5

and

> y = 0 if h<sub>&theta;</sub>(x) &lt; 0.5

Combining the above 2 we get

> "y = 1" if (&theta;' \*x) &gt;= 0

and

> "y = 0" if (&theta;' \*x) &lt; 0

Remember this condition, because it will be used when we try to understand the next important concept of "decision boundary".

Anyways, coming back to our hypothesis function, it becomes:

> h<sub>&theta;</sub>(x) = 1 / (1 + e<sup>-(&theta;' * x)</sup>)

This might seem confusing to understand, so let's try to put it in simpler terms. The meaning of the output of hypothesis function is "estimated probability that 'y = 1' on input 'x'". For example, if

> x = [x<sub>0</sub> x<sub>1]'</sub> = [1 tumorSize]'

and if, for this x

> h<sub>&theta;</sub>(x) = 0.7

then, it means that the probability that the tumor is malignant is 70%. Mathematically, it is written as

> h<sub>&theta;</sub>(x) = P(y = 1 | x; &theta;)

and is read is "probability that 'y = 1', given 'x', parameterized by '&theta;'". Conversely, probability for 'y = 0' is

> P(y = 0 | x; &theta;) = 1 - P(y = 1 | x; &theta;)

Next, let's look at another important concept called the "decision boundary". To explain this let us consider the following dataset:

![]() 

Let us also define our hypothesis function as

> h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub> x<sub>1</sub>, &theta;<sub>2</sub> x<sub>2</sub>

and assume that we have somehow found the values of &theta; already as:

> &theta; = [-4 1 1]'

So our hypothesis function becomes (based on our previously noted equation above) to predict:

> "y = 1" if -4 + x1 + x2 &gt;= 0

or

> "y = 1" if x1 + x2 &gt;= 4

Similarly,

> "y = 0" if x1 + x2 &lt; 4

![]() 

The line in the above graph that separates the 2 binary classes "y = 1" and "y = 0" is called the decision boundary. It is extremely important to note that the decision boundary is the property of the hypothesis function and is parameterized by &theta;, and is not dependent on the dataset.

I think it has been a bit heavy today, so let's stop here. In the next post, we will take a look at some other, more interesting, decision boundaries and understand more about them. So stay tuned!
