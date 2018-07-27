### Keras
##### [metrics](https://keras.io/metrics/)

###### available metrics
- binary_accuracy
- categorical_accuracy
- sparse_categorical_accuracy
sparse主要指y非one-hot，是id
- top_k_categorical
- sparse_top_k_categorical_accuracy
sparse主要指y非one-hot，是id

##### custom metrics
``` python
import keras.backend as K

def mean_pred(y_true, y_pred):
    return K.mean(y_pred)

model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
              metrics=['accuracy', mean_pred])
```
```
[How does Keras calculate accuracy?](https://www.quora.com/How-does-Keras-calculate-accuracy)