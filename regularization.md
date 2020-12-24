[[_TOC_]]

> regularization：改进问题的conditioning；把问题从ill-posed变成well-posed

# math

## Laplace–Beltrami operator

 - 拉普拉斯-贝尔特拉米算子
 - 在微分几何中，拉普拉斯算子可以推广定义到曲面上，或者更一般地黎曼流形、伪黎曼流形上，这个更一般的算子就叫做拉普拉斯-贝尔斯特拉算子；
 - 与拉普拉斯算子一样，拉普拉斯-贝尔特拉米算子定义为梯度的散度

# weight decay

 - [toward data science](https://towardsdatascience.com/this-thing-called-weight-decay-a7cd4bcfccab)
 - 

# [Tikhonov regularization](https://en.wikipedia.org/wiki/Tikhonov_regularization)

- 是`非适定性问题`的正则化的最常见的方法
- 在统计学中被称为 `ridge regression`脊回归
- 在机器学习中，被称为`weight decay` 权重衰减
- 又被称作 `linear regularization` 线性正则化
- 为了解$`\boldsymbol{A}\boldsymbol{\rm x}=\boldsymbol{\rm b}`$的问题，标准方法是最小二乘法<br>然而，如果x没有解或者有超出一个解(i.e. 方程不是unique的)<br>那么问题就是ill-posed；
  - 这种情况下，ordinary 最小二乘问题问题变得 overdetermined / more often an undetermined system<br>许多现实世界问题，从A到b的映射往往是低通滤波器；因此，在解逆问题的时候，逆映射就会变成高通滤波器，表现出我们不需要的那些放大噪声（最小的 eigenvalues / singular values 在逆映射会变得最大）的趋向
  - 另外，ordinary 最小二乘implicitly nullifies every element of the reconstructed version of x that is in the null-space of A，rather than allowing for a model to be used as a prior for x。最小二乘对于位于A的null-space的那些x的元素不会利用先验，而是nullify 他们
  - ordinary least squares 的目标：最小化平方残差和<br>$`\lVert \boldsymbol{A}\boldsymbol{\rm x}-\boldsymbol{\rm b} \rVert^2_2`$，其中$`\lVert \cdot \rVert^2_2`$代表欧几里得范数
  - 为了给出一个对带有需求属性的特定解的偏好，Tikhonov regularization 在最小化目标中额外加入一项正则化：<br>$`\lVert \boldsymbol{A}\boldsymbol{\rm x}-\boldsymbol{\rm b} \rVert^2_2 + \lVert \Gamma \boldsymbol{\rm x} \rVert^2_2`$<br>for some suitably chosen TIkhonov matrix $`\Gamma`$ 
    - 如选择单位阵的乘积：$`\Gamma=\alpha I`$，意味着偏好那些有更小的norm的solution (i.e. $`L_2`$ regularization)
    - 如选择high-pass 算子（如微分算子或加权傅里叶算子）可以用来保证平滑性，如果underlying vector基本是线性的
  - 这样的正则化可以改善问题的conditioning，从而可以得到一个直接的数值解
- 更一般的tikhonov regularization
  - [ ] (笔者的)大概理解：不应是欧几里得范数$`\boldsymbol{\rm x}^{\top} \boldsymbol{\rm x}`$，而是更一般的范数$`\boldsymbol{\rm x}^{\top}Q \boldsymbol{\rm x}`$
  - $`\lVert \boldsymbol{A}\boldsymbol{\rm x}-\boldsymbol{\rm b} \rVert^2_{P} + \lVert \Gamma \boldsymbol{\rm x} \rVert^2_{Q}`$, 其中$`\lVert x \rVert^2_{Q}`$代表weighted norm squared $`\boldsymbol{\rm x}^{\top}Q \boldsymbol{\rm x}`$
  - 这种意义下，Tikhonov matrix其实是给出的矩阵的分解矩阵：$`Q=\Gamma^{\top}\Gamma`$

# [manifold regularization](https://en.wikipedia.org/wiki/Manifold_regularization)

- 在机器学习中，manifold regularization是一种 利用数据集的<u>shape</u> 来约束从数据集学到的函数的技术
- **manifold learning**
  - 因为在许多机器学习问题中，数据并没有cover整个输入空间；
    - e.g. 人脸识别系统 并不需要识别任何可能的图像，而是只学习那些包含人脸的图像空间子集
  - manifold learning技术假设数据来自于一个流形；
  - manifold learning技术假设将要学到的函数是 *smooth*的：带有不同标签的数据不太可能彼此接近/集中在一起，因此标签函数在<u>含有很多数据点的区域</u>不应改变太快
    - 基于这种假设，manifold regularization算法可以额外利用那些unlabeled data来inform 哪些地方学到的函数要变地快，哪些地方变地慢；
    - 这里用到了Tikhonov regularization的延伸
- **manifold regularization**
  - 是正则化的一种，防止过拟合，通过惩罚complex solution来保证问题well-posed
  - 是 `Tikhonov regularization` 吉洪诺夫正则化 的延伸
  - `manifold assumption`：即问题中的数据不是来自于整个输入空间$`X`$，而是来自于其中的一个非线性流形$`M \subset X`$ 
    - 因此，这个流形 / `intrinsic space`的<u>geometry</u>就可以用来决定正则化项
  - 这种算法常可以用来扩展`semi-supervised`半监督学习和`transductive learning`"直推"式学习，因为那些算法中都有unlabeled data

## Laplacian regularization / Laplacian norm

 - 这个名称来自于拉普拉斯算子（梯度的散度）
 - 对流形M的梯度进行操作，即提供了一种目标函数有多平滑的衡量；
 - 一个平滑的函数，应当在输入数据稠密的地方改变缓慢；<br>i.e. 梯度$`\nabla_Mf(x)`$在那些`marginal probability density` $`\mathcal{P}_X(x)`$大的地方足应当小<br>$`\mathcal{P}_X(x)`$：the probabilistic density of a randomly drawn data point appearing at x，一个随机采样的数据点在x处出现的概率密度<br>即：$`\lVert f \rVert^2_I=\int_{x\in M} \lVert \nabla_Mf(x) \rVert^2 {\rm d}\mathcal{P}_X(x)`$
 - 然而实践中，由于边缘分布$`\mathcal{P}_X`$是未知的，这个范数并不能直接计算；但是它可以从所提供的数据中估计
    - 具体来说，如果输入点之间的距离可以用`graph`图来表示，那么`graph`的`laplacian matrix`拉普拉斯矩阵可以用来估计边缘概率分布
    - 假设数据有$`\mathcal{l}`$个有标签的样本(有输入x和输出y的pair)，$`u`$个无标签的样本
    - 定义*W*是graph的权重矩阵，其中$`W_{ij}`$是输入数据点$`x_i`$和$`x_j`$之间的距离度量
    - 定义*D*是对角阵：$`D=\sum_{j=1}^{\mathcal{l}+u}W_{ij}`$
    - 定义*L*为$`L=D-W`$即为拉普拉斯矩阵
    - 当数据点的个数$`\mathcal{l}+u`$逐渐增加时，矩阵$`L`$就可以收敛到`Laplace–Beltrami operator`拉普拉斯-贝尔特拉米算子$`\Delta_M`$ (推广到一般曲面、黎曼流形、伪黎曼流形的拉普拉斯算子)，即梯度的`散度`
    - 定义$`\boldsymbol{\rm f}`$为函数$`f`$在这些数据点上的函数值$`\boldsymbol{\rm f}=[f(x_1), \ldots,f(x_{\mathcal{l}+u})]^{\top}`$
    - 则这个intrinsic norm可以这样被估计：<br>$`\lVert f \rVert^2_I=\frac {1}{(\mathcal{l}+u)^2} \boldsymbol{\rm f}^{\top}L\boldsymbol{\rm f}`$