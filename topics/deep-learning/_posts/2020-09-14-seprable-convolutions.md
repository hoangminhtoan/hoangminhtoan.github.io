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
        <em>Separable Convolutions</em>
</p>


One of the most famous convolutions that can be separated spatially is the Sobel kernel, used for edges detection

![Sobel kernel](../../../assets/img/posts/deep-learning/sobel_kernel.png "Sobel kernel")
<p align="center"><em>Separating the Sobel kernel</em></p>

**However,** the main issue with the spatial separable convolution is that not all kernels can be "separated" into two, smaller kernels. This becomes particularly bothersome during training, since of all the possible kernels the network could have adopted, it can only end up using one of the tiny portion tha can be separated two smaller kernels.

## Depthwise Separable Convoltuions
