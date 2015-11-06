{:title "ml-401: Multivariate Linear Regression"
 :layout :post
 :tags  []
 :toc true}

Hi! In the last <a href="http://www.golb.in/ml-305-univariate-linear-regression-43.html">post</a>, we completed learning our very first machine learning algorithm, viz "linear regression". As you might remember from <a href="http://www.golb.in/ml-102-supervised-learning-34.html">here</a>, this is a type of "supervised learning" ML algorithm. However, during our study, we had only 1 feature (or input variable), so that what we learnt was really the "univariate linear regression". Today we will take a look at how to handle a more real life situation, that is when we have more than one feature. Such an algorithm is called the "multivariate linear regression" ML algorithm.

To recap, for univariate linear regression, the steps were:

* <b>x</b> =&gt; input variable/feature (in "univariate", we have only 1 feature)
* <b>y</b> =&gt; output variable/target (this is the value that we need to predict)
* <b>m</b> =&gt; #training examples
* <b>h(x)</b> =&gt; hypothesis function, defined as

> h<sub>&Theta;</sub>(x) = &Theta;<sub>0</sub> + &Theta;<sub>1</sub> x

* <b>cost function</b> =&gt; J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) = (&Sigma;<sub>i</sub>=1<sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)
* minimization of the cost function was done using the "gradient descent" algorithm which was implemented as

> repeat until convergence {

> &Theta;<sub>0</sub> = &Theta;<sub>0</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)), for j = 0

> &Theta;<sub>1</sub> = &Theta;<sub>1</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>) * (x<sup>(i)</sup>)), for j = 1

> }

For the "multivariate" version of "linear regression" ML algorithm, we will have multiple features x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>, etc. We define one more notation

* <b>n</b> =&gt; number of features

In this case our hypothesis function "h(x)" will change as:

> h<sub>&Theta;</sub>(x) = &Theta;<sub>0</sub> + &Theta;<sub>1</sub> x<sub>1</sub> + &Theta;<sub>2</sub> x<sub>2</sub> + &Theta;<sub>3</sub> x<sub>3</sub> + &hellip; + &Theta;<sub>n</sub> x<sub>n</sub>

or

> h<sub>&Theta;</sub>(x) = &Theta;<sub>0</sub> + &Sigma;<sub>j=1</sub><sup>n</sup> &Theta;<sub>j</sub> x<sub>j</sub>

It is customary (makes later maths easier) to add an extra feature x<sub>0</sub> whose value is always "1", so that h(x) becomes

> h<sub>&Theta;</sub>(x) = &Sigma;<sub>j=0</sub><sup>n</sup> &Theta;<sub>j</sub> x<sub>j</sub>

Our cost function too will change as:

> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>, &Theta;<sub>2</sub>, &hellip;, &Theta;<sub>n</sub>) = (&Sigma;<sub>i=1</sub><sup>m</sup> &Sigma;<sub>j=1</sub><sup>n</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>j</sub>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)

And so will the gradient descent:

> repeat until convergence {

> &Theta;<sub>0</sub> = &Theta;<sub>0</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)), for j = 0

> &Theta;<sub>1</sub> = &Theta;<sub>1</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>1</sub>) - y<sup>(i)</sup>) * (x<sup>(i)</sup><sub>1</sub>)), for j = 1

> &Theta;<sub>2</sub> = &Theta;<sub>2</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>2</sub>) - y<sup>(i)</sup>) * (x<sup>(i)</sup><sub>2</sub>)), for j = 2

> &hellip;

> &Theta;<sub>n</sub> = &Theta;<sub>n</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>n</sub>) - y<sup>(i)</sup>) * (x<sup>(i)</sup><sub>n</sub>)), for j = n

> }

or, re-written simply:

> repeat until convergence {

> &Theta;<sub>j</sub> = &Theta;<sub>j</sub> - &alpha;\*(1/m)\* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup><sub>j</sub>) - y<sup>(i)</sup>) * (x<sup>(i)</sup><sub>j</sub>)), for j = 0 to n

> }

As always, remember that the above updates to all &Theta;<sub>j</sub> (for j = 0 to n) should happen simultaneously for a correct implementation (see <a href="http://www.golb.in/ml-305-univariate-linear-regression-43.html">here</a>)

Once we compute our hypothesis function using the above implementation, it is then trivial to predict "y" for any given input set of features

> y = h(x) = &Sigma;<sub>j=0</sub><sup>n</sup> &Theta;<sub>j</sub> x<sub>j</sub>

That's it for today. In the next post we will learn how to implement these algorithms using "vectorization" for faster performance. So stay tuned!
