---
layout: post
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
last_modified_at: 2020-12-22 13:58:00 +0000
tags: [misc, CUDA, Pytorch]
---

A beginner-friendly solution walkthrough for this frustrating (and common) error in PyTorch

***What is the Error?***  

This error occurs due to the following two reasons: 

1. Inconsistency between the number of labels/classes and the number of output units
2. The input of the loss function may be incorrect.  

Let’s unpack these reasons and their solutions below:

## 1. Inconsistency between the number of labels/classes and the number of output units
When defining the final fully connected layer of my model, instead of putting 196(total number of classes for the Stanford car dataset) as the number of output units, I put 195.  
The error is usually identified in the line where you do the backpropagation. Your loss function will be comparing the output from your model and the label of that observation in your dataset. Just in case you are confused between labels and output, see how I define them below:  
**Label**: This is the tags associated with an observation. When working on a classification problem, the label is the class. For example, in the classic dog vs cat problem, the labels are cat and dog.  
**Output**: This is the predicted ‘label’ from your model. You give your model a set of features from an observation and it gives out a prediction called output in the PyTorch ecosystem. Think of it as a predicted label.  
In my case, some of the labels will have a value 195 which is beyond the range of output for my model whose greatest possible value is 194(Start counting from zero). This causes the error to be triggered.

** How to fix it?**
>> Make sure the number of output units match the number of classes

## 2. The input of the loss function may be incorrect
Loss functions have different ranges for the possible inputs that they can accept. If you choose an incompatible activation function for your output layer this error will be triggered. For example, BCELoss requires its input to be between 0 and 1. If the input(output from your model) is beyond the acceptable range for that particular loss function, the error gets triggered.  
**Recap on activation loss functions**
Activation functions are the mathematical equations that determine the output of your neural network. The purpose of the activation function is to **introduce non-linearity** into the output of a model thus making a model capable to learn and perform more complex tasks. They, in turn, determine how accurate your network gets to be.  
Loss functions are the equations that compute the error that is used to learn by means of *backpropagation*.
For a detailed explanation of loss functions and how they work, please check out this [article](https://medium.com/udacity-pytorch-challengers/a-brief-overview-of-loss-functions-in-pytorch-c0ddb78068f7) and the [Pytorch documentation](https://pytorch.org/docs/stable/nn.html#loss-functions). Find information about [activation function here](https://www.deeplearningwizard.com/deep_learning/boosting_models_pytorch/weight_initialization_activation_functions/).

### Reference
* https://towardsdatascience.com/cuda-error-device-side-assert-triggered-c6ae1c8fa4c3