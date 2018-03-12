#【SON算法】
寻找高频组合的方法。目的是为了减少对全局数据计算A-priori算法时的空间消耗。
第一轮：重复读取购物篮数据小的子集，分别使用单机的A-priori算法，得到高频物品组合。
第二轮：对全局数据过一遍，对所有候选组合重新计数。

# A-priori算法
第一轮：读取篮子，然后数每个物品的频率，如果大于阈值，则记录为高频物品。
第二轮：重新读取篮子，然后只数组合内物品都为高频的组合。

# 协同过滤
建立基于用户购买评分历史的模型，然后寻找做出相似决定的其他用户，预测并推荐其他用户的其他商品。
a.【基于临域/内存的协同过滤】基于用户的/基于物品的
(1)【基于用户的协同过滤】寻找相似的有效用户（使用Jaccard距离/余弦距离/统计学的相关性距离，设定阈值选择得到），然后通过对其他用户评分的加权预测对其他物品的评分。
(2)【基于物品的协同过滤】寻找相似的物品，然后预测用户的评分。
b.【基于模型的协同过滤】


# 中介性 Betweenness vs模块度 Modularity
【中介性 Betweenness】分别对每个节点寻找最短的路径，每一个通路被所有的最短路径通过的次数，就是中介性。反映了那条通路在社群中的重要性。使用Givan-Newman算法计算得到。
【模块度 Modularity】当前分割后的（社群内部数量-分割后的期望数量）之差的总和。用来衡量一个网络被分为几个社群的效果。基于社群内的通路的数量和期望数量。如果一个社群和另外一个社群的通路太多，那么模块度就会很小，说明社群分割的不好。
