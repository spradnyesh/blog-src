{:title "ml-404: Feature Choice and Polynomial Regression"
 :layout :post
 :tags  []
 :toc true}

Hi. It's good to see you once more. Today we will learn a particular technique to choose features that might improve the performance (in terms of prediction accuracy) of the regression algorithm, and in turn look at a subset type of regression that results from it.

In one of the initial [posts](http://www.golb.in/ml-301-linear-regression-with-one-variable-38.html)&nbsp;when we started learning the linear regression ML algorithm, we had used the following data

<table class="table table-bordered"> <tbody>
<tr> <td> size in ft<sup>2</sup> (x)</td> <td> price ($) in 1000's (y)</td> </tr>
<tr> <td> 2104</td> <td> 460</td> </tr>
<tr> <td> 1416</td> <td> 232</td> </tr>
<tr> <td> 1534</td> <td> 315</td> </tr>
<tr> <td> 852</td> <td> 178</td> </tr>
<tr> <td> &hellip;</td> <td> &hellip;</td> </tr>
</tbody> </table>

and called our problem as the "housing prediction" problem. This particular problem is the "univariate" type of linear regression because we have only 1 input feature, viz the size of the house in sq-ft.

However, it is very easy to assume that we might have got our input features in the form of "length" and "depth", that is as x<sub>1</sub> and x<sub>2</sub> instead. But, maybe, we had some background domain knowledge to know that the price of the house is _more_ dependent on the area (length * depth), instead of the individual features of length and depth themselves. So in this case, it's like we created a new feature x<sub>3</sub>

> x<sub>3</sub> = x<sub>1</sub> * x<sub>2</sub>;

and used it in place of x<sub>1</sub> and x<sub>2</sub>. Maybe, we also knew, due to domain knowledge, that given the area (x<sub>3</sub>), the features of length (x<sub>1</sub>) and depth (x<sub>2</sub>) do not play any significant role in the prediction of the price (y), and hence can be dropped; thus making y dependent only on x<sub>3</sub>.

The point to note here is that x<sub>3</sub> is no longer a simple variable/feature, but in fact is the product of 2 (x<sub>1</sub> and x<sub>2</sub>) simpler features. Thus, while the graph of x<sub>1</sub> versus y might have been linear, the graph of x<sub>3</sub> versus y would appear to have a quadratic shape (having some sort of a curved nature).

Similar effect (in terms of the graph plot) would appear if we would have used a polynomial power of the base variable itself. For example, if

> y = x<sub>1</sub> ^ 2;

or

> y = x<sub>2</sub> ^ 3;

etc, would give the curve of the input versus output variable a different shape.

![]()

![]()

![]()

Looking at the plots of your input versus output variable, you might get an idea a polynomial feature might be needed. In such cases, armed with some domain knowledge, if one can play with choosing the power of the input feature variables, it is possible to radically improve the performance (in terms of prediction accuracy, not speed) of our implementation.

Since, in these cases, we use a polynomial power of our input variable(s), these algorithms are also known as "polynomial regression" type of ML algorithms. Of course, if one has domain knowledge and already knows some relationship (although not exactly) between the input and output variables, then it can be extremely helpful.

In future posts we will take a look at some advanced algorithms which can automatically find out such relationships, and other algorithms which can automatically choose only those features which improve the performance of the implementation significantly and drop the others. So keep watching this space to learn about them :)
