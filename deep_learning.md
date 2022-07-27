# Deep Learning
## 1 Anchor-based & Anchor-free
### Object Detection
* DenseBox: 
  * FCN后得到5个通道的feature map，分别代表置信度，对应像素坐标到bbox四边的距离。
  * 以bbox的中心点为圆心，在圆内的区域设置为正样本。
  * 密集预测。
* YOLOv1: 
  * Conv + Pooling + Activate后得到S * S * (B * 5 + C)的feature map，C是类别数，B代表bbox个数，5代表置信度和(x, y, w, h)
  * 以gt的bbox中心点落入哪个grid cell确定正样本。
  * 相比DenseBox预测细粒度更大，因此需要B来避免多个目标落入同一个grid cell
