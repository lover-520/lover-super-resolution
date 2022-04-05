# 2019 FusionCNN: a remote sensing image fusion algorithm based on deep convolutional neural networks

[toc]

## Information

* 论文期刊：Multimedia Tools and Applications
* 论文链接：[link](https://link.springer.com/article/10.1007/s11042-018-6850-3)

## Comments

* 提出了一种基于卷积神经网络的图像融合算法;
* 其实从深度学习的角度来说这个网络并没有多大新意，主要在于采用了图像的纹理信息提高了全色图像的分辨率；从HLS视觉空间的角度，采用L成分作为PAN;

## Abstract

> In remote sensing image fusion field, traditional algorithms based on the human-made fusion rules are severely sensitive to the source images. In this paper, we proposed an image fusion algorithm using convolutional neural networks (FusionCNN). The fusion model implicitly represents a fusion rule whose inputs are a pair of source images and the output is a fused image with end-to-end property. As no datasets can be used to train FusionCNN in remote sensing field, we constructed a new dataset from a natural image set to approximate MS and Pan images. In order to obtain higher fusion quality, low frequency information of MS is used to enhance the Pan image in the pre-processing step. The method proposed in this paper overcomes the shortcomings of the traditional fusion methods in which the fusion rules are artificially formulated, because it learns an adaptive strong robust fusion function through a large amount of training data. In this paper, Landsat and Quickbird satellite data are used to verify the effectiveness of the proposed method. Experimental results show that the proposed fusion algorithm is superior to the comparative algorithms in terms of both subjective and objective evaluation.
>  

遥感影像融合领域，融合的规则大都依赖于人工制定，提出了一种基于卷积神经网络的图像融合算法，并构建了一个新的自然影像数据集去类比多光谱MS和全色PAN图像；

## Remote sensing image fusion algorithm

融合结构：

文章中该网络结构的输入都是color images，全色图像怎么是color的？

![Untitled](2019%20Fusio%20f1d5a/Untitled.png)

整个算法的框架：

采用CIFAR数据进行训练；

图片I当成groundtruth，对应的影像当成MS image，HLS视觉空间中的L成分当成EPAN(先双线性下采样，然后双三次上采样和MS image一样)；

问题就是这样得到之后的怎么在文中的显示效果两者如果图片大小一样大的话，怎么可能清晰度差别很大，就下图中第三列怎么可能和第二列的大小是一样大的？；

![Untitled](2019%20Fusio%20f1d5a/Untitled%201.png)

![Untitled](2019%20Fusio%20f1d5a/Untitled%202.png)

在CIFAR上进行训练之后，然后在LandSat和Quickbird上进行了测试，GLCF public dataset which contains remote sensing images from Landsat and Quickbird satellites

在定性的比较中，有作为Reference的影像怎么不直接在遥感影像上进行训练而采用CIFAR？

![Untitled](2019%20Fusio%20f1d5a/Untitled%203.png)