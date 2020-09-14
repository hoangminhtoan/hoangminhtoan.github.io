---
layout: post
subtitle: Seprable Convolutions
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
last_modified_at: 2020-08-11 13:58:00 +0000
share-img: /assets/img/path.jpg
tags: [deep-learning]
---

There are two main types of seperable convoltuions: 
 * [Spatial separable convolutions](#spatial-separable-convolutions)
 * [Depthwise separable convolutions](#depthwise-separable-convolutions)


## Spatial Separable Convoltuions
The spatial separable convoltuion deals primarily with the **spatial dimenstions** of an image and kernel: the height and width.
<br>
A spatial separable convolution simply divides a kernel into two, smaller kernels. For examples, 3x3 -> 3x1 and 1x3. And thus, instead of using 3x3=9 multiplications, we only use 3x1+1x3=6 multiplications => computational complexity goes down, and the network is able to run faster.

<p align="center">
    <img alt="Sperable Conv" src="../../../assets/img/posts/deep-learning/spatial_separable_convs.png">
    <br>
        <em>Figure 1. Separable Convolutions</em>
</p>


One of the most famous convolutions that can be separated spatially is the Sobel kernel, used for edges detection

![Sobel kernel](../../../assets/img/posts/deep-learning/sobel_kernel.png "Sobel kernel")
<p align="center"><em>Figure 2. Separating the Sobel kernel</em></p>

**However,** the main issue with the spatial separable convolution is that not all kernels can be "separated" into two, smaller kernels. This becomes particularly bothersome during training, since of all the possible kernels the network could have adopted, it can only end up using one of the tiny portion tha can be separated two smaller kernels.

## Depthwise Separable Convoltuions
Unlike spatial separable convoltuions, depthwise separable convolutions work with kernels that cannot be "factored" into two smaller kernels.<br>
The depthwise separable convolution deals not only with the spatial dimensions, but also with the depth dimension (the number of channels). <br>
Similar to the spatial separable convolution, a depthwise separable convolution splits a kernel into 2 separate kernels that do two convolutions:
 * [The Depthwise Convolution](#the-depthwise-covolution)
 * [The Pointwise Convolution](#the-pointwise-convolution)

### Normal Convolution
![Normal Conv](../../../assets/img/posts/deep-learning/normal_conv.png)
<p align="center"><em>Figure 3. A Normal Convolution</em></p>

### The Depthwise Convolution
In depthwise convolution, we use each filter channel only at one input channel. In the example, we have 3 channel filter and 3 channel image, then we break the filter and image into three different channels and convolve the corresponding image with corresponding channel and then tack them back.

|-|-|
|---|---|
|![](../../../assets/img/posts/deep-learning/depthwise_conv.png)|![](../../../assets/img/posts/deep-learning/depthwise_conv_2.png)|
----
<p algin="center"><em>Figure 4. A Depthwise Convolution</em>
</p>

Each 5x5x1 kernel iterates 1 channel of the image (note: **1 channel**, not all channels), getting the scalar products of every 25 pixel group, giving out a 8x8x1 image. Stacking these images together creates a 8x8x3 image.

### The Pointwise Convolution
