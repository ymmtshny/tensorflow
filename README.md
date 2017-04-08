    
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
>>> import tensorflow as tf
>>> sess = tf.Session()
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print(sess.run(a + b))
```