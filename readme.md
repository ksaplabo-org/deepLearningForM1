# Macbook M1にpython3 OpenCV TensorFlow開発環境を整える

目標：macbook m1のカメラを使用して手の形（グーチョキパー）を捉える。

## python3の環境構築
初期状態でmacbook内にはpython3が入っているはず。確認のみ。  
homebrew等で入れたpythonは全て消しておくほうが吉。
```
 $ python3 -V
```

## MiniForgeのインストール
macbook m1にTensorFlow for macOSをインストールするため、MiniForgeを導入する。  
以下URLから"Miniforge3-MacOSX-arm64.sh"をダウンロード後、コマンド実行  
https://github.com/conda-forge/miniforge/releases
```
$ cd ~/Downloads
$ ./Miniforge3-MacOSX-arm64.sh
```
インストール時にいくつか質問されるが Enter / yes で進む。

## miniForgeにpython3.8環境を構築、環境をアクティベート
```
$ conda create --name python38 python=3.8
$ conda activate python38
```
## ライブラリ等のインストール
```
$ conda install numpy
$ conda install six
$ conda install matplotlib
$ conda install opencv
```
## TensorFlowのインストール
以下URLからTensorFlowをダウンロード  
https://github.com/apple/tensorflow_macos/releases/  
執筆時点での最新は"tensorflow_macos-0.1alpha3.tar.gz"
```
$ cd ~/Downloads
$ tar xvzf tensorflow_macos-0.1alpha3.tar.gz
$ env="$HOME/miniforge3/envs/python38"
$ libs="$PWD/tensorflow_macos/arm64/"
$ pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/grpcio-1.33.2-cp38-cp38-macosx_11_0_arm64.whl"
$ pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/h5py-2.10.0-cp38-cp38-macosx_11_0_arm64.whl"
$ pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/tensorflow_addons_macos-0.1a3-cp38-cp38-macosx_11_0_arm64.whl"
$ conda install -c conda-forge -y absl-py
$ conda install -c conda-forge -y astunparse
$ conda install -c conda-forge -y gast
$ conda install -c conda-forge -y opt_einsum
$ conda install -c conda-forge -y termcolor
$ conda install -c conda-forge -y typing_extensions
$ conda install -c conda-forge -y wheel
$ conda install -c conda-forge -y typeguard
$ pip install wrapt flatbuffers tensorflow_estimator google_pasta keras_preprocessing
$ pip install protobuf==3.20.1
$ pip install tensorboard
$ pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/tensorflow_macos-0.1a3-cp38-cp38-macosx_11_0_arm64.whl"
```
※protbufについてはバージョン指定して動かさないと駄目っぽい。  
実行する際にDowngrade the protobuf package to 3.20.x or lower.と怒られた。

TensorFlowが入ったか確認するには、pythonのコンソール上で以下。バージョン情報が表示されればOK
```
$ python3
>>> import tensorflow as tf
>>> tf.__version__
'2.4.0-rc0'
```

