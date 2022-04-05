# 2019 HYPERSPECTRAL IMAGE SUPER-RESOLUTION USING GENERATIVE ADVERSARIAL NETWORK AND RESIDUAL LEARNING

[toc]

## Information

* 论文期刊：International Conference on Acoustics, Speech, and Signal Processing (ICASSP)
* 论文链接：[link](https://ieeexplore.ieee.org/abstract/document/8683893)

## Comments

* 文章针对高光谱图像的超分，提出了GAN方法，使用残差学习;
* 个人觉得这里面最主要的就是在生成网络部分使用了梯度特征进行学习，与初始的生成网络进行结合，能够提供更好的空间保真度，并取消了VGG网络结构；

## Abstract

Due to the limitation of image acquisition, hyperspectral remote sensing imagery is hard to reflect in both high spatial and spectral resolutions. Super-resolution (SR) is a technique which can improve the spatial resolution. Inspired by recent achievements in deep convolutional neural network(CNN) and generative adversarial network (GAN), a GAN based framework is proposed for hyperspectral image super-
resolution. In the proposed method, residual learning is used to obtain a high metrics and spectral fidelity, and a shorter connection is set between the input layer and output layer. The gradient features from low-resolution (LR) image to high-resolution (HR) are utilized as auxiliary information to assist deep CNN to carry out counter training with discriminator. Experimental results demonstrate that the proposed SR algorithm achieves superior performance in spectral fidelity and spatial resolution compared with baseline methods.

针对高光谱图像超分，提出了GAN网络方法，应用残差学习获取高指标和频谱保真度，输入层和输出层之间设置shorter connection；从低分辨率到高分辨率的梯度特征作为辅助信息帮助CNN和鉴别器进行反训练

## Introduction

针对高光谱图像超分提出了一种基于GAN的先进网络框架；

所提出的网络基于SRCNN进行改进(这里是不是有点旧了；)，加深网络，引用残差网络的结构；生成网路的部分和SRGAN相似，去掉了pixel shuffle layer，更深的网络结构和残差结构更够得到更好的指标和图像光谱保真度；为了得到更好的空间感知质量，不再采用VGG损失函数，因为这在高光谱图像中可能会产生一些虚假的细节；而是开发一个梯度学习网络，将梯度特征传输到生成网络中恢复细节；

生成器部分：上面部分是采用了残差结构的SRCNN网络部分，下面是设计的梯度学习网络，梯度应该就是中间学习到的特征图，两个网络中间学习到的特征图进行融合；

鉴别器部分：右边，将预测的HR图像与原始的HR图像，损失函数就是普通的GAN网络的损失函数；

![Untitled](2019%20HYPER%20da9a1/Untitled.png)

![Untitled](2019%20HYPER%20da9a1/Untitled%201.png)

实验在可见光和近红外上进行的；