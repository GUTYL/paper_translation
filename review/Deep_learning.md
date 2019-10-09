## 深度学习

### 原文：[Deep learning](https://creativecoding.soe.ucsc.edu/courses/cs523/slides/week3/DeepLearning_LeCun.pdf)
### 作者：Yann LeCun, Yoshua Bengio, Geoffrey Hinton

### 目录：

[TOC]

#### 1 摘要

深度学习（deep learning）允许由多个处理层组成的计算模型学习具有多个抽象级别的数据表示（representation）。这些方法显著的提高了语音识别（speech recognition）、视觉对象识别（visual object recognition）、对象检测（object detection）和许多其他的领域（如药物发现和基因组学）的最佳表现。深度学习通过使用反向传播算法（backpropagation algorithm）去指示机器如何改变内部参数（internal parameters）来发现大数据集的复杂结构，这些内部参数被用于从上一层的表示中计算每一层的表示。深度卷积网络（deep convolutional nets）带来了图像（images）、视频（video）、语音（speech）和音频（audio）处理的重大突破，而递归网络（recurrent nets）则在文本（text）和语音（speech）等序列数据（sequential data）方面取得了突破。

#### 2 概述

机器学习技术驱动了现代社会的许多方面：从网络搜索到社交网络（social netwroks）的内容过滤，再到电子商务网站（e-commerce websites)的推荐。它越来越多的出现在相机和智能手机这样的消费产品中。机器学习系统被用于识别图像中的物体，将语音转换维文本，将新闻条目、帖子或产品与用户的兴趣进行匹配，并选择搜索的相关结果。这些应用越来越多的使用一种名为深度学习的技术。

传统的机器学习技术（conventional machine-learning techniques）处理原始数据的能力有限。数十年以来，构造一个模式识别（ pattern-recognition）或者机器学习系统需要详细的工程设计和相当多的领域专业知识来设计一个特征提取器（feature extractor），将原始数据（如图像的像素值）转换成合适的内部表示（internal representation）或特征向量（feature vector），使得学习子系统（通常是一个分类器）可以从中检测（detect）或分类（classify）输入中的模式（input）。

表示学习（representation learning）是一套学习方法，它允许机器从原始数据中自动发现检测或分类所需要的表示。深度学习方法是多层表示的表示学习方法，通过组合简单但非线性的模型获得，每个模型从一个层次（从原始输入开始）转换为更高、更抽象层次的表示。

深度学习方法是一种具有多层表示的表示学习方法，通过组合简单但非线性的模块获得，每个模块将一个级别的表示(从原始输入开始)转换为一个更高、更抽象的表示。通过足够的变换组合，可以学得非常复杂的函数。对于分类任务来说，高层次的表示放大了输入的某些方面，这些方面在区别和抑制不相关变量非常重要。例如，一张图片由一个像素数组组成。

更高层次的表现放大了输入的某些方面，而这些方面对于辨别和抑制无关的变化非常重要。而第一层表示中的习得特征（features）通常表示图像中特定方向和位置边缘的存在或不存在。第三层将图案组合为更大的组合，这些组合对应于熟悉对象（familiar objects）的部分，随后的层将检测这些部分组合的对象。深度学习的关键在于，这些层的特征不是由人类工程师设计的：它们使用数据从多用途的学习程序中习得。

深度学习在解决多年来一直限制人工智能界最佳尝试的问题方面取得了重大进展。它非常擅长发现高维数据的复杂结构，因此它被用于像科学、商业和政府的许多领域。另外，它在图像识别 **[1-4]** 和语音识别 **[5-7]** 上也有很好的表现，它在预测药物分子的潜在活性 **[8]**、分析粒子加速器（particle accelerator)数据 **[9，10]**、重建大脑回路 **[11]**和预测非编码DNA突变对基因表达和疾病的影响 **[12，13]** 的这些方面上打败了其他的机器学习算法。令人更惊讶的是，深度学习算法非常有希望解决各种各样的自然语言理解的问题 **[14]**，尤其是主体分类（topic classificaiton）、情感分析（sentiment analysis）、问题回答 **[15]**和语言翻译 **[16，17]**。

我们认为深度学习在不久的将来将会取得更多的成功。因为它只需要非常少的手工操作，所以它可以很容易的利用增加的计算能力和数据。当前正在发展的的、新的、深度神经网络（deep neural networks）的学习算法和架构将会加快这个进程。

#### 3 监督学习 Supervised learning

无论是不是深度学习，监督学习都是机器学习的最常见形式。想象一下，我们想要构建一个可以根据图像内容来分类图像的系统，然后告诉我们，这是一栋房子、一辆车、一个人或者宠物。我们首先收集一个很大的数据集，其中包括房子、车、人和宠物的图像，并对每个图像进行分类。经过训练，向机器展示一张图片，它对每个类别输出所产生向量得分。我们期望在目标分类在每个分类的得分中有最高的分数，但这个在训练以前不太可能发生。我们使用一个客观的函数来衡量输出得分和期望的分数模式之间的误差（或距离）。接着机器修改其内部的、可调的参数来减少这个误差。这些可调参数通常被成为权重（weight），它们是一个真实数据（real numbers），且可以被认为是机器输入-输出函数的“旋钮”。在典型的深度学习系统中，可能会有数亿的、这样的可调参数以及训练这个机器的数亿被标记后的样例。
