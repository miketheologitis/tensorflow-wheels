# TensorFlow Wheels

This repository contains pre-built wheel files for TensorFlow.

## Compatibility

The following table lists the TensorFlow versions, hardware configuration, Python version, CUDA version, supported (and not supported) instructions, supported operating systems, and download link for each wheel (from inside this repository):

| TF version | Hardware | Python version | CUDA version | Supported instructions | Not Supported instructions | OS | Download link |
| ---------- | -------- | -------------- | ------------ | ---------------------- | -------------------------- | -- | ------------- |
| 2.12.0 | CPU | 3.9 | - | SSE, SSE2, SSE3 | SSE4.1, SSE4.2, AVX, AVX2, AVX512F, FMA, (SSSE3) | Ubuntu x86_64 18.04+ | [Download](https://github.com/miketheologitis/tensorflow-wheels/raw/main/wheels/2.12.0/py39/CPU/SSE_SSE2_SSE3/tensorflow-2.12.0-cp39-cp39-linux_x86_64.whl) |
| 2.12.0 | CPU | 3.9 | - | SSE, SSE2 | SSE3, SSE4.1, SSE4.2, AVX, AVX2, AVX512F, FMA, (SSSE3) | Ubuntu x86_64 18.04+ | [Download](https://github.com/miketheologitis/tensorflow-wheels/raw/main/wheels/2.12.0/py39/CPU/SSE_SSE2/tensorflow-2.12.0-cp39-cp39-linux_x86_64.whl) |
| 2.4.1 | CPU | 3.8 | - | SSE, SSE2, SSE3 | SSE4.1, SSE4.2, AVX, AVX2, AVX512F, FMA, (SSSE3) | Ubuntu x86_64 18.04+ | [Download](https://github.com/miketheologitis/tensorflow-wheels/raw/main/wheels/2.4.1/py38/CPU/SSE_SSE2_SSE3/tensorflow-2.4.1-cp38-cp38-linux_x86_64.whl) |
| 2.4.1 | CPU | 3.8 | - | SSE, SSE2 | SSE3, SSE4.1, SSE4.2, AVX, AVX2, AVX512F, FMA, (SSSE3) | Ubuntu x86_64 18.04+ | [Download](https://github.com/miketheologitis/tensorflow-wheels/raw/main/wheels/2.4.1/py38/CPU/SSE_SSE2/tensorflow-2.4.1-cp38-cp38-linux_x86_64.whl) |

## Installation

1. Choose your preferred build (wheel file) from the table above and download it using the provided link.

2. Create enviroment with the python version that matches the build.
```bash 
conda create --name * python=X.Y
```
```bash 
conda activate *
```

3. Using `pip` install the built tensorflow from the `.whl` file you downloaded.
```bash 
pip install *.whl 
```

4. Verify the installation
```bash
python -c "import tensorflow as tf; print(tf.__version__);"
```
```bash
python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])));"
```
