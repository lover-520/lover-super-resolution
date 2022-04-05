# 2016 Pansharpening by Convolutional Neural Networks

[toc]

## Information

* 论文期刊：remote sensing
* 论文链接：[link](https://www.mdpi.com/2072-4292/8/7/594/pdf)

## Comments

* 一篇作者说是第一次使用深度学习技术进行pansharpen的技术;
* 实话说，个人感觉这篇文章作者对pansharpen的技术很熟悉，但是对深度学习的网络并不是很熟悉；
* 在那个年代这个结果很类似于SRCNN的结构，文章比较久远，算是深度学习在pan-sharpen上的初步应用；

## Abstract

> A new pansharpening method is proposed, based on convolutional neural networks. We adapt a simple and effective three-layer architecture recently proposed for super-resolution to the pansharpening problem. Moreover, to improve performance without increasing complexity, we augment the input by including several maps of nonlinear radiometric indices typical of remote sensing. Experiments on three representative datasets show the proposed method to provide very promising results, largely competitive with the current state of the art in terms of both full-reference and no-reference metrics, and also at a visual inspection.
>  

提出了一种新的全色锐化的方法，基于卷积神经网络，采用一个简单并有效的三层网络架构；为了在不增强复杂度的同时提高精度，引入几种典型的遥感非线性辐射指数图增强输入；

## Introduction

文章主要介绍了以往的在遥感领域pansharpen的做法，分辨率较低的多光谱图像和空间分辨率较高但光谱分辨率较低的全色影像，通过融合操作得到空间分辨率较高，光谱分辨率也较高的图像；

主要做法有component substitution(CS)，翻译为组件替换？将多光谱图像中的某些领域换为高分辨率的全色图像；detail injection，翻译为细节注入？从全色图像中提取细节和上采样之后的多光谱图像进行融合；

pansharpen技术也是一种形式的超分应用；

这篇文章第一次使用深度学习的技术；使用网络2016年提出的超分网络：Image super-resolution using deep convolutional networks

## Network

网络结构十分简单，多光谱图像上采样之后，将全色图像接在后面即可；

![Untitled](2016%20Pansh%205cfc1/Untitled.png)

后面也采用了各种指数作为输入；
