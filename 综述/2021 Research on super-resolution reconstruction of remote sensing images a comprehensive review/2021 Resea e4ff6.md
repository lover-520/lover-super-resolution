# 2021 Research on super-resolution reconstruction of remote sensing images: a comprehensive review

[toc]

## Information

* 论文期刊：Optical Engineering
* 论文链接：[link](https://www.spiedigitallibrary.org/journals/optical-engineering/volume-60/issue-10/100901/Research-on-super-resolution-reconstruction-of-remote-sensing-images/10.1117/1.OE.60.10.100901.full?SSO=1)

## Comments

* 文章主要介绍超分在遥感影像上的应用，尽管文章中列出的很多文章的确是在遥感影像上应用超分的例子，但是后面进行对比的方法全是计算机视觉初步提出的方法，个人猜测这与遥感影像超分的大部分文章没有提供源码难以复现的现象有关;
* 文章主要介绍超分在遥感影像上的应用，尽管文章中列出的很多文章的确是在遥感影像上应用超分的例子，但是后面进行对比的方法全是计算机视觉初步提出的方法，个人猜测这与遥感影像超分的大部分文章没有提供源码难以复现的现象有关;
* 文章的主要贡献个人感觉仅能提供参考用;

## Abstract

> The super-resolution (SR) reconstruction of remote sensing images is a low-cost and efficient method to improve their resolution, and it is often used for further image analysis. To understand the development of SR reconstruction of remote sensing images and research hotspots and trends, we examined its history and reviewed existing methods categorized into traditional, learning-based, and deep-learning-based methods. To evaluate the reconstruction performance, we conducted experiments comparing various algorithms for the single- and multi-frame SR reconstruction of remote sensing images considering three datasets. The experimental results indicate the advantages and limitations of single- and multi-frame reconstruction, with the latter showing a higher performance. Finally, we provide directions for future development of this SR reconstruction.
>  

将现有的存在的超分方法分为传统的、基于学习的、基于深度学习的；

## Introduction

遥感影像超分具有广泛的应用，具有优点：

> (1) Massive data can be used to train a deep neural network for tasks such as classification under the guidance of user-defined labels.
(2) The increasing capabilities of graphics processors allow processing and optimization in parallel.
(3) Deep neural networks can outperform traditional methods, and the model depth and output size of the image can be adjusted.
>  

大量数据可以用于训练；并行优化；优于传统方法；(这也就最后一个能称之为优点吧)

不足：

> (1) Due to technical and budget constraints, a single-satellite sensor cannot acquire remote sensing images with high spatial and temporal resolution at the same time. Therefore, it is necessary to make effective use of time, space, and spectral correlation for multi-spectral and hyperspectral images from high latitudes.
(2) Remote sensing images mean long-distance observations encoded with a large number of sensors and scene information. Therefore, compared with natural images, remote sensing images contain richer information. Obtaining high-quality remote sensing images and extracting valuable characteristic information from them can provide a basis for remote sensing applications, such as remote sensing image classification applications.
(3) Remote sensing is affected by environmental factors, including atmospheric and weather conditions, which hinder the extraction of valuable information.
(4) Owing to the diversity in sampling methods, resolutions of remote sensing images, and available datasets, deep neural networks can be used to extract rich image information. Although deep learning can provide high performance, the computation burden increases with the complexity of the learning network, and the hardware requirements become prohibitive for practical large-scale applications.
>  

技术和预算限制，单个传感器不可能同时满足时间和空间分辨率，因此需要有效利用时间、空间和光谱信息；获取高质量遥感影像提取有效信息；受环境影像较大；数据量太大，硬件限制；

## Based on Traditional Remote Sensing Image Super-Resolution Reconstruction

Superresolution remote sensing image processing algorithm based on wave-let transform and interpolation(2003) 采用离散小波变换对遥感图像进行分解，然后使用最近邻、双线性或双三次插值对小波系数图像进行插值，然后逆离散小波变换提供相应的SR图像。能够有效保留原始HR图像中的高频信息(图像中的低频信息，低频信号、低频分量指图像中亮度或灰度值变化缓慢的区域，即图像中大片平坦的区域；高频分量即是图像中变化剧烈的部分，图像中边缘(轮廓)部分或者噪声以及细节部分)；Super resolution reconstruction of tm remote sensing image based on wavelet analysis(2016)使用小波分解从高频和低频信息中获取不同尺度的小波系数，获取适合重建图像的权重因子；Achieving super-resolution remote sensing images via the wavelet transform combined with the recursive Res-Net(2019)将小波变换和递归ResNet结构结合；Wavelet transform based image interpolation for remote sensing image(2015)一种基于小波变换的图像插值算法，对双三次插值图像进行处理以保留高频信息；An efficient satellite image super resolution technique for shift-variant images using improved new edge directed interpolation(2018)采用复小波变换提取低频带和高频带，将改进的面向边缘的插值应用于高频子带图像，获取没有伪影的HR图像；

> In the convex set projection method based on reconstruction, the traditional projection on convex sets (POCS) algorithm has contradictions in preserving image details and denoising, which affects the quality of the reconstructed image. In order to avoid this defect and obtain higher resolution, Shang26 introduced the idea of image denoising based on sparse representation on the basis of POCS, combined the image processing method of sparse representation of K-singular value decomposition with the advantages of POCS for image SR reconstruction.
Patti et al.27,28 proposed another method of SR reconstruction of POCS, which took into account the blur factors caused by non-zero aperture time, camera movement, and imaging optical components.
>  
> The reconstruction-based maximum posteriori (MAP) method is more flexible, especially in the regular terms of the MAP method;
>  

凸集投影方法POCS和基于最大后验概率的不咋常见；

基于迭代反投影的SR重建

Super resolution reconstruction of remote sensing image based on high frequency enhancement curve and iterative back projection(2019)采用非锐化掩膜提出初始重建图像的高频分量，进行高频信息分类并减轻噪声，然后使用高频增强曲线增强高频分量。但LR图像中云、大气和其他噪声源引起失真，因此应考虑局部失真。Recovering quantitative remote sensing products contaminated by thick clouds and shadows using multitemporal dictionary learning(2014)中考虑组合算法的迭代反投影，提高弹性配准和图像空间分辨率；Super resolution reconstruction of remote sensing image based on improved iterative back projection algorithm(2019)在遥感影像中提出了一种迭代过程来处理图像错误，并进一步增强图像的高频分量，提高图像重建的质量，以稳定性和鲁棒性反映高频信息。

## Super-Resolution Reconstruction Method Based on Learning

主要是基于图像块之间的字典学习映射；目前这方面的研究已经较少了；

## Super-Resolution Reconstruction of Remote Sensing Image Based on Deep Learning

**BP Neural Network**

BP神经网络需要大量的数据来收敛，目前应用较少；A study on a new method of multi-spatial-resolution remote sensing image fusion based on GA-BP(2007)中采用遗传算法使网络具有更好的收敛能力和更好的学习能力。

**Convolutional Neural Network**

(1) Single-frame remote sensing image SR reconstruction based on CNN

Deep learning for ocean remote sensing: an application of convolutional neural networks for super-resolution on satellite-derived SST data(2016)采用SRCNN在海洋遥感数据上，海面温度场数据，在PSNR指标上取得了不错的效果；**~~Super-resolution for remote sensing images via local-global conbined network(2017)~~**中提出LGCNet，局部全局组合网络，学习遥感数据的多尺度表示，包括局部细节（如物体的边缘和轮廓）和全局先验知识（如环境类型），这是因为在典型的CNN结构中，较低卷积层的神经元共享较小的感受野，更关注局部细节，较高层的神经元具有更大的感受野，覆盖区域更大。

(2) Multi-frame remote sensing image SR reconstruction based on CNN

根据这文章中介绍的，遥感影像中采用多图像超分的方法，一般是针对不同数据源进行的。全色图像具有高空间分辨率，高光谱图像具有高光谱分辨率。~~**Pansharpening by convolutional neural networks(2016)**~~针对高光谱分辨率的多光谱图像和高空间分辨率的全色图像，采用一种三层CNN结构，使用特征融合的方式生成高空间分辨率的多光谱图像；**~~FusionCNN: a remote sensing image fusion algorithm based on deep convolutional neural networks(2019)~~**考虑多光谱图像中的空间信息，在处理前利用可用的纹理信息来增强全色图像的空间分辨率，从而提高生成图像的空间分辨率。**~~Multispectral and hyperspectral image fusion using a 3-D-convolutional neural network(2017)~~**中使用3D CNN融合高光谱和全色图像生成具有高空间分辨率的高光谱图像。**~~Hyperspectral and multispectral image fusion via deep two-branches convolutional neural network(2018)~~**使用双分支CNN分别提取高光谱和多光谱图像的光谱和空间特征。

**Generative Adversarial Network**

(1) Single-frame remote sensing image SR reconstruction based on GAN

**~~Achieving super-resolution remote sensing images via the wavelet transform combined with the recursive Res-Net(2019)~~**中改进了SRGAN，并删除部分组件减小内存需求和加快计算速度；**~~Hyperspectral image super-resolution using generative adversarial network and residual learning(2019)~~**对SRGAN进行改进，扩展更深的结构和引入残差块；

(2) Multi-frame remote sensing image SR reconstruction based on GAN

**~~PSGAN: a generative adversarial network for remote sensing image PAN-sharpening(2020)~~**第一次使用双分支融合作为生成器，全卷积网络作为鉴别器，扩区了具有高空间分辨率的多光谱图像；Residual encoder-decoder conditional generative adversarial network for pansharpening(2019)中采用编码解码的结构用于GAN中；PAN-GAN: an unsupervised PAN-sharpening method for remote sensing image fusion(2020)中使用最小二乘GAN作为基本模型和无监督学习，对生成的图像采用光谱鉴别器和空间鉴别器，同时反映多光谱图像的光谱分辨率和全色图像的空间分辨率；

**Deep Dense Convolutional Network**

Super-resolution of single remote sensing image based on residual dense backprojection networks(2019)中采用残差密集反投影网络针对单帧图像超分辨率。

**Deep Residual Network**

(1) SR reconstruction of single-frame remote sensing image based on deep residual network

Super-resolution reconstruction of remote sensing image based on recursive residual network(2019)提出了一种基于递归残差网络的遥感图像SR重建算法；

(2) Multi-frame remote sensing image SR reconstruction based on deep residual network

PCDRN: progressive cascade deep residual network for pansharpening(2020)通过级联两个残差学习从LR多光谱和全色图像到HR多光谱的非线性特征图;Deep residual learning for boosting the accuracy of hyperspectral pansharpening(2019)首次使用深度残差网络融合高光谱和全色图像;Hyperspectral pansharpening using deep prior and dual attention residual network(2020)使用双注意力残差网络融合多光谱和全色图像；

**Feature Map Attention Mechanism**

包括通道注意力机制和空间注意力机制；

(1) Single-frame remote sensing image SR reconstruction based on channel attention mechanism

Remote sensing image superresolution using deep residual channel attention(2019)中在非常深的网络结构中使用残差和跳跃连接传输不同级别的信息，有效缓解数据退化，内部特征提取采注意力机制；

(2) Spatial attention mechanism

CBAM: convolutional block attention module空间注意力机制；

Residual feature aggregation network for image super-resolution(2020)组合残差模块，添加跳跃连接，使用改进后的增强空间注意力模块，残差特征更加聚焦于关键的空间内容；Hyperspectral and multispectral image fusion based on deep attention network(2019)在高光谱和多光谱图像融合的网络中引入空间注意力机制，保留更多的空间信息，生成高空间分辨率和高光谱分辨率的遥感图像；

Hyperspectral and multispectral image fusion based on deep attention network

## Quality Evaluation Criteria for Remote Sensing Image Reconstruction

PSNR 峰值信噪比，计算重建图像的最大峰值与两幅图像的均方误差MSE的比值，反映重建图像的质量；

SSIM 结构相似性，计算融合图像和参考图像的均值、方差和协方差来衡量整体融合质量；值在0-1之间，越高表示具有越高的相似性；

ERGAS 相对全局维度合成误差，考虑光谱变化的整体情况，评估光谱范围内所有融合波段的光谱质量；该值越小，融合图像在光谱范围内的光谱质量越好；

SAM 光谱角度映射器，计算融合图像和参考图像的相应像素间的角度来评估光谱质量；理想的融合效果，SAM值应该是0；

SCC 空间相关系数，评估融合图像和参考图像空间细节的相似度，使用高通滤波器提取参考图像的高频信息，计算高频信息之间的相关系数；

Q 结合三个因素计算图像失真：相关性算是、亮度失真和对比度失真；Q值为1表示最佳保真度；

QNR 一种非参考图像质量评价方法，理想值为1，表示融合图像更佳；

PI perceptual index感知指标，PI值代表图像的主管感知质量。通常，PI值越低，图像看起来越舒服，图像的感知质量越好，这与PSNR值相反。一般来说，低PI值伴随着低PSNR值；

## DataSets

UCM、AID、PatternNet

UCM 0.3m/pixel AID 0.58m/pixel PAtternNet 0.0647m/pixel

![Untitled](2021%20Resea%20e4ff6/Untitled.png)

原图当作HR图像，在MATLAB中双三次下采样4倍bicubic interpolation算法得到LR图像；

实验比较方法：

Bicubic

SRCNN

SRResnet:Photo-realistic single image super-resolution using a generative adversarial network

EDSR

RDN

RCAN:Image super-resolution using very deep residual channel attention networks

DRN:Closed-loop matters: dual regression networks for single image super-resolution

Closed-loop matters: dual regression networks for single image super-resolution

## 未来方向

遥感数据的多元数据利用，不同数据源之间的信息互补，多图像超分；作者称为时空特征融合；

轻量级网络框架，提高SR重建的适用性；

无监督学习，监督学习通常需要标记数据来指导训练；
