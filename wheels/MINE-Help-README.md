# This is not a README.md. This is for my own use.
Structured way to build Tensorflow.

## Ubuntu 18.04 x86_64 install TensorFlow 2.4.1 (python 3.8, Bazel 3.1.0) with support SSE, SSE2,SSE3 without SSSE3, SSE4.1, SSE4.2, AVX, AVX2, FMA instructions

Careful with `gcc` and `g++` compilers, `numpy` version depending on TF (got some errors, carelessness). Of course this also is true for `bazel`.

## 1. Create a new conda environment with Python 3.8
```bash
conda create --name=tf-2.4.1-noavx python=3.8
```

## 2. Activate the conda environment
```bash
conda activate tf-2.4.1-noavx
```

## 3. Install required Python packages
```bash
pip install "numpy<1.20" wheel packaging requests opt_einsum six
pip install keras_preprocessing --no-deps
```

## 4. Install Bazel 5.3.0
### a. Install dependencies
```bash
sudo apt install apt-transport-https curl gnupg -y
```

### b. Add Bazel distribution URI as a package source
```bash
curl -fsSL https://bazel.build/bazel-release.pub.gpg | gpg --dearmor >bazel-archive-keyring.gpg
sudo mv bazel-archive-keyring.gpg /usr/share/keyrings
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/bazel-archive-keyring.gpg] https://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
```

### c. Install Bazel
```bash
sudo apt update && sudo apt install bazel-3.1.0
```

### d. Create a symbolic link for Bazel
```bash
sudo ln -s /usr/bin/bazel-3.1.0 /usr/bin/bazel
```

## 5. Clone the TensorFlow repository
```bash
git clone https://github.com/tensorflow/tensorflow.git
```
## 6. Change directory to the TensorFlow repository
```bash
cd tensorflow
```

## 7. Checkout the desired TensorFlow version
```bash
git checkout v2.4.1
```

## 8. Configure TensorFlow build
```bash
./configure
```

Answer the prompts as follows:
- Do you wish to build TensorFlow with ROCm support? [y/N]: `N`
- Do you wish to build TensorFlow with CUDA support? [y/N]: `N`
- Do you wish to download a fresh release of clang? (Experimental) [y/N]: `N`
- Please specify optimization flags to use during compilation when bazel option "--config=opt" is specified [Default is -Wno-sign-compare]: `-msse -msse2 -msse3 -mno-ssse3 -mno-sse4.1 -mno-sse4.2 -mno-avx -mno-avx2 -mno-fma -mno-avx512f`
- Would you like to interactively configure ./WORKSPACE for Android builds? [y/N]: `N`

## 9. Build and install TensorFlow
### a. Build TensorFlow
```bash
bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package
```

### b. Create the pip package
```bash
./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

### c. Install the TensorFlow pip package
```bash
pip install /tmp/tensorflow_pkg/tensorflow-<version>-<additional_information>.whl
```

## In-between builds (if something goes wrong)
```bash
bazel clean --expunge
```
