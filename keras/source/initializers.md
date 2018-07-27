### Keras
##### [Initializers](https://keras.io/initializers/)
define the way to set the initial random weights of Keras layers.
``` python
model.add(Dense(64,
                kernel_initializer='random_uniform',
                bias_initializer='zeros'))
```
- Zeros
- Ones
- Constant
- RandomNormal
** args **
mean:
stddev:
seed:
- RandomUniform
** args **
minval:
maxval:
seed:
- TruncatedNormal
recommended initialzer for neural network weights and filters
** args **
familiar to RandomNormal except that values more than 2 stddev from the mean are discarded and re-drawn.
- VarianceScaling
** args **
scale: +float
mode: "fan_in", "fan_out", "fan_avg"
distribution: "normal", "uniform"
seed:
$$
\begin{align}
normal.stddev &= \sqrt{scale/n} , N(0, stddev) \\
uniform.limit &= \sqrt{3 * scale / n}, U(-limit, limit)
\end{align}
$$
- Orthogonal
** args **
gain:
seed:
- Identity
Only use for square 2D matrices
- lecun_normal
** args **
seed:
equals to VarianceScaling(scale=1.0, mode='fan_in', distribution='normal', seed=seed)
- lecun_uniform
** args **
seed:
equals to VarianceScaling(scale=1.0, mode='fan_in', distribution='uniform', seed=seed)
- glorot_normal
** args **
seed:
equals to VarianceScaling(scale=1.0, mode='fan_avg', distribution='normal', seed=seed)
- glorot_uniform
** args **
seed:
squals to VarianceScaling(scale=1.0, mode='fan_avg', distribution='uniform', seed=seed)
###### he init
does better in on deep network
- he_normal
*popular in ResNet*
** args **
seed:
equals to VarianceScaling(scale=2.0, mode='fan_in', distribution='normal', seee=seed)
- he_uniform
** args **
seed:
equals to VarianceScaling(scale=2.0, mode='fan_in', distribution='uniform', seed=seed)
- Using custom initializers

``` python
rom keras import backend as K

def my_init(shape, dtype=None):
    return K.random_normal(shape, dtype=dtype)

model.add(Dense(64, kernel_initializer=my_init))
```
