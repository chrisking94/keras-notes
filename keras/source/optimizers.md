### Keras
##### [optimizer](https://keras.io/optimizers/)
method to choose better learning rate automatically
#####1.gradient clipping
1.after fowardpropagation or backpropagation, there are several diffs $$$\vec{d}$$$ over each weights $$$\vec{w}$$$.
$$ssd=\sum_{i=1}^kd_i^2$$
if $$$ ssd > clip\_gradient $$$,then scale factor $$$sf=clip\_gradient/ssd$$$.
b.$$$ \vec{w} = \vec{w} * sf $$$
params for all optimizers
== clipnorm: maximum norm ==
== clipvalue(cv): gradients will be clipped between -cv and cv ==
##### SGD [see](https://blog.csdn.net/bvl10101111/article/details/72616097)
args:
1.lr
2.momentum
3.decay(lr decay over each update)
4.nesterov(boolean, whether to apply Nesterov momentum， 牛顿动量) [see](https://blog.csdn.net/shuzfan/article/details/75675568)
##### RMSprop(Root Mean Squared Prop) [see](https://blog.csdn.net/bvl10101111/article/details/72616378)
good for RNN
an improvement for AdaGrad, better than other optimizers within none-convex condition
RMSProp: $$$ r\leftarrow \rho r + (1-\rho)g\bigodot g $$$ (r is learning rate, where g is sqrt_sum_square(historical gradient))
aim to deal with the vibration in optimization
args:
1.lr
2.rho (recommended default)
3.espilon (recommended default) ** ? **
4.decay (recommended default)
##### Adagrad [see](https://blog.csdn.net/bvl10101111/article/details/72616097)
AdaGrad: $$$ r\leftarrow r+g\bigodot g$$$
variational learning rate
args(recommended default):
1.lr
2.epsilon
3.decay
##### Adadelta
similiar to Adagrad, but Adadelta's historical gradient is a subset of whole historical G, i.e. a moving windown of gradient updates.
args(recommended default):
1.lr
2.rho
3.epsilon(Adadelta decay factor, corresponding to fraction of gradient to keep at each time step.)
4.decay
##### Adam(Ada momentum) [see](https://blog.csdn.net/bvl10101111/article/details/72616516)
Momentum + RMSProp in actual
args:
1.lr(recommeded 0.001)
2.beta_1($$$ \rho_1 $$$, 0.9, 1st moment estimation exp decay rate)
3.beta_2($$$ \rho_2 $$$, 0.999), 2nd moment estimation exp decay rate)
4.epsilon
5.decay
6.amsgrad [see](https://www.jiqizhixin.com/articles/2017-12-06)
&emsp;&emsp;在 Adam 算法收敛到次优解的过程中，它已经观察到一些小批量数据提供了大量且具有信息的梯度，但是由于这些小批量数据发生地非常少，指数平均将降低它们的影响，这也就造成了 Adam 只能收敛到次优的极小值点。作者提供了一个简单的凸优化案例，其中 ADAM 方法并不能收敛到非常好的最优解。
&emsp;&emsp;为了解决这个问题，作者提出了一个新算法 AMSGrad，该算法使用过去梯度平方的最大值以替代指数平均值来更新参数。不带偏差修正估计的 AMSGrad 更新规则可以表示为：
$$
m_t = \beta_1m_{t-1} + (1-\beta_1)g_t \\
v_t = \beta_2v_t+(1-\beta_2)g_t^2 \\
\hat{v}_t = max(v) \\
\theta_{t+1} = \theta - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon}
$$
##### Adamax
##### Nadam
Nadam is Adam RMSprop with Nesterov momentum
args(recommended dafault):
1.lr
2.beta_1
3.beta_2
4.epsilon
5.schedule_decay
