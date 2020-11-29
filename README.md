# WSL2_NGC_Docker
Install docker on Ubuntu 18 on WSL2 and set up NGC docker.

# Windows10のバージョンを確認
~~~
# windowsの検索窓で
winver
~~~
バージョン 20H2 OSビルド 19042.630の場合、CUDAのサンプルを実行することができない。

よって(かは不明)、NGC Dockerを起動することは成功するが、--runtime=nvidiaを付けて起動することができない。

しかし、GPUを使用しないNGC Dockerでの開発は可能。

ビルド 20226と20231では、WSL2でGPUが使用できない情報あり。20236で修正されたようだ。

ビルド 19042ではGPUが使用できないようだ。

https://qiita.com/ksasaki/items/ee864abd74f95fea1efa

---
# 注意
Windowsに、Docker Desktop for Windowsを入れてはいけない。

WSL2上の docker ce と競合するようだ。

https://qiita.com/mitsu-h/items/4b21c128d178ac8a0f36

しかし、Docker for Windows10が確実に無い状態でも、ビルド19042ではGPU使用できない。

---
# Windows 10 用 Windows Subsystem for Linux のインストール ガイド
## 公式の手順に従いインストール

https://docs.microsoft.com/ja-jp/windows/wsl/install-win10

## Windows ターミナルをインストールする
https://docs.microsoft.com/ja-jp/windows/terminal/

---
# CUDA on WSL(2) User Guide
## 公式の手順に従いインストール
https://docs.nvidia.com/cuda/wsl-user-guide/index.html#installing-nvidia-drivers

## 日本語紹介
https://qiita.com/ksasaki/items/ee864abd74f95fea1efa

~~~
sudo apt-get install -y cuda-toolkit-11-0
~~~

成功するが、

~~~
cd /usr/local/cuda/samples/1_Utilities/deviceQuery/
sudo make
sudo ./deviceQuery
~~~

は失敗する

Ubuntu18上にCUDAがインストールされていなくても関係ない という情報があるが、
 * ビルドが古い

もしくは
 * Ubuntu18上でCUDAのインストールが失敗している

ため、NGC Dockerを起動できるが、GPUを使用することはできない。

---
# WSL2上のUbuntu18でDevContainer

WSLでは/mnt/c/で、windowsとwsl間でファイル共有するが、動作が遅いので、他の場所に配置する。

WSL2上のUbuntu18内で
~~~
cd ~
mkdir git
cd git
cit clone https://github.com/ShowTakano/WSL2_NGC_Docker.git
code ./WSL2_NGC_Docker
~~~
でVSCodeがRemote-WSLで起動する

https://qiita.com/sgmryk/items/580147433a0bd4eb18f3
