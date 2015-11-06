{:title "ml-403: Feature Scaling"
 :layout :post
 :tags  []
 :toc true}

Hello. Welcome back! I hope that you are enjoying this series on machine learning, especially the last 2 posts [here](http://www.golb.in/ml-402-multivariate-linear-regression-in-octave-45.html) and [here](http://www.golb.in/ml-203-vectorization-in-octave-46.html) where we implemented the "multivariate linear regression" ML algorithm and even improved its performance. In this post we will look at one more technique which should be applied to the multivariate version of the linear regression ML algorithm to improve its performance, viz "feature scaling". The reason why I say that this technique should be used for the "multivariate" version, is because by using this technique we solve a certain problem from which the "univariate" version does not suffer.

Lets take a concrete example to throw more light on what I am trying to say. For this, let's consider this [data](http://archive.ics.uci.edu/ml/machine-learning-databases/auto-mpg/auto-mpg.data), a small snippet of which is shown below:

<table class="table table-bordered"> <tbody>
<tr> <td> 18.0</td> <td> 8</td> <td> 307.0</td> <td> 130.0</td> <td> 3504.</td> <td> 12.0</td> <td> 70</td> <td> 1</td> <td> "chevrolet chevelle malibu"</td> </tr>
<tr> <td> 15.0</td> <td> 8</td> <td> 350.0</td> <td> 165.0</td> <td> 3693.</td> <td> 11.5</td> <td> 70</td> <td> 1</td> <td> "buick skylark 320"</td> </tr>
<tr> <td> 18.0</td> <td> 8</td> <td> 318.0</td> <td> 150.0</td> <td> 3436.</td> <td> 11.0</td> <td> 70</td> <td> 1</td> <td> "plymouth satellite"</td> </tr>
<tr> <td> 16.0</td> <td> 8</td> <td> 304.0</td> <td> 150.0</td> <td> 3433.</td> <td> 12.0</td> <td> 70</td> <td> 1</td> <td> "amc rebel sst"</td> </tr>
<tr> <td> 17.0</td> <td> 8</td> <td> 302.0</td> <td> 140.0</td> <td> 3449.</td> <td> 10.5</td> <td> 70</td> <td> 1</td> <td> "ford torino"</td> </tr>
<tr> <td> 15.0</td> <td> 8</td> <td> 429.0</td> <td> 198.0</td> <td> 4341.</td> <td> 10.0</td> <td> 70</td> <td> 1</td> <td> "ford galaxie 500"</td> </tr>
<tr> <td> 14.0</td> <td> 8</td> <td> 454.0</td> <td> 220.0</td> <td> 4354.</td> <td> 9.0</td> <td> 70</td> <td> 1</td> <td> "chevrolet impala"</td> </tr>
<tr> <td> 14.0</td> <td> 8</td> <td> 440.0</td> <td> 215.0</td> <td> 4312.</td> <td> 8.5</td> <td> 70</td> <td> 1</td> <td> "plymouth fury iii"</td> </tr>
<tr> <td> 14.0</td> <td> 8</td> <td> 455.0</td> <td> 225.0</td> <td> 4425.</td> <td> 10.0</td> <td> 70</td> <td> 1</td> <td> "pontiac catalina"</td> </tr>
<tr> <td> 15.0</td> <td> 8</td> <td> 390.0</td> <td> 190.0</td> <td> 3850.</td> <td> 8.5</td> <td> 70</td> <td> 1</td> <td> "amc ambassador dpl"</td> </tr>
</tbody> </table>

If you remember, we have seen this dataset earlier [here](http://www.golb.in/ml-301-linear-regression-with-one-variable-38.html). Let's ignore the first column for now, because that is the target variable, so that leaves us with 8 features. We notice that (in our limited dataset snippet):

* 1st feature ranges between 4 and 8 (in the complete dataset)
* 2nd feature ranges between 300 and 500 (approx)
* 3rd feature ranges between 100 and 250 (approx)
* 4th feature ranges between 3400 and 4500 (approx)
* 5th feature ranges between 8 and 12 (approx)
* 6th feature ranges between 70 and 85 (in the complete dataset)
* 7th feature ranges between 1 and 3 (in the complete dataset)
* 8th feature is a string (so we'll ignore it for this discussion)

The reason that we are interested in the "range" of values that our features take is because depending on the relative ranges that the feature variables take the shape of the cost function will differ. And this will impact the performance of our implementation.

I hope that you remember from [this](http://www.golb.in/ml-302-intuition-for-univariate-linear-regression-39.html) and [this](http://www.golb.in/ml-303-gradient-descent-41.html) posts that our cost function "J(&theta;)" always has a convex (like a bowl) shape. When we see a bowl from the top, we see a circle. But for our cost function, it can vary between being circular to an extremely thin [ellipse](http://en.wikipedia.org/wiki/Ellipse). Whether it will be a circle or an ellipse is determined by the relative ranges of the features.

Also, the more circular the shape of our cost function, the better is the performance of the gradient descent implementation. That is because in this case the gradient descent needs much lesser number of steps (iterations) to reach the global optima. As against this, if the shape is narrow, then the cost can oscillate around the major axis of the ellipse and take lot of iterations to reach the global optima.

In order for the shape of our cost function to be as circular as possible, we must modify our input variables such that their ranges are similar. This process is known as "feature-scaling". Although, there are various methods to achieve this, the most commonly used technique is the "mean normalization" and is defined as

> x<sub>j</sub> = (x<sub>j</sub> - m<sub>j</sub>) / s<sub>j</sub>; where

> m<sub>j</sub> = average (or mean) value of x<sub>j</sub>

> s<sub>j</sub> = range (max - min) OR std. deviation of x<sub>j</sub>

> j = j<sup>th</sup> feature

By implementing the above on all our input variables, we make the data of the form

> -1 <= X(i, j) <= 1

One thing to note though is that we need not follow the above rule very religiously; approximate values are ok too. For example,

> -1 <= X(:, 1) <= 1           % 1st feature

> 5 <= X(:, 2) <= 10           % 2nd feature

> -100 <= X(:3) <= -50         % 3rd feature

is fine. But the below is not

> -1 <= X(:, 1) <= 1           % 1st feature

> 5 <= X(:, 2) <= <b>1000</b>         % 2nd feature

> -100 <= X(:3) <= -50         % 3rd feature

Of course, even with the above data the implementation will work, but it might take a very long time to converge.

Another very important thing to remember is that we should <b>not</b> scale the pivot feature x<sub>0</sub>.

I think that's it for today. In the upcoming posts we will study other ML algorithms and also understand which to use when. So stay tuned!
