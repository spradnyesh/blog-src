{:title "ml-302: Intuition for Linear Regression"
 :layout :post
 :tags  []
 :toc true}

Hello! Welcome back. Last time we studied the "univariate linear regression" ML algorithm [here](http://www.golb.in/ml-301-linear-regression-with-one-variable-38.html). That time we took in a lot of new concepts, and not everything might be clear to all. So today we will dig a bit deeper into the various components and try to understand how and why they work correctly. This will help us analyze if our implementation is working correctly and also to debug things if it is not.

So lets begin with a quick review. First, the terminology

* m => #examples
* x => input variable/feature
* y => output variable/target
* x<sup>(i)</sup>, y<sup>(i)</sup> => i<sup>th</sup> training example
* h<sub>&Theta;</sub>(x) = &Theta;<sub>0</sub> + &Theta;<sub>1</sub> x => hypothesis function; it maps from 'x' to 'y'
* J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) = (&Sigma;<sub>i</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m) => cost function; it is a function of &Theta; (not 'x')

The algorithm flow is:

* define the hypothesis function (univariate for now)
* find optimal values for &Theta;<sub>0</sub> and &Theta;<sub>1</sub> by minimizing cost function
* substitute &Theta;<sub>0</sub> and &Theta;<sub>1</sub> in h, to find the hypothesis function
* now using this hypothesis function, we can predict value of 'y' for any given 'x'
I remember that we have still not figured out how to do the minimization step, but we will get there, don't worry :) Today we will look in detail at the first few steps to improve our understanding of them to such an extent so as to

* ensure that our implementation is correct
* fix it if it is not

So lets begin! To keep things simple, and our explanation easier to understand, lets assume that &Theta;<sub>0</sub> = 0, so that:

* h<sub>&Theta;</sub>(x) = &Theta;<sub>1</sub> x
* J(&Theta;<sub>1</sub>) = (&Sigma;<sub>i</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)

If we take the following data

```
x = [0:10]
```

and plot the following data

```
hold on
plot(x, x * 2)
plot(x, x * 3)
plot(x, x * 4)
hold off
```

![]()

that is, we take different values of &Theta;<sub>1</sub> (2, 3 and 4 respectively), then we see that we get 3 different lines. All of them pass through the origin (because &Theta;<sub>0</sub> = 0), but have different angles. This means that our variable &Theta;<sub>1</sub> defines the angle (or slope) of our line. Also note that this line is the representation of our hypothesis function. It is a straight line because we our hypothesis function is a function of a single variable (x); it is "univariate" linear regression.

Lets move on to our cost function J. As before, visualization will help us understand it better. But to get there, we should first define some data. So lets borrow the data from the last [post](http://www.golb.in/ml-301-linear-regression-with-one-variable-38.html)

<table class="table table-bordered"> <tbody>
<tr> <td> x</td> <td> y</td> </tr>
<tr> <td> 307.0</td> <td> 18.0</td> </tr>
<tr> <td> 350.0</td> <td> 15.0</td> </tr>
<tr> <td> 318.0</td> <td> 18.0</td> </tr>
<tr> <td> 304.0</td> <td> 16.0</td> </tr>
<tr> <td> 302.0</td> <td> 17.0</td> </tr>
<tr> <td> 429.0</td> <td> 15.0</td> </tr>
<tr> <td> 454.0</td> <td> 14.0</td> </tr>
<tr> <td> 440.0</td> <td> 14.0</td> </tr>
<tr> <td> 455.0</td> <td> 14.0</td> </tr>
<tr> <td> 390.0</td> <td> 15.0</td> </tr>
</tbody> </table>

```
x = [307.0; 350.0; 318.0; 304.0; 302.0; 429.0; 454.0; 440.0; 455.0; 390.0];
y = [18.0; 15.0; 18.0; 16.0; 17.0; 15.0; 14.0; 14.0; 14.0; 15.0];
```

Also, for easy implementation, lets define our hypothesis to be function of both '&Theta;<sub>1'</sub> and 'x' as follows

```
function h = hypothesis(theta, x)
  h = theta * x;
end;
```

Similarly, let us define our cost function as follows

```
function J = cost(theta, x, y)
  m = length(x);
  J = 0;
  for i = 1:m
    J = J + (((hypothesis(theta, x(i))) - y(i)) ^ 2);
  endfor;
  J = J / (2 * m);
end;
```

To get an understanding of how the cost varies with theta, we will take some theta values (say between -10 and 10 with a step of 0.5) and calculate the cost for these values. Then we can plot theta against these values to see how they interact with each other

```
theta = [-10:0.5:10];
theta = theta(:);
costs = zeros(length(theta), 1);

for i = 1:length(theta)
  costs(i) = cost(theta(i), x, y);
endfor;

plot(theta, costs);
```

![]()

```
[a, b] = min(costs)
theta(b)
```

Our cost-function (J) is minimum (122.80) when theta = 0; but that is not the point. The point is that the above curve is a 'convex' curve, and has a global minimum. In the next post we are going to learn techniques to find this global minimum value, so keep watching this space for that!

I hope that the above explanation convinces you that:

* the cost function is defined in such a way that it has a global minimum (that needs to be found)
* once we find the values of theta which minimize the cost (or error), we would get a hypothesis that will allow us to predict the value of y, given x

So lets now meet in the next post in which we will see how to implement logic to minimize the cost-function J.
