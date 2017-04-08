    
# 環境構築

## Anacondaのインストール

* 次のURLからAnaconda 4.3.1 をダウンロードした。
[https://www.continuum.io/downloads](https://www.continuum.io/downloads)

* 「自分専用にインストール」
* ANACONDA NAVIGATORを起動

```
$ python --version
Python 2.7.10
```
versionが異なるので変更した。
これでanancondaのpythonを通す。

```
export PATH=/Users/shinyayamamoto/anaconda/bin:$PATH
```


```
$ python --version
Python 3.6.0 :: Anaconda 4.3.1 (x86_64)
```

tensorflowの実行環境を作成

```
$ conda create -n tensorflow python=3.6
```

* アクティベート
```
$ source activate tensorflow
```

* 終わり
```
$ ource deativate tensorflow
```

tensorflowに必要なパッケージをインストール
```
$ source activate tensorflow
$ conda install -c conda-forge tensorflow
```

tensorflowためし。  

```
 import tensorflow as tf
 sess = tf.Session()
 a = tf.constant(10)
 b = tf.constant(32)
 print(sess.run(a + b))  

```

# MNIST for ML Beginners
[https://www.tensorflow.org/get_started/mnist/beginners](https://www.tensorflow.org/get_started/mnist/beginners)

##### キーワード
* 他校分類器
* ソフトマックス関数
* クロスエントロピー

文字データ28x28 => 786

![https://www.tensorflow.org/images/softmax-regression-scalargraph.png](https://www.tensorflow.org/images/softmax-regression-scalargraph.png)

![https://www.tensorflow.org/images/softmax-regression-scalarequation.png](https://www.tensorflow.org/images/softmax-regression-scalarequation.png)

![https://www.tensorflow.org/images/softmax-regression-vectorequation.png](https://www.tensorflow.org/images/softmax-regression-vectorequation.png)

```
y = softmax(W・x + b)
```
W => 重み  
b => bias  
x => 文字データ(786個)  
y => y1 ~ y10  


##### 実装してみる
[https://www.tensorflow.org/get_started/mnist/beginners#implementing_the_regression](https://www.tensorflow.org/get_started/mnist/beginners#implementing_the_regression)


```

# coding: utf-8

# from tensorflow.examples.tutorials.mnist import input_data
# mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)

# In[8]:

import tensorflow as tf


# In[9]:

x = tf.placeholder(tf.float32,[None,784])


# In[11]:

W = tf.Variable(tf.zeros([784,10]))
b = tf.Variable(tf.zeros([10]))


# In[12]:

y = tf.nn.softmax(tf.matmul(x,W) + b)


# In[14]:

y_ = tf.placeholder(tf.float32,[None,10])
cross_entropy = tf.reduce_mean(-tf.reduce_sum(y_ + tf.log(y), reduction_indices=[1]))


# In[16]:

train_step = tf.train.GradientDescentOptimizer(0.5).minimize(cross_entropy)


# In[17]:

init = tf.global_variables_initializer()


# In[19]:

sess = tf.Session()
sess.run(init)


# In[23]:

for i in range(1000):
    batch_xs, batch_ys = mnist.train.next_batch(100)
    sess.run(train_step, feed_dict={x: batch_xs, y_:batch_ys})


# In[24]:

correct_prediction = tf.equal(tf.argmax(y,1), tf.arg_max(y_,1))


# In[25]:

accuracy = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))


# In[30]:

print(sess.run(accuracy, feed_dict={x:mnist.test.images, y_:mnist.test.labels}))


# In[ ]:




# In[ ]:




```