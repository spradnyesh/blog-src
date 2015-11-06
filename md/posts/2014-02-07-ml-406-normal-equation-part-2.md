{:title "ml-406: Normal Equation -- part - 2"
 :layout :post
 :tags  []
 :toc true}

Hello there! Welcome back. In the last [post](http://www.golb.in/ml-405-normal-equation-part-1-49.html) we took a look at another algorithm, viz "normal equation" to solve the linear regression ML problem. However that was, maybe, too theoretical in nature. Today we will take a concrete example and see how to implement the solution for the same in octave. Are you ready? If so, lets move on&hellip;

The concrete example for today is as follows (including the pivot feature x<sub>0</sub>):

<table class="table table-bordered"> <tbody>
<tr><td></td><td>size(feet<sup>2</sup>)</td><td>#bedrooms</td><td>#floors</td><td>age (years)</td><td>price($1000)</td></tr>
<tr><td>x<sub>0</sub></td><td>x<sub>1</sub></td><td>x<sub>2</sub></td><td>x<sub>3</sub></td><td>x<sub>4</sub></td><td>y</td></tr>
<tr><td>1</td><td>2104</td><td>5</td><td>1</td><td>45</td><td>460</td></tr>
<tr><td>1</td><td>1416</td><td>3</td><td>2</td><td>40</td><td>232</td></tr>
<tr><td>1</td><td>1534</td><td>3</td><td>2</td><td>30</td><td>315</td></tr>
<tr><td>1</td><td>852</td><td>2</td><td>1</td><td>36</td><td>178</td></tr>
</tbody> </table>

In matrix forms, it gives rise to the following X (of size mx(n+1)):

<table class="table table-bordered"> <tbody>
<tr><td>1</td><td>2104</td><td>5</td><td>1</td><td>45</td></tr>
<tr><td>1</td><td>1416</td><td>3</td><td>2</td><td>40</td></tr>
<tr><td>1</td><td>1534</td><td>3</td><td>2</td><td>30</td></tr>
<tr><td>1</td><td>852</td><td>2</td><td>1</td><td>36</td></tr>
</tbody> </table>

and y (of size mx1):

<table class="table table-bordered"> <tbody>
<tr><td>460</td></tr>
<tr><td>232</td></tr>
<tr><td>315</td></tr>
<tr><td>178</td></tr>
</tbody> </table>

If that is the case, then by implementing matrix algebra, theta can be solved as:

> theta = (X<sup>T</sup> * X)<sup>-1</sup> * X<sup>T</sup> * y;

In octave, the command to solve the above is

> theta = pinv(X' * X) * X' * y;

That's it! Ain't it cool how such a complex concept can be expressed in just 1 line-of-code in a high level language like octave? Hence, as I had mentioned [here](http://www.golb.in/ml-201-octave-1-36.html), it is extremely important (and useful) to first write solutions for any ML problem in a high level language (like octave, matlab, python, etc) and only when we are sure that we have the right solution, to port them to other faster languages if need be.

Coming back to our problem at hand. Aren't you wondering that if it is so simple to solve for the values of theta, then why did we learn the "gradient descent" algorithm in the first place? Well, obviously, because there are scenarios where the normal equation method does not work. To understand this, lets compare the 2 methods, viz gradient descent and normal equation, and see their relative advantages and disadvantages.

Lets look at the advantages of normal equation method over gradient descent:

* there is no need to do feature scaling
* there is no need to choose the learning rate "&alpha;"
* there is no need iterate

Now lets look at scenarios where normal equation method does not work:

* when the number of features (n) is very large, then the cost to compute the inverse of the nxn matrix (X<sup>T</sup> * X), is extremely large (order of O(n<sup>3</sup>)). On modern computers, for n < 10000, the implementation will work (speed will decrease as n increases), but for values of n above 10000, the processing might never complete.

Although, at this stage of our study, n of the order of 10000 looks extremely big, do note that:

* in real world problems, it is possible to have these many (and more) features
* when you consider the "polynomial regression" algorithm from [this](http://www.golb.in/ml-404-feature-choice-and-polynomial-regression-48.html) post, one can easily see how n can grow very fast

Finally, there is 1 more special case when the normal equation algorithm might get stuck. This is when the matrix (X<sup>T</sup> * X) is non-invertible, that it does not have an inverse. This should happen in only the following 2 cases:

* some features x<sub>i</sub> and x<sub>j</sub> are linearly dependent on each other (for example, x<sub>1</sub> = size in feet, and x<sub>2</sub> = size in meters). in such a case we need to find out such features and remove one of them
* \#training-examples (m) <= #features (n). that is, there is not enough data to fit all features and find the optimal theta. in this case we need to
* either reduce features
* or add more data

Both the above situations are easily avoidable, which leaves us with the only limitation of "n < 10000", thus making the normal equation algorithm a very attractive choice while solving linear regression ML problems.

This also brings us to the end of the 40x series. In the next post we will start looking at other ML problems and algorithms to solve them. So don't go away. Keep watching this space :)
