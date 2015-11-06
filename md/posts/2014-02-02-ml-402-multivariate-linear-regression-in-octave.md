{:title "ml-402: Multivariate Linear Regression in Octave"
 :layout :post
 :tags  []
 :toc true}

Hi! I hope that you have been following the recent posts in the ML series where we have understood in much detail the various aspects of the linear regression ML algorithm, and also intuition about how it works. We have also formulated all the mathematical formulae, but have not seen how to implement them in octave yet. So that's what we are going to do today. Lets start with a small recap (of only the functions) of the multivariate linear regression ML algorithm:

<b>hypothesis function</b> is defined as:

> h<sub>&theta;</sub>(x) = &Sigma;<sub>j=0</sub><sup>n</sup> &theta;<sub>j</sub> x<sub>j</sub>

<b>cost function</b> is defined as:

> J<sub>(&theta;0, &theta;1, &theta;2, &hellip;, &theta;n)</sub> = (&Sigma;<sub>i=1</sub><sup>m</sup> &Sigma;<sub>j=1</sub><sup>n</sup> (h<sub>&theta;</sub>(x<sup>(i)</sup><sub>j</sub>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)

While the <b>gradient descent</b> steps are:

> repeat until convergence {

> &theta;<sub>j</sub> = &theta;<sub>j</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&theta;</sub>(x<sup>(i)</sup><sub>j</sub>) - y<sup>(i)</sup>) * (x<sup>(i)</sup><sub>j</sub>)), for j = 0 to n

> }

Before we move onto octave, lets define some variables:

> <b>X</b> =&gt; input feature "matrix" of size "mxn"

> <b>x</b> =&gt; "one" example "vector" of size "(n+1)x1" (including the pivot feature x0 (which is always = 1))

> <b>&theta;</b> =&gt; vector of size "(n+1)x1"

> <b>y</b> =&gt; output target variable "vector" of size "mx1"

Now for the actual octave program

```
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%% helper functions
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

function y = hypothesis(x, theta)
  N = length(x); % this is actually inclusive of pivot x0, so this N = n + 1, where n = #features
  y = 0;
  for j in 1:N
    y = y + x(j) * theta(j);
  end;
end;

function J = cost(X, y, theta)
  m = size(X, 1);
  X = [ones(m, 1), X]; % add the x0 feature column
  n = size(X, 2); % note that this n includes the x0 feature too
  J = 0;
  for i in 1:m
    J = J + (hypothesis(X(i, :), theta) - y(i)) ^ 2; % the inner "j" for-loop is inside the "hypothesis" function
  end;
  J = J / (2 * m);
end;

function [J, theta] = gradientDescent(X, y, theta, alpha, num\_iters)
  % ideally we should let gradientDescent run until convergence,
  % but for simplicity we will run it for a fixed number of iterations (num\_iters)
  
  m = size(X, 1);
  n = size(X, 2);
  
  for iter in 1:num\_iters
    sum = zeros(n, 1);
    for i = 1:m
      diff = hypothesis(X(i, :), theta) - y(i);
      for j = 1:n
        sum(j) = sum(j) + diff * X(i, j);
      end;
    end;
    for j = 1:n
      theta(j) = theta(j) - (alpha * (sum(j) / m));
    end;
  end;

  J = cost(X, y, theta);
end;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%% main program starts here
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

[X, y] = load("data");        % load some data

%%%%% initialize some basic variables
m = size(X, 1);               % #training examples
X = [ones(m, 1), X];          % add pivot feature vector x0
n = size(X, 2);               % #features + 1
alpha = 0.01;                 % "learning rate"; actual value needs to be determined experimentally
theta = zeros(n, 1);          % initialize to some arbitrary value
num\_iters = 1000;             % initialize to some arbitrary value

%%%%% run gradientDescent
[J, theta] = gradientDescent(X, y, theta, alpha, num\_iters);
```

That's it! Wasn't that easy?

Once we have found out the optimal values for &theta; (theta), we can find the value for any new "y", by simply calling the hypothesis function using the new (given) value for "x".
