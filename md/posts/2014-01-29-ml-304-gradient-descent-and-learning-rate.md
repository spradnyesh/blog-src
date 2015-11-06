{:title "ml-304: Gradient Descent and Learning Rate"
 :layout :post
 :tags  []
 :toc true}

Hi. In the last <a href="http://www.golb.in/ml-303-gradient-descent-41.html">post</a>, we learnt about the "gradient descent" algorithm that is used to minimize our cost function "J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)". Gradient descent algorithm was defined as:

```
repeat until convergence {
  Θj = Θj - α δ/δΘj J(Θ0, Θ1) (for j = 0, 1)
}
```

where,

* <b>&alpha;</b>: is called the "learning rate"
* <b>&delta;/&delta;&Theta;<sub>j</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)</b>: is the partial derivative of the cost function (J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)) with respect to &Theta;<sub>j</sub>

Today we will try to understand the working of the gradient descent algorithm itself. We will also learn about the role of the learning rate "&alpha;". Let us start by understanding a single step of the algorithm, viz

> &Theta;j = &Theta;j - &alpha; &delta;/&delta;&Theta;j J(&Theta;0, &Theta;1) (for j = 0, 1)

As we have mentioned above, the term "&delta;/&delta;&Theta;<sub>j</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)" is the partial derivative of the cost function (J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)) with respect to &Theta;<sub>j</sub>. The partial derivative of a function defines the "slope" of that function at a given point. That is, in this case, this term defines the slope of our cost function at a given point.

![]()

We also know, from this <a href="http://www.golb.in/ml-302-intuition-for-univariate-linear-regression-39.html">post</a>, that the term &Theta; defines the slope of our hypothesis function "h(x)". So in a single step of the gradient descent algorithm, we are trying to change the slope &Theta; by a small amount (given by &alpha; times the slope of J).

![]()

How "small" is the change, is what is determined by the learning rate "&alpha;". If "&alpha;" is too small, then the changes will be very small and our gradient descent implementation will take a long time to converge (see the green points in the graph below). Whereas if "&alpha;" is too large, then gradient descent will take very big steps, and it is even possible for it to overshoot the minimum value and even diverge. But if "&alpha;" is just right (see red points in graph), then the implementation will take just the right steps and converge soon to the local minimum.

![]()

As such, the gradient descent algorithm can be used to find any minima (local or global). But because we have defined our cost function in such a way, that it is always convex and always has a global minima, our gradient descent implementation will always find the global minima!
