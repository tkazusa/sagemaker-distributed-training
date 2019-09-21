# Sagemakerでの分散学習

## Tensorflow
### [Amazon SageMaker Tensorflow ハンズオン](https://github.com/aws-samples/amazon-sagemaker-examples-jp/blob/master/tensorflow_script_mode_training_and_serving/tensorflow_script_mode_training_and_serving.ipynb)
- パラメーターサーバを使った分散学習ハンズオン
- 学習データはMNISTデータ


### [TensorFlow 分散トレーニングオプション](https://github.com/aws-samples/amazon-sagemaker-script-mode/blob/master/tf-distribution-options/tf-distributed-training.ipynb)
- 解説記事：[Amazon SageMaker の Horovod またはパラメータサーバーでTensorFlow 分散トレーニングを簡単に起動する](https://aws.amazon.com/jp/blogs/news/launching-tensorflow-distributed-training-easily-with-horovod-or-parameter-servers-in-amazon-sagemaker/)
- Tensorflowのネイティブパラメーターサーバーを用いた分散学習とHorovodを使った分散学習の両方についての概要を提供。
- データはcifer-10をTFrecordeに変換して使用、Tensorflowの実装は1.13の'tf.keras'
- パラメーターサーバーを用いた分散学習
  - SageMakerのTensorflow Estimatorのdistributions引数に`distributions = {'parameter_server': {'enabled': True}}`を渡した上で、instance_countを複数にすればOK。
  - 学習が進むと.pb形式でモデルが保存され、それはTensorflow servingのコンテナで読み込める。
- Horovodを用いた分散学習
  - SageMakerのTensorflow Estimatorインスタンスのdistributions引数に`distributions = {'parameter_server': {'enabled': True}}`を渡した上で、instance_countを複数にすればOK。


### [Sagemaker Distributed Training with Parameter Server and Horovod](https://github.com/aws-samples/sagemaker-horovod-distributed-training)
- [Horovod Distributed Training with SageMaker TensorFlow script mode](https://github.com/aws-samples/sagemaker-horovod-distributed-training/blob/master/notebooks/tensorflow_script_mode_horovod.ipynb)では、Horovodを用いたTensorflowで以下の4つの分散学習の実施方法を比較している。
  - MPIを使ったnotebookインスタンス上での分散学習
  - 学習インスタンス上での分散学習
  - 各学習インスタンス上で複数のCPU/GPUを使った分散学習
  - VPCを用いてネットワークレイテンシを低減させた上で、各学習インスタンス上で複数のCPU/GPUを使った分散学習
- awslabのリポジトリにも同様の[notebook](https://github.com/awslabs/amazon-sagemaker-examples/blob/master/sagemaker-python-sdk/tensorflow_script_mode_horovod/tensorflow_script_mode_horovod.ipynb)がある


# 参考
- [Power Machine Learning at Scale](https://d1.awsstatic.com/whitepapers/aws-power-ml-at-scale.pdf)
  - AWSインフラ上で分散学習をやった際のホワイトペーパー
  - 分散深層学習だけじゃなくてDaskとかRayとかについても言及してるっぽい。
- - [PARALLELIZED DATA DISTRIBUTION](https://sagemaker-workshop.com/builtin/parallelized.html)

# 疑問
- インスタンスタイプと分散学習の通信速度の関係
  - p2.xlargeとp2.8xlargeでやると、同じインスタンス数をしていしていた場合、どの程度違う？
