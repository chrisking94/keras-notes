### Keras
##### [Constraints](https://keras.io/constraints/)
constraints for (activation function) weights matrix
``` python
from keras.constraints import max_norm
model.add(Dense(64, kernel_constraint=max_norm(2.)),
					bias_constraint=max_norm(2.))
```
##### Available constraints
- max_norm
1 of its appealing properties: network cannot "explode" even when the learning rates are set too high because the updates are always bounded.
eg. max_norm(x): if the L2-Norm of weights exceeds m, scale whole weight matrix by a factor that reduces the norm to m.
- non_neg
- unit_norm
$$
unit\_norm(w) = \frac{w}{\sqrt{\sum w^2}}
$$
- min_max_norm
** args **
min_value:
max_value:
rate:
axis:
