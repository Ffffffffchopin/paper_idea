#  Class-Balanced Loss Based on Effective Number of Samples  一篇基于有效样本数量加权解决长尾分布的论文解析

### 因为最近在做imbalance场景下active learning的领域，所以泛读（瞎读）了几篇

## 背景

	众所周知，数据的imbalance，即long-tailed长尾分布在现实世界的大规模数据中十分常见。小概率事件的发生总是更能吸引人们的注意力，这也符合信息论的看法，因此解决长尾分布问题是应用深度学习算法的重要基础（也因此给了我等低级炼丹师水论文的机会）。传统的解决imbalance的方法主要分为re-sample重采样和re-weight重加权两大类。


