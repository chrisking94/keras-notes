## Keras
##### [losses](https://keras.io/losses/)
*def loss(y_true, y_pred)*
suppose n is sample size
- MSE: mean_squared_error
$$
MSE(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^{n}(y_i - \hat{y}_i)^2
$$
- MAE: mean_absolute_error
$$
MAE(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^{n} \vert y_i - \hat{y_i} \vert
$$
- MAPE: mean_absolute_percentage_error
$$
MAPE(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^n \vert \frac{y_i - \hat{y}_i}{y_i} \vert
$$
- MSLE: mean_squared_logarithmic_error
$$
MSLE(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^n(log(\hat{y}_i + 1) - log(y + 1))^2
$$
- RMSLE:
RMSLE is usually used when you don't want to penalize huge differences in the predicted and true values when both predicted and true values are huge numbers.
- hinge
notably used in SVM
suppose labels are {-1, 1}
$$
hinge(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^n max(0, 1-y_i*\hat{y_i})
$$
- SH: squared_hinge
$$
SH(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^n max^2(0, 1 - y_i * \hat{y}_i)
$$
- CH: categorical_hinge
TODO
- logcosh
$$
logcosh = \frac{1}{n} \sum_{i=1}^n log(cosh(\hat{y}_i - y_i)) \\
\begin{align}
cosh &= \frac{e^x + e^{-x}}{2} \\
sinh &= \frac{e^x - e^{-x}}{2} \\
\end{align} \\
$$
$$$logcosh(x) \approx x^2/2$$$ for small x and $$$ logcosh(x) \approx \vert x \vert - log(2) $$$ for large x .This means that 'logcosh' works mostly like the MSE, but will not be so strongly affected by the occasional wildly incorrect prediction.
- - -
[**prerequisites**](https://blog.csdn.net/rtygbwwwerr/article/details/50778098)
*entropy:* $$$ H(x) = -\sum_{x \in X} p(x)logp(x) $$$, appoint $$$p(x)logp(x) \to 0 $$$ when $$$ x \to 0 $$$
*relative entropy*: (i.e. Kullback-Leibler divergence,KL Distance), is a metric of distance between 2 randomly distributed variable.It measures the ineffictivity of distribution q when the real distibution is q.Note as:
$$
D_{KL}(p \Vert q) = \sum_{x \in X} p(x)log\frac{p(x)}{q(x)} = H_p(q) - H(p)
$$
*cross entropy*: $$$ CEH(p,q) = -\sum_{x \in X}p(x)logq(x) = H_p(q)$$$.Minimizing $$$ CEH $$$ is equivalent to minimization of $$$ D_{kl} $$$, where $$$ H_p $$$ is a constant.
** cross-entropy cost function **
$$
C = - \frac{1}{n} \sum_{i=1}^n[y_iln\hat{y}_i+(1-y_i)ln(1-\hat{y}_i)]
$$
3 characteristics
&nbsp; a.non-negativity
&nbsp; b.$$$when \ \hat{y} \sim y \ then\ C \sim 0 $$$
&nbsp; c.the huger difference between $$$ \hat{y} $$$ and $$$ y $$$, the bigger $$$ C $$$ is.That means the faster update on weights.
- categorical_crossentropy
for multi labels
- sparse_categorical_crossentropy
- binary_crossentropy
- kullback_leibler_divergence
$$$ D_{KL}(p\Vert q) $$$
also called relative divergence,  is a measure of how one probability distribution diverges from a second, expected probability distribution.

- - -

- poisson
is a measure of how the distribution diverges from the expected distribution.
$$
poisson(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^n (\hat{y}_i - y_i * log(\hat{y_i}))
$$
- cosine_proximity
K.l2_normalize:
$$
y' = L2(y), \hat{y}'=L2(\hat{y}) \\
cosine_proximity(y, \hat{y}) = -\sum_{i=1}^n(y_i', \hat{y}_i')
$$
$$
L2(x) = \frac{x}{\sqrt{max( \sum_{i=1}^n x^2, \epsilon)}}
$$