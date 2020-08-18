---
layout: post
subtitle: Object Detectors
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [computer-vision, deep-learning, object-detector]
---

![Object Detector](../../../assets/img/posts/computer-vision/yolov4_1.png)

All object detectors take an image in for **input** and compress features down through a convolutional neural network **backbone**. 
 * In image classification, these backbones are the end of the network and prediction can be made off of them.
 * In object detection, multiple bounding boxes need to be drawn around images along with classification, so the feature layers of the convolutional backbone need to be mixed and help up in light of one another.

The combination of backbone feature layers happens in **the neck.**

It is also useful to split object detectors into two categories: 
 * One-stage detectors: make the predictions for object localization and classification at the same time.
 * Two-stage detectors: decouple the task of object localization and classification for each bounding box.

Detection happens in the **head.**




## References:
 * [The anatomy of an object detector](https://blog.roboflow.ai/a-thorough-breakdown-of-yolov4/)
