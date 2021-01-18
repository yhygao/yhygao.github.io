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


## Abstract

Transformer由于能够较好的捕捉序列中远距离的关系，在NLP领域大放异彩。近期，也有vision领域也有许多关于Transformer的工作。Transformer的基本模块是self-attention module，而self-attention在vision领域已经热过一阵子了，有很多有影响力的工作 [<sup>1</sup>](#refer-anchor-1) [<sup>2</sup>](#refer-anchor-2)。但是这些self-attention都存在一些问题，比如计算量过大，导致整个网络一般只有在降采样到最小分辨率之后，才使用一层self-attention来捕捉long-range的关系。如果想将Transformer应用到Vision领域，这个问题是需要解决的。本论文就是一个尝试，它提出了两种self-attention module： pairwise self-attention，patchwise self-attention。

## Introduction











<div id="refer-anchor-1"></div>
- [1] [Non-local Neural Networks] (https://arxiv.org/abs/1711.07971)
<div id="refer-anchor-2"></div>
- [2] [Dual Attention Network for Scene Segmentation] (https://arxiv.org/abs/1809.02983)