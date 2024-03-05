+++
title = "MNIST Benchmarks (CPU vs GPU / Tensorflow vs Pytorch)"
date = "2023-08-08"
draft = false
+++

I got ROCm to work on my laptop and guess what that means, benchmarks!

## Hardware

- Form factor: Laptop
- Model: Asus G513QY
- CPU: AMD Ryzen 5900HX (83rd percentile on cpu.userbenchmark.com, ~ 10% slower than a desktop 5500)
- GPU: AMD Radeon 6800m 
(91st percentile on gpu.userbenchmark.com, ~15% slower than a desktop 3060, 1/5th the power of a desktop 4090)

## Tensorflow

### Model Summary

```
Model: "sequential"
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 conv2d (Conv2D)             (None, 26, 26, 32)        320

 conv2d_1 (Conv2D)           (None, 24, 24, 64)        18496

 max_pooling2d (MaxPooling2D  (None, 12, 12, 64)       0
 )

 dropout (Dropout)           (None, 12, 12, 64)        0

 flatten (Flatten)           (None, 9216)              0

 dense (Dense)               (None, 128)               1179776

 dense_1 (Dense)             (None, 10)                1290

=================================================================
Total params: 1,199,882
Trainable params: 1,199,882
Non-trainable params: 0
_________________________________________________________________

```

Code can be found [here](https://gist.github.com/berinaniesh/7028945386613c76e80dca02ab060350)

### CPU

![CPU TF](/cpu_mnist_tf.png)

Took 654 seconds (10 minutes, 54 seconds).

### GPU

![GPU TF](/gpu_mnist_tf.png)

Took 63 seconds (1 minute, 3 seconds).

## Pytorch

### Model Summary

```
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 32, 26, 26]             320
            Conv2d-2           [-1, 64, 24, 24]          18,496
           Dropout-3           [-1, 64, 12, 12]               0
            Linear-4                  [-1, 128]       1,179,776
           Dropout-5                  [-1, 128]               0
            Linear-6                   [-1, 10]           1,290
               Net-7                   [-1, 10]               0
================================================================
Total params: 1,199,882
Trainable params: 1,199,882
Non-trainable params: 0
----------------------------------------------------------------

```

Code can be found [here](https://github.com/pytorch/examples/blob/main/mnist/main.py)

### CPU

![CPU](/cpu_mnist_torch.png)

Took 458 seconds (7 minutes 38 seconds).

### GPU

![GPU](/gpu_mnist_torch.png)

Took 110 seconds (1 minute, 50 seconds).

## CPU usages compared

Measured during CPU runs.

### Tensorflow

![CPU usage TF](/cpu_usage_tf.png)

Load Average: 11.4

### Pytorch

![CPU usage torch](/cpu_usage_torch.png)

Load Average: 7.05

## Inference

- Tensorflow GPU is about 10 times faster than Tensorflow CPU (654 vs 63 seconds).
- Pytorch GPU is about 4 times faster than Pytorch CPU (458 vs 110 seconds).
- Pytorch CPU is about 1.4 times faster than Tensorflow CPU (654 vs 458 seconds).
- Tensorflow GPU is about 1.7 times faster than Pytorch GPU (110 vs 63 seconds)
- Tensorflow is much harder on the CPU than Pytorch (11.4 vs 7.05 load average).

## Conclusions / Recommendations

_Disclaimer: Everything is based on a few runs on my machine with ROCm. 
Results could wildly vary for other use cases._

- A GPU can greatly speedup workflows.
  - Even cheaper graphics cards help.
  - This is due to GPUs' parallel architecture and being better optimized for lower precision calculations and matrix multiplications.
- If there is GPU available, use Tensorflow
  - Tensorflow is much faster (1.7 times) than Pytorch with GPU.
- If there is no GPU available, use Pytorch
  - Tensorflow really pounds the CPU (11.4 vs 7.05 load avg) albeit being slow (654 vs 458 seconds).

Let me know if you have suggestions / corrections.

Have a good time ahead!

