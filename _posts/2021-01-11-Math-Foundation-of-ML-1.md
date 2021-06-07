---
layout:     post
title:      Mathematics Foundation of Modern Machine Learning
subtitle:   (1) Introduction
date:       2021-01-11
author:     Yunhe
header-img: img/post-bg-math.jpg
catalog: true
tags:
    - Mathematics
    - Machine Learning
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

# Preface

作为计算机视觉方向的PhD，上来就是从深度学习入的门。尽管各种深度学习模型看起来都很fancy，效果也好，能解决很多问题，但是如果想不仅仅做个魔改模型的调参侠，还是要从传统的解决方案里找思路的。因此想要系统的学习一下机器学习方面的理论知识已经很久了，但是因为很多数学基础已经很久没有使用过了，还需要花些时间来复习线性代数之类课程的知识。这些机器学习理论的内容总是看一些就断掉了，或者需要用到哪些就去看哪些。一直都没有很系统的将不同方法联系梳理起来。而且平时看各种其他人的博客学习，自己也很少输出些知识。想要掌握好某些知识，最好的办法就是当老师来讲解这些东西。因为只有熟练的掌握了这些知识，才能给别人讲清楚问题。所以这次趁着假期，将这些理论知识串联起来，并整理成一系列的博客记录一下。

# Introduction

所谓的机器学习，或者说人工智能，是想让计算机拥有智能。
**智能是指一个agent能够观察环境并作出决策行动，达到某种目标。** 
因此AI需要的核心问题包括感知，推理，规划，输出（使用工具或操纵外界的物体），交流等。这里的每一个能力，都是当前AI领域研究的热点问题。

所谓感知(recognition)，就是一个agent收集环境的信息，获取当前的状态。人类能够感知自然界中各种各样的信号，光信号，声信号，温度，湿度，触感等等，并从中获取环境的信息，如自己的位置，周围有什么物体，是否有危险等。人类身体上的各种感受器能够接收这些信号，并将电信号通过神经传递到大脑来处理。对于计算机来说，各种sensor就是他的感受器，而我们所编写的算法就相当于让计算机理解这些信号的大脑。对于我最熟悉的计算机视觉，图像来自各种照相机，或者医学器械如CT，MRI。视觉中的各种任务，无论是分类，分割，检测，定位等等都是想要从图像中找到我们感兴趣的部分，并得到它的信息。感知可以说是AI的基础，或者说第一步，因为只有对自己和周围环境的状态有准确的了解，才能据此推理，规划，以及进一步输出，与外界进行交互。



# Basics

Modern machine learing is driven by data and model, where the model is used to describe data and manipulate data.

## Data representation
Some typical data can be spread sheet, images etc. For example, in the spread sheet, each row of data represent a person, while each collumn represent some kinds of features, e.g. sex, height, weight and other health metrics. Using this way, a dataset can be a spread sheet with thoudsands of such rows. Mathametically, each person can be represented with a **vector**: $\boldsymbol{V}=(v_1, v_2, \dots, v_n)$. Each value can be either real valued vectors (e.g. heights), boolean value (sex), or discrete value (age).

In image perspective, a picture of cat is a $1000\times 1000\times 3$ matrix, which has 3 million dimensions. It is extremely difficult to classify images with such high dimension. One solution is using **embeddings**, a convenient data transformation approach, to embed the high-dimensional data to some low-dimensional space which is easier for classification. For instance, if we can find a function *f*, such that $f(\textbf{V})$ embeds cats in the third quadrant while embeds dogs in the first quadrant, we can easily classify cat vs. dog using a linear classifier. 
<div align=center >
<img src="https://raw.githubusercontent.com/yhygao/yhygao.github.io/master/img/post_img/math_foundation/Catdog.png" width="200" height="200"/>
</div>
But finding a good embedding from high-dimensional data is a difficult task. DNNs are good at learning this kind of representation hierarchically. 
