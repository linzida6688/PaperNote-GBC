# 读文章笔记-GBC
# 背景
- Computer Science > Machine Learning上的一篇文章，发表于2022年1月。重庆邮电大学计算机学院院长王国胤等教授，带领学生发表的论文。
- 数据集来自：University of California, Irvine (UCI) benchmark
- 实验硬件: PC with an Intel Core i7-107000 CPU@2.90 GHz with 32 GB RAM. Experimental 716；软件: Python 3.9.
# 内容
- 基于原有的GB算法提出一种高效和自适应的加速GB生成算法，在速率上优于k均值算法(K-Means)。并且可以结合SVM和KNN，在精确度上GBKNN是普通KNN的百倍；更是提出了GBNRS，有更高的分类精度，它是第一个在无先验知识的情况下处理连续数据的无参数粗糙集算法。
## 定义1+现有GB生成过程
在定义1中：如果达到GB纯度阀值时，则算法停止分类。现有颗粒球生成的主要过程：
- 1将一整个数据集看成球；
- 2然后随机k个子球；
- 3每个球都达到纯度阀值。是则停止分割并且覆盖；否则继续分割直到到达纯度阀值。

## GBKNN
从多粒度的角度来看，k优化问题的根源是过度细粒度的关注，GBkNN是不用优化k vlaue，既不用优化参数k。GBkNN和传统kNN的共同特点是查询点的标记由多个点决定。**GBS生成的边界比随机抽样生成的边界更接近原始数据集的边界.** 它的三个优点：
- 不需要优化参数k，查询点标签由自适应生成的具有不同粗粒度的最近邻GB确定；
- GB的数量远小于样本点，并且查询点查询到的最近GB的计算量远小于kNN，时间复杂度为O(n)；
- 不会像KNN那样被标签噪声干扰；

## GB生成算法
- 这里的的意思就是在保证最小的GBs数量的同时保证最大的覆盖度，以达到最优；调整λ1 and λ2是关键。因此，以上因素都不是缺一不可的。因素1.覆盖度；因素2.GBs的数量；因素3.GBs的大小。
- GB是否分裂取决于，子球的纯度是否高于它自己。
- 如果W>T，就是子球中包含的样本数量大于父球中的样本数量；W=T，则相等。
- 子球的分裂条件：1.当子球的加权纯度总和大于其母球的纯度；2.GB纯度达到下限时；3.或者有重叠。

# 疑问
- Bk-means效率是同类算法的几十倍，特别是在具有挑战性的大k聚类问题中？这里说的应该是K值不能太大，会发生过拟合？
- 这里的GB生成是否为了用于三维的数据，或者是将数据升维(类似核函数)，在三维数据中进行分类？
- GBs子颗粒球，纯度高可能意味着不稳定；GBs的数量多，但是不一定可以形成高质量的GBs，如图fig.4.e，但是分割结果很稳定；
- 关于公式(4),(5);这里所说的积极和消极是否指的是，当点a半径小于GB的r那么就是积极，反之则是消极？
- GB生成方法仍有某些随机性

# 文献脉络
- GBkNN [17] and GBS [38] ：state-of-the-art methods based on granular computing。