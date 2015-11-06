{:title "ml-303: Gradient Descent"
 :layout :post
 :tags  []
 :toc true}

Hi, welcome back! I hope you have been following our machine learning algorithm series in the last few posts. If you have, then you know that till now we have developed the basic framework for a particular algorithm called "univariate linear regression" and the only step pending is to minimize our cost function "J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)" so that we can find the optimal values of &Theta;<sub>0</sub> and &Theta;<sub>1</sub>. Once we have these values, we can substitute them and arrive at the definition of our hypothesis function "h(x)" which will let us predict the values for our target variable "y".</p>

I hope that things are clear till here. If they are, then lets move on to our last and final step of the algorithm, that is to minimize our cost function "J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)". The general outline of the steps that we will follow to achieve this are:</p>

* start with some value of &Theta;<sub>0</sub>, &Theta;<sub>1</sub> (a common choice is "0, 0")</li>
* keep changing &Theta;<sub>0</sub>, &Theta;<sub>1</sub> to reduce J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) until we hopefully end up at a minimum</li>

<img alt="" src="/static/photos/3f253e13ef98f0f1eab3f715986f0bc81_600.png" style="width: 600px; height: 332px;" /></p>

There are various minimization algorithms available, but the most commonly used (and the one that we will study now) is the "gradient descent" minimization algorithm. It is defined as below</p>

> repeat until convergence { &Theta;<sub>j</sub> = &Theta;<sub>j</sub> - &alpha; &delta;/&delta;&Theta;<sub>j</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>) (for j = 0, 1) }</pre>

where,</p>

* <b>&alpha;</b>: is called the "learning rate"</li>
* <b>&delta;/&delta;&Theta;<sub>j</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)</b>: is the partial derivative of the cost function (J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)) with respect to &Theta;<sub>j</sub></li>

Note that in the above algorithm, in any 1 step, <span style="text-decoration:underline;">all</span> of the &Theta;'s should be updated simultaneously. So,</p>

> temp0 = &Theta;<sub>0</sub> - &alpha; &delta;/&delta;&Theta;<sub>0</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)

> temp1 = &Theta;<sub>1</sub> - &alpha; &delta;/&delta;&Theta;<sub>1</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)

> &Theta;<sub>0</sub> = temp0

> &Theta;<sub>1</sub> = temp1</pre>

is correct, but the following is not</p>

> temp0 = &Theta;<sub>0</sub> - &alpha; &delta;/&delta;&Theta;<sub>0</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)

> &Theta;<sub>0</sub> = temp0

> temp1 = &Theta;<sub>1</sub> - &alpha; &delta;/&delta;&Theta;<sub>1</sub> J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)

> &Theta;<sub>1</sub> = temp1</pre>

That is because in the second set of commands, when we are calculating temp1, we use the <span style="text-decoration:underline;">new</span> value of &Theta;<sub>0</sub>, instead of the old one. This is a very important step and missing this can lead to a lot of difficult to find errors, so be careful about implementing this step.</p>

That's it for today. In the next post we will dig deeper to get an understanding of how gradient descent works to find the minimal value of the cost function (J(&Theta;<sub>0</sub>, &Theta;<sub>1</sub>)) and in turn help us to find the optimal values of &Theta;<sub>0</sub> and &Theta;<sub>1</sub>. We will also see what is the learning rate "&alpha;" and how it's value will have an impact on the performance of our gradient descent implementation.</p>
