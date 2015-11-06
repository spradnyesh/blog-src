{:title "ml-405: Normal Equation -- part - 1"
 :layout :post
 :tags  []
 :toc true}

Hello! Today we will learn an amazing ML algorithm that allows us to find the hypothesis function for a regression problem in just 1 step. Sounds exciting? So lets move forward with full force!</p>

As we already know from [here](http://www.golb.in/ml-402-multivariate-linear-regression-in-octave-45.html), the steps to solve a regression problem are:</p>

<b>hypothesis function</b> is defined as:</p>

> h<sub>&Theta;</sub>(x) = &Sigma;<sub>j</sub>=0<sup>n</sup> &Theta;<sub>j</sub> x<sub>j</sub></pre>

<b>cost function</b> is defined as:</p>

> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>, &Theta;<sub>2</sub>, &hellip;, &Theta;<sub>n</sub>) = (&Sigma;<sub>i</sub>=1<sup>m</sup> &Sigma;<sub>j</sub>=1<sup>n</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>j</sub>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)</pre>

While the <b>gradient descent</b> steps are:</p>

> repeat until convergence {

> &Theta;<sub>j</sub> = &Theta;<sub>j</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i</sub>=1<sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>j</sub>) - y<sup>(i)</sup>) * (x<sup>(i)</sup><sub>j</sub>)), for j = 0 to n

> }</pre>

Notice that the last step, viz the "gradient descent" is a loop, that is it takes an "iterative" approach to minimize the cost function, and thus find the optimal values for &Theta; (that is &Theta;<sub>0</sub>, &Theta;<sub>1</sub>, &hellip;, &Theta;<sub>n</sub>).</p>

Wouldn't it be great if we could skip this whole iteration step, and find the optimal values for &Theta; directly? Well, it is certainly possible; and that is exactly what we will learn today. This method of mathematically finding the optimal values of &Theta; directly (in just 1 step) is known as the "normal equation" method. Let us try to understand how it works by first solving a simple problem and then going on to the more general but difficult problem definition. So for now, let us assume that &Theta; is a scalar (real number), instead of a vector (&Theta;<sub>0</sub>, &Theta;<sub>1</sub>, &hellip;, &Theta;<sub>n</sub>). So our cost function is defined as:</p>

> j(&Theta;) = a * &Theta;<sup>2</sup> + b * &Theta; + c;</pre>

The mathematical way to find the optimal value of &Theta; that minimizes the above cost function is to find the derivative of the cost function and set it to 0 as follows</p>

> 2 * a * &Theta; + b = 0;</pre>

This is an equation with a single variable (&Theta;) and can be easily solved. The resulting value of &Theta; is the optimal value that we are looking for! Ain't that cool?</p>

To generalize, lets look at our original cost function again:</p>

> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>, &Theta;<sub>2</sub>, &hellip;, &Theta;<sub>n</sub>) = (&Sigma;<sub>i</sub>=1<sup>m</sup> &Sigma;<sub>j</sub>=1<sup>n</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>j</sub>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)</pre>

According to calculus theory, if we take the "partial derivatives" of the above cost function with respect to each of the &Theta;s (&Theta;<sub>0</sub>, &Theta;<sub>1</sub>, &hellip;., &Theta;<sub>n</sub>), set them to 0 (zero) and solve, we will get the optimal values for each of our &Theta;<sub>j</sub> (j = 0, 1, &hellip;, n)! Now these values can be easily substituted in the hypothesis function and used to predict values for "y".</p>

Ain't this cool? If it is, keep watching this space for the next post where we will look at the implementation of this method in octave, and also look at what advantages and disadvantages does this method have when compared with the gradient descent algorithm.</p>
