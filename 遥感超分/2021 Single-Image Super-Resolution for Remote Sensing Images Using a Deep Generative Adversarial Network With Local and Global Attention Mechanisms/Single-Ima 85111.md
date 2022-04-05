# 2021 Single-Image Super-Resolution for Remote Sensing Images Using a Deep Generative Adversarial Network With Local and Global Attention Mechanisms

[toc]

## Information

* 论文期刊：IEEE Transactions on Geoscience and Remote Sensing
* 论文链接：[link](https://ieeexplore.ieee.org/abstract/document/9479919)

## Comments

* 整篇文章的结构还是挺复杂的，每个block中都有residual learning、densenet、local attention，结构中只有最后有一个global attention和short-cut connection；
* 文章的结构其实与ESRGAN十分类似，这或许也反映了一定的趋势，好多超分网络是在ESRGAN的基础上进行修改的，对block进行添加，然后堆叠block；这种思路看起来比较简单，其实如何做到能够有效提升指标还是挺难的，特别是需要在感知指标上有较大的提升，不然指标提升了目视效果没什么改进那也难以应用；

## Abstract

> Super-resolution (SR) technology is an important way to improve spatial resolution under the condition of sensor hardware limitations. With the development of deep learning(DL), some DL-based SR models have achieved state-of-the-art performance, especially the convolutional neural network (CNN). However, considering that remote sensing images usually contain a variety of ground scenes and objects with different scales, orientations, and spectral characteristics, previous works usually treat important and unnecessary features equally or only apply different weights in the local receptive field, which ignores long-range dependencies; it is still a challenging task to exploit features on different levels and reconstruct images with realistic details. To address these problems, an attention-based generative adversarial network (SRAGAN) is proposed in this article, which applies both local and global attention mechanisms. Specifically, we apply local attention in the SR model to focus on structural components of the earth’s surface that require more attention, and global attention is used to capture long-range interdependencies in the channel and spatial dimensions to further refine details. To optimize the adversarial learning process, we also use local and global attentions in the discriminator model to enhance the discriminative ability and apply the gradient penalty in the form of hinge loss and loss function that combines L1 pixel loss, L1 perceptual loss, and relativistic adversarial loss to promote rich details. The experiments show that SRAGAN can achieve performance improvements and reconstruct better details compared with current state-of-the-art SR methods. A series of ablation investigations and model analyses validate the efficiency and effectiveness of our method.
> 

正如文章标题中描述的一样，文章中主要使用了Local Attention和Global Attention，摘要中说明在generator和discriminator中添加local、global attention mechanisms；

## Introduction

> remote sensing images contain a variety of ground scenes and objects with different scales, orientations and spectral characteristics, and the small-scale objects with fine details, and those large-scale
objects with rough texture are usually processed equally by most previous CNN-based models, which limit the ability of models in reconstructing realistic HR images with rich texture details.
> 

遥感影像具有更复杂的背景，目标大小、角度以及光谱信息都会有差距；

1) We propose an attention-based SR model for SISR of remote sensing images, which applies both local and global attention mechanisms. Local attention can help the model focus on important channels and regions to promote perceptually realistic textures for multiscale scenes, and global attention is used to capture long-range interdependencies in the channel and spatial dimensions to refine the reconstructed details.
2) Under the adversarial learning framework, local and global attention blocks (GABs) are used in the discriminator model to enhance discriminative ability; we combine the L1 pixel loss, the L1 perceptual loss, and the adversarial loss to constrain different aspects of the SR process and apply relativistic adversarial loss and gradient penalty in the form of hinge loss to optimize the adversarial learning process.
3) We train our method using a large number of diverse remote sensing images and evaluate its performance on different classes of images. SRAGAN performs better than the state-of-the-art CNN-based methods. We explored the impact of different ways of applying attention blocks, pooling operation in local attention, different noise levels, multiple loss functions, and adversarial learning algorithms.

文章的主要贡献分为三点：1) 提出一种采用local attention 和 global attention的SISR方法；2) 在generator和discriminator中都采用local attention 和 global attention，并结合了GAN中常见的损失，L1 pixel loss、L1 perceotual loss and adversarial loss；3) 实验证明方法先进；

## Related Work

这部分没啥注意的；

## Methodology

网络结构十分明了，采用了RDAB块，这个与之前的RDB进行比较的话，主要差别是添加了local attention模块；

![Untitled](Single-Ima%2085111/Untitled.png)

那么上面的RDAB模型如下：

如图中我写的笔记，每个block中都使用了local attention， 先channel attention， 后接spatial attention

![Untitled](Single-Ima%2085111/Untitled%201.png)

那么attention模块，无论是channel还是spatial attention，都在下图中：

channel attention是卷积到1*1的大小，那么里面的每个值就表示每个通道的重要性；spatial attention获取的结果最后就只有一个通道；这里采用了两种池化方法，一般之前都是使用的avgpool，这里文章中提到采用maxpool能够获取更多的细节信息；

![Untitled](Single-Ima%2085111/Untitled%202.png)

## Experiments

数据集：RSCNN7、NWPU-RESISC、AID、DOTA dataset、UCMERCED

低分辨率影像由原始影像下采样得到；

> all the selected images are randomly cropped and rotated, and we get corresponding LR images by blurring, down-sampling using the bicubic interpolation method, and adding the Gaussian noise on HR samples
> 

评价指标：MSE、PSNR、SSIM、LPIPS、ERGAS

LPIPS是一种感知评价指标，ERGAS在MSE的基础上考虑到了放大倍数的影响；

需要注意的是最后的实验结果中：

从指标上来看，这篇文章中的特征注意力机制和通道注意力机制对指标的提升十分明显，目视效果上差别不大；指标上LPIPS指标每次都低于ESRGAN，感知评价指标，这在一定程度上说明该方法在感知质量上结果并不如ESRGAN；