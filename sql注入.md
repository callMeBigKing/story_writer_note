---
title: 决策树
tags: ID3,C4.5，Cart
grammar_cjkRuby: true
---
   决策树（decision tree）是一个树结构（可以是二叉树或非二叉树）。其每个非叶节点表示一个特征属性上的测试，每个分支代表这个特征属性在某个值域上的输出，而每个叶节点存放一个类别。使用决策树进行决策的过程就是从根节点开始，测试待分类项中相应的特征属性，并按照其值选择输出分支，直到到达叶子节点，将叶子节点存放的类别作为决策结果。如下图所示
  ![enter description here][1]
构造决策树的关键点就在于每层属性的选择，也就是最优划分属性，一般是希望决策树的分支节点所包含的样本尽可能的属于同一类别，即节点的**纯度**越高越好
## 算法
### ID3
ID3 采用信息熵来衡量纯度
记D为样本集合，D的熵（entropy）为![enter description here][2]
  现在我们假设将训练元组D按属性A进行划分，则A对D划分的期望信息为：
  ![enter description here][3]
  信息增益为
  ![enter description here][4]
  
 A\*=max arg gain(A)
 ### C4.5
 ID3算法存在一个问题，就是偏向于多值属性，例如，如果存在唯一标识属性ID，则ID3会选择它作为分裂属性，这样虽然使得划分充分纯净，但这种划分对分类几乎毫无用处。ID3的后继算法C4.5使用增益率（gain ratio）的信息增益扩充，试图克服这个偏倚。
 ![enter description here][5]
得到新的目标函数
![enter description here][6]
### CART
cart 采用基尼指数来选择划分属性数据集D的纯度可以用基尼值来衡量：
![enter description here][7]
![enter description here][8]
基尼值反应了从数据集中随机冲去两个样本，其类别标记不一致的概率，因此Gini(D)越小，数据集D的纯度越高，属性I的基尼指数定义为
![enter description here][9]

## 剪枝
 剪枝是决策树对付过拟合的主要手段，按照训练前后有预剪枝和后剪枝
 ### 预剪枝
 预剪枝是在决策树生成过程中，对每个接娃娃店在划分前先进行估计，若当前节点的划分不能带来决策树泛华性能的提升，则停止划分并将当前节点标记为叶节点
 ### 后剪枝
 后剪枝是先从训练集生成一颗完整的决策树，然后自底向上的对非叶节点进行考察，若该节点对应的子树替换成叶节点能够带来决策树泛华新年提升，则将该节点替换为叶节点。
### 判断性能方法
测试集，准确率来判断
预剪枝基于贪心思想禁止分支展开，有欠拟合的风险
后剪枝性能好，但是要自底向上逐一考察，因此训练时间与开销大。

## 连续与缺失值


 - List item

  [1]: http://images.cnblogs.com/cnblogs_com/leoo2sk/WindowsLiveWriter/34d255f282ae_B984/1_3.png
  [2]: ./images/1496815354032.jpg
  [3]: ./images/1496815490954.jpg
  [4]: ./images/1496815516775.jpg
  [5]: ./images/1496815659310.jpg
  [6]: ./images/1496815674707.jpg
  [7]: ./images/%E5%A4%A7%E5%A4%A7%E5%A4%A7.gif "大大大"
  [8]: ./images/1496816699198.jpg
  [9]: ./images/1496816725789.jpg