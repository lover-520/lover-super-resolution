# 2018 Hyperspectral and Multispectral Image Fusion via Deep Two-Branches Convolutional Neural Network

[toc]

## Information

* 论文期刊：remote sensing
* 论文链接：[link](https://www.mdpi.com/2072-4292/10/5/800/htm?ref=https://githubhelp.com)

## Comments

* 采用双分支的方法进行了HSI和MSI影像融合以提高HSI分辨率;
* 个人觉得这个创新点主要在于提取HSI和提取MSI的特征所采用特征提取方式是不一样的，提取HSI特征时是从一维卷积的角度进行的，但是这不与自动编码器差不多了嘛；提取MSI影像的特征是与普通的二维卷积类似；

## Abstract

> Enhancing the spatial resolution of hyperspectral image (HSI) is of significance for applications. Fusing HSI with a high resolution (HR) multispectral image (MSI) is an important technology for HSI enhancement. Inspired by the success of deep learning in image enhancement, in this paper, we propose a HSI-MSI fusion method by designing a deep convolutional neural network (CNN) with two branches which are devoted to features of HSI and MSI. In order to exploit spectral correlation and fuse the MSI, we extract the features from the spectrum of each pixel in low resolution HSI, and its corresponding spatial neighborhood in MSI, with the two CNN branches. The extracted features are then concatenated and fed to fully connected (FC) layers, where the information of HSI and MSI could be fully fused. The output of the FC layers is the spectrum of the expected HR HSI. In the experiment, we evaluate the proposed method on Airborne Visible Infrared Imaging Spectrometer (AVIRIS), and Environmental Mapping and Analysis Program (EnMAP) data. We also apply it to real Hyperion-Sentinel data fusion. The results on the simulated and the real data demonstrate that the proposed method is competitive with other state-of-the-art fusion methods.
> 

加强高光谱图像HSI的空间分辨率具有重要的意义，将多光谱图像MSI和HSI进行融合是一项重要的技术；鉴于深度学习的广泛应用，提出了一种HSI-MSI融合方法，设计了一种具有两个分支的CNN网络分别表示HSI和MSI图像的特征；

## Introduction

> Inspired by the success of CNN in single image enhancement, in this study, we propose a deep CNN with a two-branch architecture for the fusion of HSI and MSI. In order to exploit the spectral correlation of HSI and fuse the MSI, the spectrum of LR HSI and the corresponding spatial neighborhood in HR MSI is used as input pair of the network. We extract the features from the spectrum of LR HSI and the corresponding neighborhood in MSI with the two CNN branches. In order to fully fuse the information extracted from HSI and MSI, the extracted features of the two branches are concatenated and then fed to fully connected (FC) layers. The final output of the FC layers is the spectrum of the expected HR HSI.
> 

考虑到CNN在单图像增强上的成功应用，提出一种具有两个分支结构的深层CNN，用于HSI和MSI的融合；

三个贡献点：

• We propose learning the mapping between LR and HR HSIs via deep learning, which is of highlearning capacity, and is suitable to model the complex relationship between LR and HR HSIs.
• We design a CNN with two branches extracting the features in HSI and MSI. This network could exploit the spectral correlation of HSI and fuse the information in MSI.
• Instead of reconstructing HSI in band-by-band fashion, all of the bands are reconstructed jointly, which is beneficial for reducing spectral distortion.

1. 提出了一种通过深度学习在HR HSI和LR HSI中建立映射关系的方法；
2. 设计了一个双分支CNN，两个分支提取HSI和MSI中的特征，该网络利用HSI中的光谱相关性，融合MSI中的信息；
3. 不是通过对每个波段的方式重建HSI，而是联合重建所有频带，有利于减少频谱失真；

## Network

![Untitled](2018%20Hyper%20f8cc0/Untitled.png)

上面的分支是提取HSI特征的，先将HSI上采样到和MSI一样大小；

对HSI中每个pixel，得到spectrum，然后转换到一维空间上，通过一维卷积的方式提取特征；对MSI中那个pixel的邻近区域，通过卷积层提取特征；

两个分支提取的特征然后concat，通过全连接层继续提取特征，得到HR HSI中的对应pixel的各个频谱的值；