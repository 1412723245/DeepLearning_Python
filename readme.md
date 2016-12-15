深度学习 Deep Learning
==============

- 有关神经网络的部分可以查看[这里](https://github.com/lawlite19/MachineLearning_Python)的`BP神经网络`的部分：[https://github.com/lawlite19/MachineLearning_Python](https://github.com/lawlite19/MachineLearning_Python)

## 一、CNN卷积神经网络
- 参考文章：http://cs231n.github.io/convolutional-networks/#conv

### 1、概述
- 典型的深度学习模型就是很深层的神经网络，包含多个`隐含层`，多隐层的神经网络很难直接使用`BP算法`进行直接训练，因为反向传播误差时往往会发散，很难收敛
- `CNN`节省训练开销的方式是**权共享weight sharing**，让**一组**神经元使用相同的权值
- 主要用于**图像识别**领域

### 2、卷积（Convolution）特征提取
- `卷积核`（Convolution Kernel），也叫`过滤器filter`，由对应的权值`W`和偏置`b`体现
- 下图是`3x3`的卷积核在`5x5`的图像上做卷积的过程，就是矩阵做**点乘**之后的和
![enter description here][1]   
第`i`个隐含单元的输入就是：![$${W_{\rm{i}}}{x_{small}} + {b_i}$$](http://latex.codecogs.com/png.latex?%5Cdpi%7B120%7D%20%5Clarge%20%24%24%7BW_%7B%5Crm%7Bi%7D%7D%7D%7Bx_%7Bsmall%7D%7D%20&plus;%20%7Bb_i%7D%24%24)，其中![$${x_{small}}$$](http://latex.codecogs.com/png.latex?%5Cdpi%7B120%7D%20%5Clarge%20$${x_{small}}$$)就时与过滤器filter过滤到的图片
- 另外上图的步长`stride`为`1`，就是每个`filter`每次移动的距离
- 卷积特征提取的原理
 - 卷积特征提取利用了自然图像的统计平稳性，这一部分学习的特征也能用在另一部分上，所以对于这个图像上的所有位置，我们都能使用同样的学习特征。
 - 当有多个`filter`时，我们就可以学到多个特征，例如：轮廓、颜色等

- 多个过滤器`filter`（卷积核）
 - 例子如下
![enter description here][2]
 - 一张图片有`RGB`三个颜色通道，则对应的filter过滤器也是三维的，图像经过每个`filter`做卷积运算后都会得到对应提取特征的图像，途中两个`filter`:W0和W1,输出的就是**两个**图像
 - 这里的步长`stride`为`2`（一般就取2,3）
 - 在原图上添加`zero-padding`，它是`超参数`，主要用于控制输出的大小
 - 同样也是做卷积操作，以下图的一步卷积操作为例：   
 与w0[:,:,0]卷积：`0x(-1)+0x0+0x1+0x1+0x0+1x(-1)+1x0+1x(-1)+2x0=-2`   
 与w0[:,:,1]卷积：`2x1+1x(-1)+1x1=2`   
 与w0[:,:,2]卷积：`1x(-1)+1x(-1)=-2`   
 最终结果：`-2+2+(-2)+1=-1`  (1为偏置)
![enter description here][3]

### 3、池化（Pooling）
- `Pooling`过程
 - 把提取之后的特征看做一个矩阵，并在这个矩阵上划分出几个不重合的区域，
 - 然后在每个区域上计算该区域内特征的**均值**或**最大值**，然后用这些均值或最大值参与后续的训练
 ![enter description here][4]
 -下图是使用最大`Pooling`的方法之后的结果
 ![enter description here][5]
- `Pooling`的好处
 - 很明显就是减少参数
 - `Pooling`就有平移不变性（(translation invariant）
 如图`feature map`是`12x12`大小的图片，Pooling区域为6x6,所以池化后得到的`feature map`为`2x2`,假设白色像素值为1，灰色像素值为0，若采用`max pooling`之后，左上角窗口值为**1**
 ![enter description here][6]      
 将图像右移一个像素，左上角窗口值仍然为**1**
 ![enter description here][7]     
 将图像缩放之后，左上角窗口值仍然为**1**
 ![enter description here][8]
- `Pooling`的方法中`average`方法对背景保留更好，`max`对纹理提取更好


  [1]: ./images/CNN_01.gif "CNN_01.gif"
  [2]: ./images/CNN_02.gif "CNN_02.gif"
  [3]: ./images/CNN_03.png "CNN_03.png"
  [4]: ./images/CNN_04.gif "CNN_04.gif"
  [5]: ./images/CNN_05.png "CNN_05.png"
  [6]: ./images/CNN_06.png "CNN_06.png"
  [7]: ./images/CNN_07.png "CNN_07.png"
  [8]: ./images/CNN_08.png "CNN_08.png"