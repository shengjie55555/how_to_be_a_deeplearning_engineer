# Deep Learning
## 1 Visual 2D Object Detection
### Anchor-free
核心在于如何定义gt，并解决正负样本不均衡的问题。
* DenseBox: 
  * FCN后得到5个通道的feature map，分别代表置信度，对应像素坐标到bbox四边的距离。
  * 以bbox的中心点为圆心，在圆内的区域设置为正样本。
  * 密集预测。
* YOLOv1: 
  * Conv + Pooling + Activate后得到S * S * (B * 5 + C)的feature map，C是类别数，B代表bbox个数，5代表置信度和(x, y, w, h)
  * 以gt的bbox中心点落入哪个grid cell确定正样本。
  * 相比DenseBox预测细粒度更大，因此需要B来避免多个目标落入同一个grid cell
* CenterNet:
  * Backbone后接Corner Pooling和Center Pooling来得到Corner Heatmaps和Center Heatmaps，然后可以得到角点及其embedding和中心点，通过embedding判断哪两个是属于一个object，然后再判断两个角点组成的bbox中是否含有中心点来剔除错误的bbox。
  * 以gt中心为Guassion中心，得到正样本分布，避免正负样本的不均衡
* CornerNet：
  * 逐类别预测两个Heatmap，代表左上和右下，输出为Heatmap，embedding和offset。Heatmap分辨率比原图低，需要offset来refine。embedding则用于计算最小距离进行匹配。 

## 2 Trajectory Prediction
### Anchor-free/based
Anchor-based：需要复杂的手工方法来生成候选目标，限制了可能的搜索空间，但是可以考虑先验信息，得到的轨迹更加合理。  
Anchor-free：实现简单，可以让模型更好的根据数据来确定可能的输出模态。但是可能会产生极其不合理的轨迹。（自动驾驶更可怕的是完全没预测到，而不是预测有误差）。
* LaneRCNN:
  * 通过道路中心线生成候选终点，然后再进行分类和offset回归得到更加精确的终点。
* PRIME：
  * 考虑道路限制和车辆动力学，通过规划的方法实现生成feasible trajectories，然后采用learning-based evaluator来评分，选择top-k的轨迹。
* DenseTNT & DSP:
  * 根据场景信息得到一系列的goal candidates，（DenseTNT是根据车道线，DSP是根据drivable area），然后采用图结构进行feature之间的传播。
* KEMP & ATDS & LaneGCN
  * 直接通过MLP生成未来轨迹，采用WTA策略保证多模态。
  * 生成goal point，key points，再得到full trajectory。对于长距离预测效果更好。

### Backbone
* CNN
  * HOME：采用不同的颜色编码不同元素，多通道灰度图表示历史轨迹，最后concatenate得到multi-channel images，作为CNN backbone的输入。
* GNN
  * VectorNet:
    * 先用类似PointNet的方法得到每个多段线的特征，再用一个fully-connetecd的图网络进行交互建模。
  * LaneGCN：
    * 考虑道路的连接关系，得到四种邻接矩阵，并考虑沿道路方向的长距离交互（邻接矩阵相乘）。
* Transformer
  * mmTransformer
    * 初始化一系列Trajectory Proposals，然后通过Motion Extractor，Map Extractor和Social Constructor来更新这些Proposals，最后通过Generator和Selector得到top-k的轨迹
  * Wayformer
    * 将历史轨迹、高精度地图、交通灯状态和交互表示成A * S * T * D的Tensor，然后采用self-attention更新每个输入自身状态，采用cross-attention考虑各个输入之间的交互。
    * 设计了三种融合模式：前融合，后融合和分层融合（组合了前融合和后融合）
    * 设计了分解注意里模型，对于序列长度S * T的输入，分解成S和T，即在spatial维度和temporal分开做self-attention，这里面还考虑了s和t交替，还是一半s一半t。

## 3 Point Cloud 3D Object Detection
### PointNet & PointNet++
#### PointNet
* 输入n * 3的Tensor，通过MLP和T-Net得到高维度特征。T-Net的输出为一个变换矩阵，保证模型对特定空间转换的不变性。MLP就是纯粹的提升维度。
* 最后通过maxpooling得到全局特征做分类任务。如果是分割任务的话，则将maxpooling的全局特征和每个点的特征进行拼接，然后对每个点进行分类。
* 只考虑了点自身和全局的特征，没有提取局部特征。对于数量较多的点云，计算效率低下。
#### PointNet++
* 最远点采样：随机选择一个点作为初始点；计算未选择点集中距离已选择点集中距离最远的点，加入已选择点集；迭代上述操作直到数量满足要求。
* 根据采样的点，向外扩展query ball的半径，直到数量达到要求作为一个子区域。
* 对于每个子区域采用PointNet提取子区域的全局特征
* 两种特征融合方法：
  * Multi-scale grouping：对于一个中心点，采用不同的半径，分别提取特征并并拼接。
  * Multiresolution grouping：对于30个点，先划分为3个包含10个点的子区域提取3个特征后，对3个子区域再划分为2个包含两个点（可以有交集）的子区域，在分别提取后拼接。
