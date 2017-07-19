# Tensorflow 1.2.1 + Jestson TX2
### Prerequisites
    * JetPack 3.0 (Ubuntu 16.04, CUDA 9.0, CUDNN 5.1, gcc 5.4)
    * Download and unzip bazel-0.5.2-dist at /home
    * git clone tensorflow && git checkout v1.2.1 at /home

### Install
    * Change to the Repo, run installDependencies.sh
    * Change to directory bazel-0.5.2-dist，sudo ./compile.sh && cp -rf output/bazel /usr/local/bin
    * Change to directory tensorflow，using tensorflow.patch  to modify workspace.bzl: patch -p1 < tensorflow.patch
    * Change to the Repo, run setTensorFlowEV.sh and buildTensorFlow.sh
    * Change to the Repo, Run packageTensorFlow.sh
    * Install complied Tensorflow： pip install $HOME/wheel file

### Test
    * MNIST
    * mobileNet

# installTensorFlowTX2
April 1, 2017
Install TensorFlow v1.2.0 on NVIDIA Jetson TX2 Development Kit

Jetson TX2 is flashed with JetPack 3.0 which installs:
* L4T 27.1 an Ubuntu 16.04 64-bit variant (aarch64)
* CUDA 8.0
* cuDNN 5.1.10

### Installation
Before installing TensorFlow, a swap file should be created (minimum of 8GB recommended). The Jetson TX2 does not have enough physical memory to compile TensorFlow. The swap file may be located on the internal eMMC, and may be removed after the build.

Note: This procedure was derived from these discussion threads: 

<ul>
<li>https://github.com/tensorflow/tensorflow/issues/851</li>
<li>http://stackoverflow.com/questions/39783919/tensorflow-on-nvidia-tx1/</li>
<li>https://devtalk.nvidia.com/default/topic/1000717/tensorflow-on-jetson-tx2/</li>
<li>https://github.com/tensorflow/tensorflow/issues/9697</li>
</ul>

TensorFlow should be built in the following order:

#### installPrerequisites.sh
Installs Java and other dependencies needed. Also builds:

##### Bazel
Builds version 0.4.5. Includes patches for compiling under aarch64. 

#### cloneTensorFlow.sh
Git clones v1.2.0 from the TensorFlow repository and patches the source code for aarch64

#### setTensorFlowEV.sh
Sets up the TensorFlow environment variables. This script will ask for the default python library path. There are many settings to chose from, the script picks the usual suspects. Uses python 2.7.

#### buildTensorFlow.sh
Builds TensorFlow.

#### packageTensorFlow.sh
Once TensorFlow has finished building, this script may be used to create a 'wheel' file, a package for installing with Python. The wheel file will be in the $HOME directory.

#### Install wheel file
$ pip install $HOME/<em>wheel file</em>


#### Build Issues

For various reasons, the build may fail. The 'debug' folder contains a version of the buildTensorFlow.sh script which is more verbose in the way that it describes both what it is doing and errors it encounters. See the debug directory for more details.

#### Notes

