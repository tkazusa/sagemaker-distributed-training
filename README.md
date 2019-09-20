# Sagemakerでの分散学習

- [PARALLELIZED DATA DISTRIBUTION](https://sagemaker-workshop.com/builtin/parallelized.html)

## [Amazon SageMaker Tensorflow ハンズオン](https://github.com/shokout/handson-201812)
- パラメーターサーバを使った分散学習ハンズオン


### [TensorFlow 分散トレーニングオプション](https://github.com/aws-samples/amazon-sagemaker-script-mode/blob/master/tf-distribution-options/tf-distributed-training.ipynb)
- Tensorflowのネイティブパラメーターサーバーを用いた分散学習とHorovodを使った分散学習の両方を提供している
- データはcifer-10をTFrecordeに変換して使用、Tensorflowの実装は1.13の'tf.keras'
- パラメーターサーバーを用いた分散学習
  - SageMakerのTensorflow Estimator Ovjectのdistributions引数に分散学習用の設定を渡した上で、instance_countを複数にすればOK。
  - 学習が進むと.pb形式でモデルが保存され、それはTensorflow servingのコンテナで読み込める。



## Horovodを用いた分散学習 

- [Amazon SageMaker の Horovod またはパラメータサーバーでTensorFlow 分散トレーニングを簡単に起動する](https://aws.amazon.com/jp/blogs/news/launching-tensorflow-distributed-training-easily-with-horovod-or-parameter-servers-in-amazon-sagemaker/)
- [Sagemaker Distributed Training with Parameter Server and Horovod](https://github.com/aws-samples/sagemaker-horovod-distributed-training)
- [Amazon SageMaker TensorFlow のスクリプトモードを使用した Horovod 分散トレーニング](https://github.com/awslabs/amazon-sagemaker-examples/blob/master/sagemaker-python-sdk/tensorflow_script_mode_horovod/tensorflow_script_mode_horovod.ipynb)


# 参考
- [Power Machine Learning at Scale](https://d1.awsstatic.com/whitepapers/aws-power-ml-at-scale.pdf)
  - AWSインフラ上で分散学習をやった際のホワイトペーパー
  - 分散深層学習だけじゃなくてDaskとかRayとかについても言及してるっぽい。

# 疑問
- インスタンスタイプと分散学習の通信速度の関係
  - p2.xlargeとp2.8xlargeでやると、同じインスタンス数をしていしていた場合、どの程度違う？
