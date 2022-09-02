# Intro

在极少量标签数据的情况下，尤其是没有办法拿到不同类别下标签的时候（imbalance ?)，few-shot learning和半监督的效果都不好（都需要在不同类别中的统一采样）此时需要经过SSL预训练的active learning

# relate work

Few-shot learning（这里指的应该是MAML)需要在不同类别下统一数量的标签

uncertainty-base的方法不适合大量数据和复杂模型

基于分布的例如coreset在数据维度较高时表现差

VAAL,DFAL这些对抗性方法容易重复选择

半监督学习需要统一分布标注所以难以直接比较，但仍然比较


