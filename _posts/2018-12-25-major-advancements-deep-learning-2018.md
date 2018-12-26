---
title: "[翻译]2018年深度学习主要进展"
category: translation
layout: post
tags: [翻译,dl]
date: '2018-12-20 21:00:24'
---
原文：[链接](https://tryolabs.com/blog/2018/12/19/major-advancements-deep-learning-2018/)

---

在过去的多年里，深度学习已经发生了天翻地覆的变化.每天都有各种基于深度学习技术的产品出现：保健、金融、人力资源、零售、地震预测以及自动驾驶。而已经应用的产品性能也在提高。

在学术界，有关深度学习的论文每20分钟就有一篇生成。

本文将介绍深度学习在2018年的主要进展。像去年的[那篇](http://blog.rubenxiao.com/posts/dl-in-nlp-for-2017.html)一样(译者注：去年刚好也翻译了这篇)，本文没法详细的介绍每个成果。所以这里只介绍一些印象深刻的成果。

### 语言模型：Google的BERT模型

在自然语言处理领域，语言模型用来估计语言单元（linguistic units）的概率分布，典型的如一句话中的词。这些模型可以提升很多NLP任务的效果，比如机器翻译、语音识别、依存分析。
历史上最著名的语言模型是基于马尔可夫模型和n-gram语言模型。随着深度学习的发展，LSTM网络为语言模型带来了极大的提升。尽管效果已经不错，但是现有的模型是非双向的，这就意味着只考虑到了单词的左（或者右）方向上的上下文。
过去的十月份，Google AI语言组发布的一篇[论文](https://arxiv.org/abs/1810.04805)在NLP社区引起了轰动。他们提出的BERT模型是一种新的双向语言模型哦那个，在多个NLP任务中取得了最好的结果，包括情感分析、QA、语义检测。

<img src="https://tryolabs.com/images/blog/post-images/2018-12-19-major-advancements-deep-learning-2018/glue-test-results.42b7601b.png" height="320">

<center>GLUE测试集上的结果.</center>

与传统的从左到右或者从右到左的语言模型策略不同，BERT的预训练策略如下：

- 将部分输入的token设置为掩码，然后预测这些掩码处的token；这就表示在多层上下文中可以简介的"看见这些token".

- 建立一个二元分类模型预测句子B是否跟在句子A后面，这表示模型学习到了句子间的关系，这是传统语言模型直接学习不到的现象。

Google开源了BERT的[Tensorflow代码](https://github.com/google-research/bert)，Pytorch版本的代码也有不同的实现：[Thomas Wolf](https://github.com/huggingface/pytorch-pretrained-BERT)和[Junseong Kim](https://github.com/codertimo/BERT-pytorch).

BERT对于商业应用提供了极大的提升，不管是机器翻译，还是chatbot，还包括邮件自动回复，用户评价分析。


### Video-to-video Synthesis

我们都习惯由图形引擎创建的虚拟器或视频游戏的交互环境。虽然有声有色，但是传统的方法成本较高，因为场景的集合、材料、光照以及其他的参数必须要详细的设定。一个很好的思路就是：如何利用比如深度学习这样的技术自动化的构建这些环境。

在论文[video-to-video synthesis](https://arxiv.org/abs/1808.06601)中，英伟达的研究人员尝试解决这个问题。简单的说他们的目标就是构建将输入视频映射到真实的准确描述输入内容的输出视频的函数。作者将这个问题建模为自动创建的视频的条件分布与最终的视频的条件分布的分布匹配问题。为了达到这个目标，他们使用GAN创建该模型。这个方法的关键是，生成的合成数据不能被判别器分辨出为假的。他们定义了一个时空学习目标方程，旨在生成时空一致性的视频

生成的结果特别的令人惊喜，如下图所示：

<img src="https://tcwang0509.github.io/vid2vid/paper_gifs/cityscapes_comparison.gif" height="320">

<center>Video-to-video synthesis.</center>

左上是[Cityscapes](https://www.cityscapes-dataset.com/)数据集中的街景语义分割视频。作者还与两个baseline进行了对比: pix2pixHD (右上) 和COVST (左下).

该方法可以应用到多个任务重，比如用于视频人脸交换的草图到视频生成。下面的视频，从左到右，先是由原视视频生成草图，然后由草图生成合成视频。

<video width="480" height="320" controls="controls">
<source src="https://tcwang0509.github.io/vid2vid/paper_gifs/face.mp4" type="video/mp4">
</video>
<center>视频合成之换脸.</center>

本方法甚至可以应用于预测未来视频；先给定一些现有视频，然后预测之后的视频，也得到令人惊喜的结果。
此外，英伟达开源了[vid2vid代码](https://github.com/NVIDIA/vid2vid)。

### Improving word embeddings

去年已经介绍了词嵌入对于NLP的重要性，在不久的将来将会得到更多的关注。大家对于King - Man + Woman = Queen这种转换关系已经变得不像当初那么兴奋了，而这在实践中也有很多的限制。最重要的是无法解决一次多亿以及不能准确的建立词之间的关系。同义词？下义词？另一个限制就是形态学上的关系：词嵌入不能分辨driver和driving在形态学上的关系。

正如标题显示的一样, [Deep contextualized word representations](https://arxiv.org/abs/1802.05365) (NAACL 2018的优秀论文), Allen Institute for Artificial Intelligence以及 the Paul G. Allen School of Computer Science & Engineering提出了一种新的深度上下文词表征方式，模拟了词使用的复杂特征（比如语法和语义），以及在语言间的上下文的使用变化（比如多义）。

核心的思路从语言模型中获取词嵌入，即Embeddings from Language Models (ELMo)，就是指用整句或者整个上下文对词进行向量化。为了实现这个目标，作者首先使用大量的语料训练了一个双向语言模型。此外，因为这个语言模型是基于字母的，因而单词之间的形态学关系也能得到。所以，这个模型能够很好的处理从未出现过的情形，比如字典外的词。

<img src="https://tryolabs.com/images/blog/post-images/2018-12-19-major-advancements-deep-learning-2018/word-embeddings-results-nlp-task.b1783137.png" height="320">

<center>6个测试集上的结果对比.</center>

作者通过简单的添加ELMo到当前的一些先进的方法中就能在很多NLP任务重获得更好的结果，比如文本蕴含，指代消解，QA。ELMo对Google的BERT有很大的贡献，相信能对一些商业应用能有更好的促进。

### 可视化任务之间的结构化关系

视觉任务之间有关联吗？这个问题由斯坦福和伯克利大学的研究人员在[Taskonomy: Disentangling Task Transfer Learning](https://arxiv.org/abs/1804.08328)中做了回答。该文获得 [CVPR 2018最佳论文](http://cvpr2018.thecvf.com/program/main_conference#awards)。

毫无疑问，很多视觉任务之间存在关联。比如说知道物体的表面特征能够帮助对图片进行深度估计。在这种场景下，迁移技术或者使用监督学习的结果是很有用的。

作者提出了一种计算方法建立26种常见视觉任务之间通过迁移学习建立依赖结构，包括物体识别、边缘检测、深度估计。

![](https://tryolabs.com/images/blog/post-images/2018-12-19-major-advancements-deep-learning-2018/visual-task-sample-task-structure.9b8b571a.png)

<center>A sample task structure discovered by the computational task taxonomy.</center>

正如上图展示的一样，如果联合表面检测和边缘检测，则阴影和点的匹配模型只需要少量的标注数据就能得到。

这项工作的一个主要的贡献就是证明了少量的标注数据通过迁移学习可以减少2/3左右的标注工作量。这对于商业应用来说非常重要。



### 文本分类中微调的全局语言模型

深度学习模型对于NLP领域的促进非常巨大，很多NLP任务的先进结果都是利用的深度学习模型。然而，这些模型都需要构建大量的数据并耗费大量的时间进行训练。

[Howard and Ruder](https://arxiv.org/abs/1801.06146)的工作提供了一种利用Universal Language Model Fine-tuning (ULMFiT)的迁移学习的方法。主要的思路就是微调已经训练好的语言模型。这种巧妙的方法能够使得我们可以使用少量的标注数据就可以对其他任务进行探索。

![](https://tryolabs.com/images/blog/post-images/2018-12-19-major-advancements-deep-learning-2018/ulmfit-test-error-rates.447ebaf9.png)
<center>模型的错误率.</center>

他们的方法在6个文本分类任务上取得最好的结果，减少错误率18-24%.对于训练数据的数量，结果也是惊人的：他们的方法使用100个标注数据和50k非标注数据，而从0开始训练的模型是10k标注数据。但是他们的方法却取得一样的结果。

他们的结果表明迁移学习在NLP领域非常值得去研究的。想要了解细节可以参考[代码](http://nlp.fast.ai/category/classification.html)。


### 总结

今年深度学习的技术继续得到广泛的应用。尤其迁移学习得到了越来越多的关注，从战略的角度来看这是今年最好成果。希望这个趋势能够得到持续。

另外还有一些没有在文章中列出来的进展依然值得关注，比如[OpenAI Five](https://blog.openai.com/openai-five)在DOTA2中击败了职业玩家。另外[spherical CNN](https://arxiv.org/abs/1801.10130)和[ PatternNet and PatternAttribution](https://arxiv.org/abs/1705.05598)在CNN的可解释性上的工作也值得关注。

从商业的角度来说，上述突破在商业应用上的促进作用是可以预见的，比如机器翻译、健康诊断、聊天机器人、仓储管理、自动邮件回复、人脸识别、用户评价分析等。

从学术的角度来说，[Deep Learning:
A Critical Appraisal ](https://arxiv.org/abs/1801.00631)对深度学习的综述值得品读。该文清晰的指出了当前深度学习的不足指出，并且提出深度学习需要借助认知和发展心理学、符号科学和混合建模等学科的发展。


### 参考文献

[Spherical CNNs](https://arxiv.org/abs/1801.10130). Taco S. Cohen, Mario Geiger, Jonas Koehler, and Max Welling.

[BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/abs/1810.04805). Jacob Devlin, Ming-Wei Chang, Kenton Lee, and Kristina Toutanova.

[Universal Language Model Fine-tuning for Text Classification](https://arxiv.org/abs/1801.06146). Jeremy Howard and Sebastian Ruder.

[Learning how to explain neural networks: PatternNet and PatternAttribution](https://arxiv.org/abs/1705.05598). Pieter-Jan Kindermans, Kristof T. Schütt, Maximilian Alber, Klaus-Robert Müller, Dumitru Erhan, Been Kim, and Sven Dähne.

[Deep Learning: A Critical Appraisal](https://arxiv.org/abs/1801.00631). Gary Marcus.

[Deep contextualized word representations](https://arxiv.org/abs/1802.05365). Matthew E. Peters, Mark Neumann, Mohit Iyyer, Matt Gardner, Christopher Clark, Kenton Lee, and Luke Zettlemoyer.

[GLUE: A Multi-Task Benchmark and Analysis Platform for Natural Language Understanding](https://arxiv.org/abs/1804.07461). Alex Wang, Amanpreet Singh, Julian Michael, Felix Hill, Omer Levy, and Samuel R. Bowman.

[Video-to-Video Synthesis](https://arxiv.org/abs/1808.06601). Ting-Chun Wang, Ming-Yu Liu, Jun-Yan Zhu, Guilin Liu, Andrew Tao, Jan Kautz, and Bryan Catanzaro.

[Taskonomy: Disentangling Task Transfer Learning](https://arxiv.org/abs/1804.08328). Amir Zamir, Alexander Sax, William Shen, Leonidas Guibas, Jitendra Malik, and Silvio Savarese.
