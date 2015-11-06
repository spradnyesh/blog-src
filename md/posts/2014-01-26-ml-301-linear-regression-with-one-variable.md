{:title "ml-301: Linear Regression with one variable"
 :layout :post
 :tags  []
 :toc true}

Welcome back! After having gone through some posts on introduction to ML ([here](http://www.golb.in/ml-101-introduction-to-machine-learning-33.html), [here](http://www.golb.in/ml-102-supervised-learning-34.html), [here](http://www.golb.in/ml-103-unsupervised-learning-and-recommender-systems-35.html), [here](http://www.golb.in/ml-201-octave-1-36.html) and [here](http://www.golb.in/ml-202-octave-2-37.html)), lets now start learning a real ML algorithm. The algorithm that we will study today is a [supervised learning](http://www.golb.in/ml-102-supervised-learning-34.html) regression algorithm.

First lets define the problem statement. Today we will use a subset of [this](http://archive.ics.uci.edu/ml/datasets/Auto+MPG) [data](http://archive.ics.uci.edu/ml/machine-learning-databases/auto-mpg/auto-mpg.data). The first few training examples in the data are:

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
<tr> <td> 15.0</td> <td> 8</td> <td> 383.0</td> <td> 170.0</td> <td> 3563.</td> <td> 10.0</td> <td> 70</td> <td> 1</td> <td> "dodge challenger se"</td> </tr>
<tr> <td> 14.0</td> <td> 8</td> <td> 340.0</td> <td> 160.0</td> <td> 3609.</td> <td> 8.0</td> <td> 70</td> <td> 1</td> <td> "plymouth 'cuda 340"</td> </tr>
<tr> <td> 15.0</td> <td> 8</td> <td> 400.0</td> <td> 150.0</td> <td> 3761.</td> <td> 9.5</td> <td> 70</td> <td> 1</td> <td> "chevrolet monte carlo"</td> </tr>
<tr> <td> 14.0</td> <td> 8</td> <td> 455.0</td> <td> 225.0</td> <td> 3086.</td> <td> 10.0</td> <td> 70</td> <td> 1</td> <td> "buick estate wagon (sw)"</td> </tr>
<tr> <td> 24.0</td> <td> 4</td> <td> 113.0</td> <td> 95.00</td> <td> 2372.</td> <td> 15.0</td> <td> 70</td> <td> 3</td> <td> "toyota corona mark ii"</td> </tr>
<tr> <td> 22.0</td> <td> 6</td> <td> 198.0</td> <td> 95.00</td> <td> 2833.</td> <td> 15.5</td> <td> 70</td> <td> 1</td> <td> "plymouth duster"</td> </tr>
<tr> <td> 18.0</td> <td> 6</td> <td> 199.0</td> <td> 97.00</td> <td> 2774.</td> <td> 15.5</td> <td> 70</td> <td> 1</td> <td> "amc hornet"</td> </tr>
</tbody> </table>

In this data, the 1st column is the "mpg" target variable, or the parameter that we have to predict, while the rest of the columns are the features or input variables. But today we will go simple and will use only 1 input variable, that is the 3rd column "displacement". To keep the algorithm simple, we will assume that our target variable "mpg" is someway dependent or related to only "displacement", our input variable.

So now the first 10 training examples look like (notice that I have swapped the order of the data Note that the first column is x (input variable(s)), and second column is y (target variable))

<table class="table table-bordered"> <tbody>
<tr> <td> x</td> <td> y</td> </tr> <tr> <td> 307.0</td> <td> 18.0</td> </tr>
<tr> <td> 350.0</td> <td> 15.0</td> </tr> <tr> <td> 318.0</td> <td> 18.0</td> </tr>
<tr> <td> 304.0</td> <td> 16.0</td> </tr> <tr> <td> 302.0</td> <td> 17.0</td> </tr>
<tr> <td> 429.0</td> <td> 15.0</td> </tr> <tr> <td> 454.0</td> <td> 14.0</td> </tr>
<tr> <td> 440.0</td> <td> 14.0</td> </tr> <tr> <td> 455.0</td> <td> 14.0</td> </tr>
<tr> <td> 390.0</td> <td> 15.0</td> </tr>
</tbody> </table>

Thus the problem definition is given a new "displacement" (x), we need to predict the value for "mpg" (y). To do this we need to a function "h" that maps the input "x" to the output "y". In ML world, this function "h" is called the hypothesis function, and is represented as

> h<sub>&Theta;</sub>(x) = &Theta;<sub>0</sub> + &Theta;<sub>1</sub> x</blockquote>

In the above example "h" is also called 'univariate linear regression', because we are using only 1 variable (or feature).

Before we move ahead, lets get some terminology noted

* m => #examples
* x => input variable/feature
* y => output variable/target
* x<sup>(i)</sup>, y<sup>(i)</sup> => i<sup>th</sup> training example, so for example, in the above data, x<sup>(1)</sup> = 307.0, x<sup>(5)</sup> = 302.0, y<sup>(7)</sup> = 14.0

What we need to do next is to chose &Theta;<sub>0</sub> and &Theta;<sub>1</sub> so that h<sub>&Theta;</sub>(x) is as close to y for our training examples (x, y). I hope you understand why we are doing this. This is because, if the hypothesis function that we find out (as the end goal of our ML problem) is perfect, then the value of h<sub>&Theta;</sub>(x<sup>(i)</sup>) should be exactly equal to the corresponding y<sup>(i)</sup>, for any example i.

So, obviously, our goal would be to do the following

> minimize<sub>(&Theta;<sub>0</sub>,&Theta;<sub>1</sub>)</sub> (&Sigma;<sub>i</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)</blockquote>

The division by 2m is simply taking an average of the squared error and is done to make later math easier. This function is called the cost function J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>), and also called squared error function, or squared error cost function. This is the most most commonly used error function in ML world.

By implementing the above we would find the optimum values of &Theta;<sub>0</sub> and &Theta;<sub>1</sub> that will minimize our cost function J. Then all we need to do is to insert these &Theta;<sub>0</sub> and &Theta;<sub>1</sub> values into our hypothesis function h<sub>&Theta;</sub>(x) and our ML problem is solved. Then given any new value for x, we can simply put that x in the hypothesis function to get the y.

Ain't that cool? We have already started solving ML problems and making predictions!

Well, not so fast stud ;) We still have to figure out how to perform the last step of the puzzle, viz "minimize", don't we? But I think this much study is good for today, and we will jump to the minimization problem in the next post. So keep watching this space :)
