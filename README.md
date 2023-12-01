#战略坐标#

战略坐标是指在制定和执行战略时所采用的一种方法，用于确定组织在竞争环境中的位置和方向。它通常包括两个维度：市场需求和竞争优势。
市场需求维度包括了市场规模、市场增长率、市场分割、市场趋势等因素。这些因素可以帮助组织了解市场的潜在机会和风险，从而确定组织的目标市场和发展方向。
竞争优势维度包括了组织在竞争中相对于其他竞争对手的优势，如产品差异化、成本优势、品牌影响力等。通过确定自身的竞争优势，组织可以制定相应的战略，并在市场中取得竞争优势。
战略坐标的应用场景包括但不限于以下几个方面：

1. 市场定位：通过分析市场需求和竞争优势，确定组织在市场中的定位，确定目标市场、目标客户群体和市场细分策略。
2. 竞争策略：根据竞争优势和市场需求，制定相应的竞争策略，包括差异化策略、成本领先策略、专注策略等。
3. 发展方向：基于市场需求和竞争优势，确定组织的发展方向，包括产品线扩展、市场拓展、国际化等。
4. 决策支持：战略坐标可以为组织的决策提供支持和指导，帮助组织在复杂和不确定的环境中做出明智的决策。

1 战略坐标的机理图
![](file:///C:\Users\69493\AppData\Local\Temp\ksohtml24440\wps1.png)
1.1 战略坐标的计算公式
战略坐标= 市场需求权重 × 市场需求得分 + 竞争优势权重 × 竞争优势得分
```
import numpy as np
from sklearn.cluster import KMeans

# 生成示例数据
data = np.random.rand(100, 2)

# 使用K-means聚类算法进行聚类
kmeans = KMeans(n_clusters=3)
kmeans.fit(data)

# 计算类团密度
cluster_density = kmeans.inertia_

# 计算类团向心度
cluster_centroid = kmeans.cluster_centers_
data_centroid = np.mean(data, axis=0)
cluster_centrality = np.linalg.norm(cluster_centroid - data_centroid)

print("类团密度：", cluster_density)
print("类团向心度：", cluster_centrality)
```
2 战略坐标的可视化
2.1战略坐标的图绘制有几个需要注意的点：
1. 需要注意Cluster的定义和分类
2. 我的scatter里面其实是定义了size的，这样可以根据不同领域的节点数值大小而变化，这部分做微观分析的时候有着更深入的研究。
3. 凸边的绘制其实是参考最外侧的连边，判定的规则需要新定义，具体而言就是计算x（cluster_density）和y（cluster_centrality）的距离，判定该区域的节点是距离中心点最远的。
```def encircle(x,y, ax=None, **kw):
    if not ax: ax=plt.gca()
    #计算凸边    
    p = np.c_[x,y]
    hull = ConvexHull(p)
    #加边界
    poly = plt.Polygon(p[hull.vertices,:], **kw)
    ax.add_patch(poly)
#ec是线 fc是颜色
encircle(x0, y0, ec="k", fc="#37ad6b", alpha=0.15) 
```
4. 数据的格式可以参考这个图，当然战略坐标的应用场景有很多，在做企业的市场竞争也能经常用得到，指标可以自己搭配，然后做一个数据降维（PCA、LDA、t-SNE、NMF、ICA等等），并不局限于广义上的类团密度和类团向心度（但是现有研究做这个的很少，反而是业界做得比较多）
![[Pasted image 20231201101904.png]]

2.2 宏观战略坐标
https://github.com/LaVineLeo/Strategic-coordinate-scatter-plot/blob/main/%E5%AE%8F%E8%A7%82%E5%9B%BE.jpg
2.3微观战略坐标
其实微观战略坐标分析还能再做一个战略坐标（类似于套娃Doge），因为这些小节点可以理解为是一个领域内（可以是不同行业、不同地域的）的企业数量，举个例子某区域地产公司的战略坐标分析，这部分其实可做的点有很多（欢迎大家来探讨）。
![[Pasted image 20231201101011.png]]


更多的论文细节可以参考以下这篇文章：
https://www.researchgate.net/publication/367110731_Data-Driven_Evolution_Analysis_and_Trend_Prediction_of_Hotspots_in_Global_PPP_Research

