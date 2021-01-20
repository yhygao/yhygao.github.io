---
layout:     post
title:      Exploring Self-attention for Image Recognition
subtitle:   论文笔记
date:       2021-01-18
author:     Yunhe
header-img: img/post_img/vision_transformer/post-bg-transformer.jpg
catalog: true
tags:
    - Vision Transformer
    - Computer Vision
    - Paper Reading
---


<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

## Prologue

Transformer由于能够较好的捕捉序列中远距离的关系，在NLP领域大放异彩。近期，vision领域也有许多关于Transformer的工作。Transformer的基本模块是self-attention module，而self-attention在vision领域已经热过一阵子了，有很多有影响力的工作 [<sup>1</sup>](#refer-anchor-1) [<sup>2</sup>](#refer-anchor-2)。但是这些self-attention都存在一些问题，比如计算量过大，导致整个网络一般只有在降采样到最小分辨率之后，才使用一层self-attention来捕捉long-range的关系。如果想将Transformer应用到Vision领域，这个问题是需要解决的。本论文就是一个尝试，它提出了两种self-attention module： pairwise self-attention，patchwise self-attention。

## Introduction

卷积神经网络在视觉领域近些年有革命性的进展，对于image recognition有一系列网络模型上的突破，从GoogLeNet，VGG，ResNet，DenseNet，SENet等等。这些模型都是基于卷积的。卷积的操作从数学上可以写为：$ F*k(p)=\sum_{s+t=p} F(s)k(t) $，其中F是图片，k是卷积核。通常认为一个卷积核对某个特定的特征会有较高的响应值，卷积核以滑动窗口的形式，在图片上提取特征，因此卷积神经网络拥有平移不变性。但由于卷积核的尺寸和形状都是固定的，比如大多是固定的正方形3\*3，5\*5的，所以不具有旋转不变性。同时固定的卷积核也不能适应图片内容。这个问题在网络浅层可能不是很严重，因为浅层主要是提取基础特征。但是在深层就比较严重了，因为深层主要是语义信息，比如说一个汽车，如果卷积核能够根据根据图片的content，按照一个汽车的形状去从临近像素aggregate信息，那么就会得到更准确的特征。Deformable convolution[<sup>3</sup>](#refer-anchor-3) 的一系列文章就在尝试着解决这个问题。

在这个论文里，作者提出了两种self-attention operator。第一种是**pairwise self-attention**，其实就是NLP中点乘attention在图像领域的拓展，也就是图像领域之前常用的attention。它是通过每个像素的feature，计算pixel-wise的similarity matrix。这样其实就是只跟图像的特征有关，具有平移旋转等permutation的不变性。同时能够极大的提高感受野，在全图范围aggregate信息。第二种是**patch-wise self-attention**，并claim这是一种严格优于convolution的operator。


self-attention的一个大的问题是显存占用和计算量的问题，要计算每个像素的pair-wise attention map，计算量和存储大矩阵都是与feature map维度成平方关系的，对于浅层大分辨率的特征图是扛不住的。Stand-alone self-attention[<sup>4</sup>](#refer-anchor-3) 提出了在local path中，如7\*7，使用self-attention，这样能够解决计算量和现存的问题，使得self-attention能够应用在整个网络中。


## Method

作者将卷积神经网络层的功能分为了两种：feature aggregation和feature transformation。所谓feature aggregation就是将前面一层的feature收集起来，transformation就是通过线性和非线性映射将特征映射到更高维的空间，增加拟合能力。transformation在transformer里面就是用feedforward pereceptron+非线性激活函数来做的。因此本文focus在feature aggregation这一步。

传统卷积操作是通过固定的卷积核和训练好的参数从附近像素中提取特征。这个卷积核weights和卷积核覆盖的范围都是固定不变的，不会根据图片的内容而变化。作者提出了新的feature aggregation方法（via self-attention），和feature transformation（via elementwise perceptrons）。

### Pairwise Self-attention

$ y_i = \sum_{j\in R(i)} \alpha(x_i, x_j) \odot \beta(x_j) $

这个就是之前常用的self-attention的形式的一个抽象，唯一的区别就是这里并不是全图aggregate，而是限制在区域$R(i)$中。$\beta(x_j)$是经过transform的特征。$\alpha(x_i, x_j)$为aggregate所需要的矩阵，它包含了从区域$R(i)$中每个像素aggregate信息的权重。$\alpha$ function可以有很多种选择，文章里尝试了summation，subtraction，concatenation，Hadamard product和Dot product。self-attention是完全从feature角度来的，忽略掉了位置信息，因此文章里也加入了position encoding来补充位置信息。

### Patchwise Self-attention

其实这里没怎么看懂








<div id="refer-anchor-1"></div>
- [1] [Non-local Neural Networks] (https://arxiv.org/abs/1711.07971)
<div id="refer-anchor-2"></div>
- [2] [Dual Attention Network for Scene Segmentation] (https://arxiv.org/abs/1809.02983)
<div id="refer-anchor-3"></div>
- [3] [Deformable Convolutional Networks] (https://arxiv.org/abs/1703.06211)
<div id="refer-anchor-4"></div>
- [4] [Stand-alone self-attention in vision models] (https://arxiv.org/abs/1906.05909)
