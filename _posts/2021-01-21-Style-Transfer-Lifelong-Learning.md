---
layout:     post
title:      Style Transfoer and Lifelong Learning
subtitle:   论文笔记
date:       2021-01-18
author:     Yunhe
header-img: img/post_img/vision_transformer/post-bg-transformer.jpg
catalog: true
tags:
    - Computer Vision
    - Paper Reading
---

最近看了几篇论文，好像把很久以来的思路理顺了。这里总结一下这一系列的论文，并把思路整理一下。


最初的style transfer的论文，Gatys通过神经网络中间特征的Gram矩阵来描述style特征，并通过optimization来迭代优化。后面出现了image-to-image translate来使用了feed-forward网络来实现图片对儿的风格迁移，以及类似cycle-GAN的两个domain的unpair风格迁移。