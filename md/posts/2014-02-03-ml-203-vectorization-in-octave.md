{:title "ml-203: Vectorization in Octave"
 :layout :post
 :tags  []
 :toc true}

I hope you have noticed that we have jumped back to the 20x series from the last [post](http://www.golb.in/ml-402-multivariate-linear-regression-in-octave-45.html) which was in the 30x series, and wondered why are we moving backwards ;). Well, that is because in the last 20x [post](http://www.golb.in/ml-202-octave-2-37.html) I had said that there is still one thing left about octave that we have not studied yet, but which we will study after completing one ML algorithm. So lets get onto that.

But before we move ahead, I urge you to take a look at our final program for "multivariate linear regression" ML algorithm implementation in the previous [post](http://www.golb.in/ml-402-multivariate-linear-regression-in-octave-45.html), because our today's discussion is all about how we can improve it's performance by making use of the "vectorization" property in octave.

The basic meaning of vectorization is that instead of running a (for) loop over a vector, we use matrix theory to do the computations. This is because in most of the programming languages that support matrix manipulations the libraries for doing them are heavily optimized and can run orders of magnitude faster than the corresponding loop implementation.

Lets take a concrete example to understand better. Lets look at the following snippet from our complete multivariate linear regression implementation (see previous [post](http://www.golb.in/ml-402-multivariate-linear-regression-in-octave-45.html)):

```
function y = hypothesis(x, theta)
  N = length(x);
  y = 0;
  for j in 1:N
    y = y + x(j) * theta(j);
  end;
end;
```

Remember that, the input variables "x" and "theta" in the above function are "1xN" and "Nx1" vectors respectively, so if we do the following vector multiplication

```
x * theta;
```

then the result is exactly the same as that of our previous implementation of the hypothesis function. So by implementing our hypothesis function as the following:

```
function y = hypothesis(x, theta)
  y = x * theta;
end;
```

we get the following benefits:

* our LOC (lines of code) reduces; and the less code we write, the less bugs it will have ;)
* more importantly, we have moved from a loop structure to matrix algebra, so that we are making use of the highly optimized libraries of octave. thus our overall program performance will improve tremendously
* the implementation becomes generic and will work for all of scalars, vectors and matrices

Similarly, we should take benefit from octave functions that will work on vectors and matrices and avoid loops completely. Taking cue from the above, lets re-implement our multivariate linear regression algorithm as follows:<div id="i-ads"><div class="g-ad"><ins class="adsbygoogle" style="display:inline-block;width:234px;height:60px" data-ad-client="ca-pub-7627106577670276" data-ad-slot="9310803587"></ins></div><div class="g-ad"><ins class="adsbygoogle" style="display:inline-block;width:234px;height:60px" data-ad-client="ca-pub-7627106577670276" data-ad-slot="1787536781"></ins></div></div>

```
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%% helper functions
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function y = hypothesis(x, theta)
  y = x' * theta;
end;

function J = cost(X, y, theta)
  m = size(X, 1);
  X = [ones(m, 1), X]; % add the x0 feature column
  J = sum((hypothesis(X, theta) - y) .^ 2) / (2 * m);
end;

function [J, theta] = gradientDescent(X, y, theta, alpha, num\_iters)
  m = size(X, 1);
  n = size(X, 2);
  for iter in 1:num\_iters
    diff = hypothesis(X, theta) - y;
    sum = zeros(n, 1);
    for j = 1:n
      sum(j) = sum(diff(j) .\* X'(:, j));
    endfor;
    theta = theta - (alpha * (sum / m));
  endfor;
  J = cost(X, y, theta);
end;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%% main program remains unchanged
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

Do you see the reduction in complexity? Still there is an improvement in the generality of the program! And to top it all this implementation runs super fast as compared to the previous. Ain't that great?

Ensure that you understand what is going on here. Take help from the previous 20x octave posts [here](http://www.golb.in/ml-201-octave-1-36.html) and [here](http://www.golb.in/ml-202-octave-2-37.html). Remember, the easiest trick to know that you are doing the correct thing is to check the ranks of the matrices that you are doing computation on. For example, in the first example above,

```
rank(x) => 1, n
rank(theta) => n, 1

expected rank of h => 1, 1

so it should be that => h = x * theta
```

If you remember the above rule-of-thumb, it should be difficult to make mistakes ;) But if you still have any doubts, don't hesitate to ask them using the comments, and I'll try my best to answer them. So what are you waiting for? Try implementing the above in octave on your system and try experimenting to improve your own understanding!

ps: In the coursera ML course, all octave programs are really programming assignments and have credits. I have broken the promise by giving (partially) answers here and in the previous [post](http://www.golb.in/ml-402-multivariate-linear-regression-in-octave-45.html). I will not show anymore octave programs continuing forward, but only the functions and intuitions behind them. I hope that you will understand. Thanks :)
