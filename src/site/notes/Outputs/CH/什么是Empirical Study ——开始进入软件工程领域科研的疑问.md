---
{"dg-publish":true,"permalink":"/Outputs/CH/什么是Empirical Study ——开始进入软件工程领域科研的疑问/"}
---

### 软工领域中的Empirical Study
#### 背景介绍

从偏AI的计算机转到软件工程方向。在读论文的时候，发现软件工程领域有些论文在以前从未见过，写作范式也完全不一样，那便是：Empirical Study。

在知乎上查，似乎也很少对Empirical Study的介绍。某篇回答也提到"好像CS中也只有软工领域有Empirical Study这种神奇的文章。"

所以趁着我正好在写一篇Empirical Study，浅薄的分享一下软工领域中的Empirical Study。不足之处多多包涵~
#### Empirical Study是什么？

用维基百科的话来说：
>实证研究是使用实证证据进行的研究。它也是通过直接和间接的观察或经验来获取知识的一种方式。经验主义比其他研究更重视一些研究。经验证据（一个人的直接观察或经验的记录）可以定量或定性地分析。 量化证据或以定性形式理解证据，研究人员可以回答经验问题，这些问题应该明确定义并可以用收集到的证据（通常称为数据）来回答。研究设计因领域和所调查的问题而异。许多研究人员将定性和定量的分析形式结合起来，以更好地回答在实验室环境中无法研究的问题，特别是在社会科学和教育领域。

直观点看：
Empirical Study就是发现了某个有意思的话题/观点/问题，于是可以通过数据搜集与统计的方法，回答所提出的问题，得到某些有意思的发现。

我的感受：
软工中的Empirical Study特别像文科中的理科，理科中的文科。

事实上：
如果想做一个比较创新的方向，比较好的流程也是：先写一篇Empirical Study，中个比较好的会议或者期刊。再根据Empirical Study提出的方向，进行后续这个较新方向的研究。
#### 软件工程领域常见的Empirical Study组成部分（简洁版）
##### 1. Research Question
整篇文章都是围绕着你提出的RQ来进行写作的。从Introduction引入RQ，到Methodology中如何回答RQ，再到Results中围绕着RQ得到了什么findings。

RQ是整篇文章的核心，也是最重要的创新点。
##### 2. Collecting Data
软工领域，提出的观点基本围绕着软件开发进行，自然而然，数据来源也应该是和软件开发相关的论坛。

研究的数据来源基本离不开这三个网站：StackOverflow、StackExchange以及Reddit。
并且科研人员往往会下载[Stack Exchange Data Dump](https://archive.org/details/stackexchange)上的完整转储，来进行分析。
##### 3. Topic Modeling
得到了想要的数据，大部分论文会选择使用LDA进行主题建模，看看这些讨论都集中在什么话题。也可以分析主题的相关性、主题热度随时间变化等。从而得到RQ的findings。

如果想要回答的RQ更复制，LDA主题建模无法得出结论。可以采用人工去看数据，打标签的方法来分析数据。

#### 软件工程领域常见的Empirical Study组成部分（复杂版）

有空再写。



