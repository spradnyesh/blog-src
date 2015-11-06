{:title "ml-305: Univariate Linear Regression"
 :layout :post
 :tags  []
 :toc true}

In the last posts [here](http://www.golb.in/ml-303-gradient-descent-41.html)&nbsp;and [here](http://www.golb.in/ml-304-gradient-descent-and-learning-rate-%CE%B1-42.html), we looked in much depth at the "gradient descent" minimization algorithm. Today we will complete the puzzle by fitting that last piece in the whole jigsaw of the "univariate linear regression" ML algorithm that we have been studying in this 30x series.

To do that, lets recap what we have learnt so far:

* x =&gt; input variable/feature (in "univariate", we have only 1 feature)
* y =&gt; output variable/target (this is the value that we need to predict)
* m =&gt; #training examples
* h(x) =&gt; hypothesis function, defined as

> h<sub>&Theta;</sub>(x) = &Theta;<sub>0</sub> + &Theta;<sub>1</sub> x

* J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) = (&Sigma;<sub>i</sub>=1<sup>m</sup> (h<sub>&Theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup>)/(2\*m)
* Goal is to minimize the cost function, to find optimal values of &Theta;<sub>0</sub> and &Theta;<sub>1</sub> (to be substituted in the hypothesis function). This is achieved using gradient descent algorithm, defined as

> repeat until convergence {

> &Theta;<sub>j</sub> = &Theta;<sub>j</sub> - &alpha; &delta;/&delta;&Theta;<sub>j</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) (for j = 0, 1)

> }

where,

* <b>&alpha;</b>: is called the "learning rate"
* <b>&delta;/&delta;&Theta;<sub>j</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)</b>: is the partial derivative of the cost function (J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)) with respect to &Theta;<sub>j</sub>

The only thing left is to substitute the real value of J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) inside the gradient descent algorithm. To do that we need to know the partial derivative of J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) with respect to &Theta;<sub>0</sub> and &Theta;<sub>1</sub>. Without going into derivation of the partial derivatives (because

* it is too complex and mathematically involved
* i don't know it ;) and
* knowing the derivation is not needed to correctly implement gradient descent

), the gradient descent steps are defined (for our cost function for univariate linear regression) as:

> repeat until convergence {

> &Theta;<sub>0</sub> = &Theta;<sub>0</sub> - &alpha;*(1/m)* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x(i)) - y(i))), for j = 0

> &Theta;<sub>1</sub> = &Theta;<sub>1</sub> - &alpha;*(1/m)* (&Sigma;<sub>i=1</sub><sup>m</sup> (h<sub>&Theta;</sub>(x(i)) - y(i)) * (x(i))), for j = 1

> }

That is we are inserting the actual values of the partial derivatives of J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>), with respect to &Theta;<sub>0</sub> and &Theta;<sub>1</sub> respectively in the gradient descent implementation. As mentioned previously, while implementing this step in octave (or any other software), it is extremely important to make both updates simultaneously.

With this we have completed learning our first ML algorithm, viz the "univariate linear regression". I hope you have had as much fun learning it as I have teaching it. For me, a lot of my concepts have become clear while explaining things over here in so much detail! This alone has made the whole effort worthwhile. It has also given me motivation to continue this series. So in the upcoming posts I will try to explain other more advanced ML algorithms.

Do leave comments below to share with me your experience here, especially (constructive) criticism about how I can strive to make these posts better. I am eagerly looking forward to hearing from you :)
