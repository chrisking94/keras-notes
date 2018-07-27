### Keras
##### [Core Layers](https://keras.io/layers/core/)
- Dense
- Activation
- Dropout
- Flatten
- Input
- Reshape:
e.g.
model.add(Reshape((3, 4))) 3x4
model.add(Reshape((2, 6))) 2x6
model.add(Reshape((-1, 2, 2))) 3x2x2
- Permute
exchange the dims
Q:Why do this? A:To centralize feature map.Following is a picture about it.
![](why_permute.jpg "why_permute" "width:300px")
[SSD为什么要用到permute层？](https://www.zhihu.com/question/269160464)
- RepeatVector
Reapeats the input n times.i.e. expanding dimension.
- Lambda
it's just like a data processor in pydmlib
- ActivityRegularization
Layer that applies an update to the cost function based input activity.
aim to avoid overfitting, enhence generalization ability.
p norm:
$$
\Vert x \Vert _p = (\sum_{i=1}^N \vert x_i \vert ^p)^{\frac{1}{p}}
$$
[正则化方法：L1和L2 regularization、数据集扩增、dropout](https://www.cnblogs.com/mfryf/p/6245050.html)
[【直观详解】什么是正则化](https://charlesliuyx.github.io/2017/10/03/%E3%80%90%E7%9B%B4%E8%A7%82%E8%AF%A6%E8%A7%A3%E3%80%91%E4%BB%80%E4%B9%88%E6%98%AF%E6%AD%A3%E5%88%99%E5%8C%96/)
L1 Regularization: 使原最优解的元素产生不同的偏移，使某些元素为0；
L2 Regularization: 对原最优解的每个元素进行不同比例的缩放；
从而使某些元素为0，从而产生稀疏矩阵。
范数限制了梯度的方向（[深入理解L1、L2正则化](https://zhuanlan.zhihu.com/p/29360425)），当梯度分量在范数球切线方向的分量为零时达到最优解。
2 Arguments:
l1: L1 regularization factor (positive float).
l2: L2 regularization factor (positive float).
- Masking
mask timesteps, may usually used in RNN.
- SpatialDropout1D
- SpatialDropout2D

##### [Convolutional Layers](https://keras.io/layers/convolutional/)
- Conv1D
- Conv2D
- SeparableConv1D
- SeparableConv2D
- Conv2DTranpose
- Conv3D
- Cropping1D
- Cropping2D
- Cropping3D
- UpSampling1D
- UpSampling2D
- UpSampling3D
- ZeroPadding1D
- ZeroPadding2D
- ZeroPadding3D

##### [Pooling Layers](https://keras.io/layers/pooling/)
- MaxPooling1D
- MaxPooling2D
- MaxPooling3D
- AveragePooling1D
- AveragePooling2D
- AveragePooling3D
- GlobalMaxPooling1D
- GlobalAveragePooling1D
- GlobalMaxPooling2D
- GlobalAveragePooling2D
- GlobalMaxPooling3D
- GlobalAveragePooling3D

##### [LocallyConnected](https://keras.io/layers/local/)
- LocallyConnected1D
- LocallyCOnnected2D

##### [Recurrent Layers](https://keras.io/layers/recurrent/)
- RNN
- SimpleRNN
- GRU
- LSTM
- ConvLSTM2D
- SimpleRNNCell
- GRUCell
- LSTMCell
- CuDNNGRU
- CuDNNLSTM

##### [Embedding Layers](https://keras.io/layers/embeddings/)
- Embedding

##### [Merge Layers](https://keras.io/layers/merge/)
- Add
- Subtract
- Multiply
- Average
- Maximun
- Concatenate
- Dot

##### [Advanced Activation Layers](https://keras.io/layers/advanced-activations/)
- LeakyReLU
- PReLU (Parametric ReLU)
- ELU
$$
f(x) =
\begin{equation}
\left\{
\begin{array}{}
x, &x>0 \\
\alpha (e^x - 1), &x \leq 0
\end{array}
\right.
\end{equation}
$$
- ThresholdReLU
- Softmax
- ReLU
[ELU的提出](https://blog.csdn.net/mao_xiao_feng/article/details/53242235)

##### [Normalization Layers](https://keras.io/layers/normalization/)
Normalize the activations of the previous layer at each batch.
- BatchNormalization
to N(0,1)

##### [Noise layers](https://keras.io/layers/noise/)
They are useful to mitigate overfitting.
- GaussianNoise
arg:
stddev: float
Add $$$ N(0, stddev) $$$ noise on input data.
only active at training time.
- GaussianDropout
arg:
rate: float, denote as r
Multiply $$$ N(1, \sqrt{r/(1-r)}) $$$ noise on input data.
only active at training time.
- AlphaDropout
args:
rate: float
seed: a Python integer
Alpha Dropout是一种保持输入均值和方差不变的Dropout，该层的作用是即使在dropout时也保持数据的自规范性。 通过随机对负的饱和值进行激活，Alphe Drpout与selu激活函数配合较好。

##### [Layer wrapper](https://keras.io/layers/wrappers/)
- TimeDistributed
- Bidirectional

##### [custom Keras layers](https://keras.io/layers/writing-your-own-keras-layers/)
``` python
from keras import backend as K
from keras.engine.topology import Layer
import numpy as np

class MyLayer(Layer):

    def __init__(self, output_dim, **kwargs):
        self.output_dim = output_dim
        super(MyLayer, self).__init__(**kwargs)

    def build(self, input_shape):
        # Create a trainable weight variable for this layer.
        self.kernel = self.add_weight(name='kernel', 
                                      shape=(input_shape[1], self.output_dim),
                                      initializer='uniform',
                                      trainable=True)
        super(MyLayer, self).build(input_shape)  # Be sure to call this at the end

    def call(self, x):
        return K.dot(x, self.kernel)

    def compute_output_shape(self, input_shape):
        return (input_shape[0], self.output_dim)
```