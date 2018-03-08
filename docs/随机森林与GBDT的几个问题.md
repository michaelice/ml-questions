随机森林与GBDT的几个问题：

1.gbdt与随机深林的相同点：
（1）都是由多棵树组成
（2）最终的结果都是由多棵树一起决定

2.gbdt与随机森林的不同点：
（1）组成随机森林的树是分类数，也可以是回归树；而gbdt只由回归树组成
（2）组成随机森林的树可以并行生成；而gbdt只能是串行生成
（3）对于最终的输出结果而言，随机森林采用多数投票等；而gbdt则是将所有结果累加起来，或者加权累加起来
（4）随机森林对异常值不敏感，gbdt对异常值非常敏感
（5）随机森林对训练数据一视同仁，gbdt是基于权值的弱分类器的集成
（6）随机森林是通过减少方差提高性能，gbdt是通过减少模型偏差提高性能

3.随机森林的pro和con是什么？
优势是accuracy高，不易过拟合，但缺点是速度会降低。并且解释性会差很多，也会存在

4.为什么要最大化information gain？
从root到leaf，使得各class distribution的Entropy不断减低。如果相反的话，就会增加预测的不确定性。

5.熵entrophy的意义是什么？
首先信息量的大小和可能情况的对数函数取值有关系。变量的不确定情况越大，熵越大。

6.如何避免在随机森林中出现overfitting？
对树的深度的控制也即对模型复杂度的控制，可以在一定程度上避免overfitting，简言之就是shallow tree。此外就是prune，把模型训练比较复杂，看合并节点后的subtree能否降低generation error。随机选择训练集的subset，也可以实现避免overfitting。

7.Bagging的代价是什么？
Bagging的代价是不用单次决策树来做预测，具体哪个变量起到重要作用重要作用变得未知，所以bagging改进了预测准确率但损失了解释性。

8.Random forest和bagged tree的区别是什么？
随机森林的构建过程中，当考虑每个split时，都只从所有p个样本中选取随机的m个样本，作为split candidate。特别的m大概会取p的平方差。其核心目的是decorrelate不同的树。bagged tree和random forest的核心区别在于选择subset的大小。

9.什么是gbdt？
通过boosting的方法迭代性的构建week decision tree的ensemble。其优势是不需要feature normalization，feature selection可以在学习过程中自动的体现。并且可以指定不同的loss function。但是boosting是一个sequential process， 并非并行化。计算非常intensive，对高维稀疏数据的feature vector表现相当poor。

10.gbdt训练的步骤是什么？
使用information gain来获得最好的split，然后根据best split来partition数据。低于cut的数据分至left node，高于cut的数据分至right node。接下来进行boosting， 梯度函数可以有多种形式，gradient 是下一棵树的目标。

11.classification tree和regression tree的区别是什么？
回归树的output label是continuous，而分类树的output label是离散的。因此目标函数也要做相应的调整。特别的regression tree所给出的是probabilistic， non-linear regression， regression tree可以associate未知的独立的测试数据和dependent，continuous的预测。
