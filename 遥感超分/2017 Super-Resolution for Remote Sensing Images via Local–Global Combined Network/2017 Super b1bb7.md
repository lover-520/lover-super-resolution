# 2017 Super-Resolution for Remote Sensing Images via Local–Global Combined Network

[toc]

## Information

* 论文期刊：IEEE Geoscience and Remote Sensing Letters
* 论文链接：[link](https://ieeexplore.ieee.org/abstract/document/7937881)

## Comments

* 文章中规中矩吧，目前来看这种思路已经明显过时了，无非就是不同级别的特征图的一个累加;

## Abstract

> Super-resolution is an image processing technology that recovers a high-resolution image from a single or sequential low-resolution images. Recently deep convolutional neural networks (CNNs) have made a huge breakthrough in many tasks including super-resolution. In this letter, we propose a new single-image super-resolution algorithm named **local–global combined networks (LGCNet)** for remote sensing images based on the deep CNNs. Our LGCNet is elaborately designed with its “multifork” structure to learn multilevel representations of remote sensing images including both local details and global environmental priors. Experimental results on a public remote sensing data set (UC Merced) demonstrate an overall improvement of both accuracy and visual performance over several state-of-the-art algorithms
>  

提出了一种单图像超分算法，局部全局结合(听起来感觉像是多尺度信息结合)；

## Network

文章网络结构十分简单

分为三部分：representation、combination、reconstruction

representatation部分网络可以任意，从中选取三个不同层次的卷积层，在combination部分执行concat操作即可；

![Untitled](2017%20Super%20b1bb7/Untitled.png)

文章比较的方法十分普通，Bicubic、SRCNN、FSRCNN、VDSR；

数据集是UC Merced

这里可以注意到里面可以比较不同类之间的PSNR指标，有的类别的超分效果相对而言比较好，因为这些类别的图像相对而言更为光滑；

在高分2号卫星影像上定性地进行了效果比较；