# 2019 Achieving Super-Resolution Remote Sensing Images via the Wavelet Transform Combined With the Recursive Res-Net

[toc]

## Information

* 论文期刊：IEEE Transactions on Geoscience and Remote Sensing
* 论文链接：[link](https://ieeexplore.ieee.org/abstract/document/8600724)

## Comments

* 文章的主要创新点在于使用小波变换提取分量，对分量进行超分，然后逆小波变换合成;
* 个人觉得这篇文章充分展示了基本的图像处理知识与深度学习知识相结合的潜力，从深度学习中网络的角度来看，这篇文章中所提出的网络是不足以达到较好的结果的，网络的创新性并不是很强，但重点就在于前面结合了图像处理中的小波变换，提升了超分辨率效果；

## Abstract

> Deep learning (DL) has been successfully applied to single image super-resolution (SISR), which aims at reconstructing a high-resolution (HR) image from its low-resolution (LR) counterpart. Different from most current DL-based methods, which perform reconstruction in the spatial domain, we use a scheme based in the frequency domain to reconstruct the HR image at various frequency bands. Further, we propose a method that incorporates the wavelet transform (WT) and the recursive Res-Net. The WT is applied to the LR image to divide it into various frequency components. Then, an elaborately designed network with recursive residual blocks is used to predict high-frequency components. Finally, the reconstructed image is obtained via the inverse WT. This paper has three main contributions: 1) an SISR scheme based on the frequency domain is proposed under a DL framework to fully exploit the potential to depict images at different frequency bands; 2) recursive block and residual learning in global and local manners are adopted to ease the training of the deep network, and the batch normalization layer is removed to increase the flexibility of the network, save memory, and promote speed; and 3) the low-frequency wavelet component is replaced by an LR image with more details to further improve performance. To validate the effectiveness of the proposed method, extensive experiments are performed using the NWPU-RESISC45 data set, and the results demonstrate that the proposed method outperforms several state-of-the-art methods in terms of both objective evaluation and subjective perspective.
> 

不同于传统的基于深度学习的，从空间域进行重建，本文中采用基于频域的方法重建不同频带的HR图像。此外，结合了小波变换WT和递归ResNet网络。使用WT将LR图像划分成各种频率分量；使用设计好的递归ResNet网络预测高频分量；最后使用逆WT重建图像。三个贡献点：1)基于频域的SISR方法，充分探索不同频段对图像的描绘能力；2)全局和局部的递归残差网络缓解网络训练，增强网络的灵活性；3)低频小波分量被替换为细节更多的LR图像；

## Introduction

> Most current DL-based SISR methods perform reconstruction in the spatial domain and are devoted to learning the relationship between LR pixels and their counterparts in HR images to improve resolution. Although restoring the lost high-frequency information in the frequency domain seems to be more straightforward, this technique has been ignored in DL-based SISR approaches.
> 

前面是一些超分的应用和超分领域别人的工作，这里指出目前大多数基于深度学习的超分辨率重建方法主要是在空间域中执行重建，学习LR图像中每个像素与在HR图像中对应像素的关系；在频域中恢复图像的高频信息似乎更直接，但是目前的基于Dl的SISR方法并未采用这种思路；

> Although the WT has been proven to be an effective tool for traditional super-resolution methods, to the best of our knowledge, few studies have focused on incorporating the WT into deep CNNs, which is expected to further improve the reconstruction accuracy due to their respective advantages.
> 

小波变换WT被证实是传统超分辨率方法的有效工具，但就目前而言，很少有工作在深度学习中应用WT，由于CNN和WT具有各自的特性，因此有望进一步提高图像重建的精度。

> In this paper, we present a three-step super-resolution method for remote sensing images via the WT combined with the recursive Res-Net (WTCRR). First, the LR image is decomposed into four subbands of LR wavelet components using single-level 2-D discrete WT (DWT), and the low-frequency subband is replaced by the LR image. The combination of the four subbands is fed into the following designed network. Then, a novel deep network that uses recursive residual learning is applied to predict the residuals of the four corresponding subbands of the HR wavelet components. Finally, the reconstructed HR image is obtained using the inverse 2D-DWT.
> 

本文提出了一种针对遥感图像结合WT变换和递归ResNet的三步超分辨率方法；使用DWT将LR图像分解为LR小波分量的四个子带，低频子带替换为LR图像；四个子带的组合送入神经网络中；一种使用递归残差学习的网络预测HR小波分量的四个对应子带的残差；最后使用逆2D—DWT获取重建后的HR图像；

## Background

### Wavelet Transform

对2维的图像而言，m*n大小，从一维的角度进行处理：先从列的角度进行1D-DWT得到m*(n/2)大小的图，然后再从行的角度再次减小2倍；L(x)和H(x)分别表示低通滤波器和高通滤波器；

四个子带分别表示图像I的平均(LL)、水平(LR)、垂直(HL)和对角线(HH)分量；平均(LL)分量表示图像的低频成分，水平(LR)、垂直(HL)和对角线(HH)分量表示图像的高频成分，也提供了部分结构信息；

![Untitled](2019%20Achie%20bf5ba/Untitled.png)

### DWT+Non-DL SR

传统的基于DWT的超分方法，不采用深度学习；

首先采用2D DWT提取四个子带，采用non-DL SR提升四个子带分量的分辨率，然后采用逆小波变换2D IDWT重建HR图像；

![Untitled](2019%20Achie%20bf5ba/Untitled%201.png)

## METHODOLOGY

> A high-quality HR image with abundant textural details and global topology information can be restored from an LR image if the corresponding wavelet components are accurately predicted. Hence, the process of reconstructing an HR image can be transformed into the process of predicting its wavelet components. However, the CNN model has achieved great success in SR due to its powerful feature extraction and representation ability. The above two facts motivate us to introduce the WT to the CNN-based SR scheme and propose the WT combined with recursive Res-Net (WTCRR). The entire architecture of WTCRR is illustrated in Fig. 3, and can be separated into the disassembled part, the predicted part and the reconstructed part.
>  

对应的小波分量能够准确预测的话，那么就可以从LR图像中恢复出具有丰富纹理细节和全局拓扑信息的高质量HR图像。因此，重建HR图像的过程可以转化为预测其小波分量的过程。CNN由于具有强大的特征提取和表示能力，因此将WT引入基于CNN的SR中，并结合递归残差网络。整个网络WTCRR包括三个部分，拆解部分disassembled part、预测部分predicted part、重构部分reconstructed part

![Untitled](2019%20Achie%20bf5ba/Untitled%202.png)

Flowchart of the proposed WTCRR method, which consists of the disassembled part, the predicted part and the reconstructed part. The disassembled part decomposes the interpolated version of the LR image into four LR wavelet components. The predicted part makes use of the designed CNN-based SR network to estimate the HR wavelet components from their LR counterparts. The reconstructed part applies the 2D-IDWT to generate the super-resolved image from the HR wavelet components.
提出的WTCRR流程图说明，disassembled part将LR图像的插值版本(采用Bicubic先上采样插值)Haar小波变换分解成四个LR小波分量，预测部分采用设计的网络从LR对应部分估计HR小波分量，重建部分应用2D IDWT从HR小波分量生成超分辨率图像；

disassembled part包含三个作用：1)Bicubic插值上采样；2)DWT提取4个分量；3)第一个平均分量没有用到，取而代之的是初始的低分辨率影像，与另外三个分量一同输入到后面的网络中；reconstructed part中使用逆小波变换对前面的四个输出合成HR图像；

预测网络部分实际上比较简单，没有较多花里胡哨的东西；

(a)是VDSR的结构，采用了一种全局残差的结构；(b)是DRCN的结构，添加了递归模块，递归模型就是很多网络层采用一样的参数，大大减小了参数量；(c)是本文提出的WTCRR的结构，采用了递归模块，然后全局和局部上都采用了残差模块；别的图像是针对RGB图像，3通道的输入；WTCRR4通道的输入；

![Untitled](2019%20Achie%20bf5ba/Untitled%203.png)

### Experiments

数据集采用NWPU-RESISC45，文中所展示的例子都是里面的飞机一类，比较的方法也是最近的计算机视觉领域的网络；

小波变换的例子可参考：

[Python 离散小波变换（DWT） pywt库_wsp_1138886114的博客-CSDN博客_pywt.dwt2](https://blog.csdn.net/wsp_1138886114/article/details/116780542)