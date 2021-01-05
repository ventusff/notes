---
note_type: basic
title: math for deformations
---

* TOC
{:toc}
# math for deformations

 - resource
    - MIT [Continuum Mechanics 课程笔记](http://web.mit.edu/abeyaratne/Volumes/RCA_Vol_II.pdf)，Chapter 2
       - 重要参考资料：非常详尽、非常严谨、非常简洁明了，与线代知识紧密接续

## basics

 - 两个向量的`dot product`点积
    -  $$\vec{a} \cdot \vec{b}$$
 - 两个向量的`vector product`向量积；叉乘
    - $$\vec{a} \times \vec{b}$$
 - 两个向量的`tensor product`张量积
    - $$\vec{a} \otimes \vec{b}=\vec{a} \vec{b}^{\top}$$
    - e.g. $$\underset{3 \times 1}{\vec{a}}  \otimes \underset{3 \times 1}{\vec{b}} = \underset{3 \times 1}{\vec{a}} \quad \underset{1 \times 3}{\vec{b}^{\top}} = \underset{3 \times 3}{C}$$

## deformations

 - `deformation`：形变
    - 考虑一个物体（只需要是`continuum`，连续介质），其中一个`particle`粒子 $$x\in \mathcal{R}_0$$，属于`reference/undeformed configuration`参考物体空间 $$\mathcal{R}_0$$
    - 考虑物体变形以后，粒子$$\boldsymbol {\rm x}$$的新位置：$$\boldsymbol {\rm y} \in \mathcal{R}$$，属于`deformed configuration` 变形后的物体空间 $$\mathcal{R}$$
    - 从 reference configuration 到 deformed configuration的 `deformation` 形变定义为一个映射：
       - $$\boldsymbol {\rm y}=\hat{\boldsymbol {\rm y}}(\boldsymbol {\rm x})$$
       - takes $$\mathcal{R}_0 \rightarrow \mathcal{R}$$
    - `displacment vector field` $$\hat{u}(x)$$ 定义为
       - $$\hat{\boldsymbol {\rm u}}(\boldsymbol {\rm x})=\hat{\boldsymbol {\rm y}}(\boldsymbol {\rm x})-\boldsymbol {\rm x}$$
    - <img src="media/image-20210105200719506.png" alt="image-20210105200719506" style="zoom:67%;" />

## `Deformation Gradient Tensor` 形变梯度张量: deformation in the neighborhood of a particle 在一个粒子邻域中的变形

 - `deformation gradient tensor` 形变梯度张量
    - 为了考虑物体在粒子x处的`state of stress`应力状态等，需要考虑不仅在x处的变形，还要考虑粒子$$\boldsymbol {\rm x}$$的一个`small neighborhood`小邻域中的`all particles`所有粒子的变形
    - 直觉上讲：我们期望在这个局部小邻域球中的粒子经历的变形由`rigid translation`刚体平动、`rigid rotation`刚体旋转 和 `"straining"` "应变"组成；在后面将会准确公式化表述
    - 在一个generic粒子x处的 `deformation gradient tensor`形变梯度张量定义为：
       - $$\boldsymbol{\rm F}(\boldsymbol {\rm x})={\rm Grad} \; \boldsymbol {\rm y}(\boldsymbol {\rm x})$$
       - 这是用于描述、研究在邻域中的变形的主要量
       - $$\boldsymbol{\rm F}(\boldsymbol {\rm x})$$是一个2-tensor，它的元素为：
          - $$F_{ij}(\boldsymbol {\rm x})=\frac{\partial y_i(\boldsymbol {\rm x})}{\partial x_j} $$
          - 是一个3x3矩阵场 $$[F(\boldsymbol {\rm x})]$$
 - 一个`infinitesimal material fiber`无穷小 *物质* 纤维的deformation
    - 考虑两个在reference configuration中放置于$$\boldsymbol {\rm x}$$和$$\boldsymbol {\rm x} + {\rm d}\boldsymbol {\rm x}$$处的两个粒子p, q；
    - 考虑包含这两个粒子的`infinitesimal material fiber`无穷小 *物质* 纤维：$${\rm d}\boldsymbol {\rm x}$$
    - 在deformed configuration中，这两个粒子位于$$\boldsymbol {\rm y}(\boldsymbol {\rm x})$$和$$\boldsymbol {\rm y}(\boldsymbol {\rm x} + {\rm d}\boldsymbol {\rm x})$$处
    - 则这个infinitesimal material fiber的deformed [`image` 像](https://en.wikipedia.org/wiki/Image_(mathematics))（代数中的概念）用如下 **<u>向量</u>** 描述
       - $${\rm d}\boldsymbol {\rm y}=\boldsymbol {\rm y}(\boldsymbol {\rm x} + {\rm d}\boldsymbol {\rm x})-\boldsymbol {\rm y}(\boldsymbol {\rm x})$$
    - 由于这两个粒子p,q是相邻的，距离$$\lVert {\rm d}\boldsymbol {\rm x} \rVert$$很近，因此可以用`Taylor expansion`泰勒展开来近似该表达式
       - $${\rm d}\boldsymbol {\rm y}=\left( {\rm Grad} \; \boldsymbol {\rm y} \right ) {\rm d}\boldsymbol {\rm x} + {\rm O}(\lVert {\rm d}\boldsymbol {\rm x} \rVert^2) = \boldsymbol {\rm F} \; {\rm d}\boldsymbol {\rm x} + {\rm O}(\lVert {\rm d}\boldsymbol {\rm x} \rVert^2)$$
       - 即近似为：
          - $${\rm d}\boldsymbol {\rm y}=\boldsymbol {\rm F}{\rm d}\boldsymbol {\rm x}$$
       - 其组分为：
          - $${\rm d}y_i=\underset{j}{\sum} F_{ij} {\rm d}x_j$$ or $$\{y\}=[F]\{x\}$$
       - 注意，这个近似并不需要假设梯度场的变化小；它只需要假设p和q挨得足够近
       - 即：$$\boldsymbol {\rm F}$$ 把 无穷小未变形物质纤维$${\rm d}\boldsymbol {\rm x}$$ `carries into`带到了它在变形configuration中的位置$${\rm d}\boldsymbol {\rm y}$$处
    - <img src="media/image-20210105203801521.png" alt="image-20210105203801521" style="zoom:67%;" />
 - $$\boldsymbol {\rm F}$$应具有的一些假设
    - 行列式不为0
       - 考虑一个物理上可实现的变形：单个物质纤维不会裂变为两个物质纤维；两个不同的物质纤维不会合并为同一个物质纤维
       - 即，$${\rm d}\boldsymbol {\rm y}=\boldsymbol {\rm F}{\rm d}\boldsymbol {\rm x}$$需要是一个`one-to-one`一一映射，即$$\boldsymbol {\rm F}$$需要是 `non-sigular`非奇异矩阵：
          - $$J=\det \boldsymbol {\rm F} \neq 0$$
          - $$J$$也叫做 `Jacobian determinant` 雅克比行列式
    - 行列式为正值
       - 考虑三个独立物质纤维$${\rm d}\boldsymbol {\rm x}^{(i)}, i=1,2,3$$ 
       - 变形场 把这些纤维带到了3组位置：$${\rm d}\boldsymbol {\rm y}^{(i)}=\boldsymbol {\rm F} {\rm d}\boldsymbol {\rm x}^{(i)}, i=1,2,3$$
       - 如果这个变形把右手组合纤维$$\{ {\rm d}\boldsymbol {\rm x}^{(1)}, {\rm d}\boldsymbol {\rm x}^{(2)}, {\rm d}\boldsymbol {\rm x}^{(3)} \}$$带到了右手组合纤维$$\{ {\rm d}\boldsymbol {\rm y}^{(1)}, {\rm d}\boldsymbol {\rm y}^{(2)}, {\rm d}\boldsymbol {\rm y}^{(3)} \}$$，则称这个变形被称作是`preveserves orientation` `定向保留`的
          - 这里的[`orientation`](https://en.wikipedia.org/wiki/Orientation_(vector_space))是群论/向量空间中的概念：定向；其实反映的是一种类似`手性`的概念，orientation preserving即意味着手性得到保留；
          - 镜射变换，手性就不保留；
       - 一个变形是`orientation preserving`的，当且仅当行列式大于0：
          - $$J=\det \boldsymbol {\rm F} \gt 0$$
       - <img src="media/image-20210105210342160.png" alt="image-20210105210342160" style="zoom: 67%;" />
 - **变形的正式表述**
    - 如上，一个粒子$$\boldsymbol {\rm x}$$一般的邻域粒子$$\boldsymbol {\rm x} + {\rm d}\boldsymbol {\rm x}$$的变形正式表述为：
       - $$\boldsymbol {\rm y}(\boldsymbol {\rm x} + {\rm d}\boldsymbol {\rm x})=\boldsymbol {\rm y}(\boldsymbol {\rm x})+\boldsymbol {\rm F}{\rm d}\boldsymbol {\rm x}$$
       - 因此，想要描述粒子$$\boldsymbol {\rm x}$$的整个邻域的变形特征，就必须知道变形函数$$\boldsymbol {\rm y}(\boldsymbol {\rm x})$$和变形梯度张量$$\boldsymbol{\rm F}(\boldsymbol {\rm x})$$
          - 变形函数$$\boldsymbol {\rm y}(\boldsymbol {\rm x})$$刻画的是邻域粒子的平动
          - 变形梯度张量$$\boldsymbol{\rm F}(\boldsymbol {\rm x})$$刻画的是旋转和"应变"

## 特殊形变：一些均匀变形：纯拉伸，简单剪切变形

 - `homogeneous deformation` 均匀变形
   - 如果一个变形的变形梯度张量在整个ref区域$$\mathcal{R}_0$$都是常量，那么这个变形$$\boldsymbol {\rm y}(\boldsymbol {\rm x})$$就是一个`homogeneous deformation`
   - 因为变形梯度张量是一个常量，因此这种变形可以有如下表述：
     - $$\boldsymbol {\rm y}(\boldsymbol {\rm x})=\boldsymbol {\rm F} \boldsymbol {\rm x} + \boldsymbol {\rm b}$$
     - 其中，$$\boldsymbol {\rm F}$$是一个常张量，$$\boldsymbol {\rm b}$$是一个常向量
     - 这其实就是一个一般的仿射变换：平动，旋转，缩放，剪切

- 假设$$\{\boldsymbol {\rm e}_1, \boldsymbol {\rm e}_2, \boldsymbol {\rm e}_3\}$$ 是ref的`orthonormal basis` 标准正规基底；假设基底和一个单位cube的边对齐，从这个单位方出发进行变形

### `pure stretch` 纯拉伸

<img src="media/image-20210105211037474.png" alt="image-20210105211037474" style="zoom:50%;" />

 - $$\boldsymbol {\rm y}=\boldsymbol {\rm F} \boldsymbol {\rm x} \qquad where \qquad \boldsymbol {\rm F}=\lambda_1 \boldsymbol {\rm e}_1 \otimes \boldsymbol {\rm e}_1 + \lambda_2 \boldsymbol {\rm e}_2 \otimes \boldsymbol {\rm e}_2 + \lambda_3 \boldsymbol {\rm e}_3 \otimes \boldsymbol {\rm e}_3$$
 - 在标准正规基底$$\{\boldsymbol {\rm e}_1, \boldsymbol {\rm e}_2, \boldsymbol {\rm e}_3\}$$下
    - $$\boldsymbol {\rm e}_1 \otimes \boldsymbol {\rm e}_1$$就是$$\begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} \begin{pmatrix} 1 & 0 & 0 \end{pmatrix} =  \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$$
    - $$\boldsymbol {\rm F}=\begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & \lambda_2 & 0 \\ 0 & 0 & \lambda_3  \end{pmatrix}$$
    - $$\lambda_1, \lambda_2, \lambda_3$$代表在3个基底方向上的拉压比率
 - 如果$$\lambda_1 \lambda_2 \lambda_3 = 1$$，则是`isochoric`等容的变形

 - `pure dilatation` 纯膨胀
    - $$\lambda_1 = \lambda_2 = \lambda_3$$
 - `uniaxial stretch` 单轴拉伸
    - $$\lambda_2 = \lambda_3 =1$$
    - $$\boldsymbol {\rm F}=\lambda_1 \boldsymbol {\rm e}_1 \otimes \boldsymbol {\rm e}_1 + \boldsymbol {\rm e}_2 \otimes \boldsymbol {\rm e}_2 + \boldsymbol {\rm e}_3 \otimes \boldsymbol {\rm e}_3 = \boldsymbol{\rm I} + (\lambda_1-1) \boldsymbol {\rm e}_1 \otimes \boldsymbol {\rm e}_1$$
    - 在标准正规基底$$\{\boldsymbol {\rm e}_1, \boldsymbol {\rm e}_2, \boldsymbol {\rm e}_3\}$$下
       - $$\boldsymbol {\rm F}=\begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1  \end{pmatrix}$$
    - 更一般地：
       - $$\boldsymbol {\rm F}= \boldsymbol{\rm I} + (\lambda_1-1) \boldsymbol {\rm n} \otimes \boldsymbol {\rm n}, \qquad \lVert \boldsymbol {\rm n} \rVert=1$$

### `simple shearing deformation` 简单剪切变形

<img src="media/image-20210105214214790.png" alt="image-20210105214214790" style="zoom:67%;" />

 - $$\boldsymbol {\rm y}=\boldsymbol {\rm F} \boldsymbol {\rm x} \qquad where \qquad \boldsymbol {\rm F}=\boldsymbol {\rm I} + k \;  \boldsymbol{\rm e}_1 \otimes \boldsymbol {\rm e}_2$$
 - 在标准正规基底$$\{\boldsymbol {\rm e}_1, \boldsymbol {\rm e}_2, \boldsymbol {\rm e}_3\}$$下
    - $$\boldsymbol{\rm e}_1 \otimes \boldsymbol {\rm e}_2$$ 就是$$\begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} \begin{pmatrix} 0 & 1 & 0 \end{pmatrix} =  \begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$$
    - $$\boldsymbol {\rm F}=\begin{pmatrix} 1 & k & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1  \end{pmatrix}$$
 - $$\boldsymbol {\rm u}(\boldsymbol {\rm x})=\boldsymbol {\rm y}(\boldsymbol {\rm x})-\boldsymbol {\rm x}=\boldsymbol {\rm F}\boldsymbol {\rm x}-\boldsymbol {\rm x}=k \;  \boldsymbol{\rm e}_1 \otimes \boldsymbol {\rm e}_2 \; \boldsymbol {\rm x}=kx_2\boldsymbol {\rm e}_1$$
    - 意味着$$x_2={\rm constant}$$平面朝着$$x_1$$-方向 刚体平动，平动量为$$kx_2$$
    - 把矩阵$$\boldsymbol {\rm F}$$中出现$$k$$的那个剪切量，行标的方向称为`shearing direction`剪切方向，列标的方向对应法向量的平面称为`shearing/glide plane`剪切平面
 - 更一般地：
    - $$\boldsymbol {\rm F}=\boldsymbol {\rm I} + k \;  \boldsymbol{\rm m} \otimes \boldsymbol {\rm n}, \qquad \lVert \boldsymbol {\rm m} \rVert=\lVert \boldsymbol {\rm n} \rVert = 1, \qquad \boldsymbol {\rm m} \cdot \boldsymbol {\rm n} = 0 $$
    - $$\boldsymbol {\rm m}$$为剪切方向，$$\boldsymbol {\rm n}$$法向量对应的平面为剪切平面

## 一般形变：研究长度、朝向、夹角、体积、表面的改变

### 一个物质纤维的改变：长度、朝向

<img src="media/image-20210105215817089.png" alt="image-20210105215817089" style="zoom:67%;" />

 - 长度改变比例：$$\lVert \boldsymbol {\rm F} \boldsymbol {\rm n}_0 \rVert$$
 - 新朝向：$$\frac {\boldsymbol {\rm F} \boldsymbol {\rm n}_0}{\lVert \boldsymbol {\rm F} \boldsymbol {\rm n}_0 \rVert}$$

### 两个物质纤维的改变：夹角

<img src="media/image-20210105220321108.png" alt="image-20210105220321108" style="zoom:67%;" />

 - 考虑由$$\boldsymbol {\rm n}_0^{(1)}$$，$$\boldsymbol {\rm n}_0^{(2)}$$定义的夹角
 - 新夹角大小：$$\cos{\theta_y}= \frac {\boldsymbol {\rm F}\boldsymbol {\rm n}_0^{(1)} \cdot \boldsymbol {\rm F}\boldsymbol {\rm n}_0^{(2)}} { \lVert \boldsymbol {\rm F}\boldsymbol {\rm n}_0^{(1)} \rVert  \lVert \boldsymbol {\rm F}\boldsymbol {\rm n}_0^{(2)} \rVert}$$

### 一块体积物质的改变：体积

<img src="media/image-20210105220459906.png" alt="image-20210105220459906" style="zoom:67%;" />

 - 考虑由$${\rm d}\boldsymbol {\rm x}^{(1)}, {\rm d}\boldsymbol {\rm x}^{(2)}, {\rm d}\boldsymbol {\rm x}^{(3)}$$ 定义的`tetrahedron`四面体
 - 体积改变：$${\rm d}V_y=J {\rm d}V_x \qquad where \qquad J=\det\boldsymbol {\rm F}$$

### :pushpin: :warning: 一块表面物质的改变：面积，平面法向量

<img src="media/image-20210105220824590.png" alt="image-20210105220824590" style="zoom:67%;" />

 - 考虑由$${\rm d}\boldsymbol {\rm x}^{(1)}, {\rm d}\boldsymbol {\rm x}^{(2)}$$ 定义的`parallelogram`平行四边形
 - 新法向量：$$\boldsymbol {\rm n}=\frac {\boldsymbol {\rm F}^{-\top} \boldsymbol {\rm n}_0 }  {\lVert  \boldsymbol {\rm F}^{-\top} \boldsymbol {\rm n}_0  \rVert}$$
 - 面积变化比例：$${\rm d}A_y={\rm d}A_x \, J \lVert \boldsymbol {\rm F}^{-\top} \boldsymbol {\rm n}_0 \rVert$$
 - 注意：平面法向量一般不继承变形操作
    - 变形后的平面的法向量$$\boldsymbol {\rm n}$$，**<u>一般不与</u>** 变形前平面法向量$$\boldsymbol {\rm n}_0$$变形后的向量$$\boldsymbol {\rm F} \boldsymbol {\rm n}_0$$ 平行
    - 变形前与平面垂直的法向量$$\boldsymbol {\rm n}_0$$，在变形后的向量$$\boldsymbol {\rm F} \boldsymbol {\rm n}_0$$ **<u>一般不与</u>** 变形后的平面垂直
    - [ ] Q: 有待数学证明
       -  若要使平面法向量 **<u>处处</u>** 继承变形操作，需要对任意$$\boldsymbol {\rm n}_0$$满足$$\boldsymbol {\rm F}^{-\top} \boldsymbol {\rm n}_0$$与$$\boldsymbol {\rm F} \boldsymbol {\rm n}_0$$方向一致；
       -  $$\boldsymbol {\rm F}^{\top}\boldsymbol {\rm F} \boldsymbol {\rm n}_0=\alpha \boldsymbol {\rm n}_0$$ 对于任意$$\boldsymbol {\rm n}_0$$均成立
       -  意味着$$\boldsymbol {\rm F}^{\top}\boldsymbol {\rm F}$$是正交矩阵？变形是homogeneous的，而且只包含旋转+等比缩放？

## 特殊形变：`rigid deformation`刚性形变

 - 刚性形变的定义
    - 物体中的所有对粒子在变形后保持变形前距离
    - i.e. 任意两个粒子$$\boldsymbol {\rm z}$$，$$\boldsymbol {\rm x}$$在变形前在ref configuration中距离为$$\lVert \boldsymbol {\rm z}-\boldsymbol {\rm x} \rVert $$，应与变形后在deformed configuration中距离$$\lVert \boldsymbol {\rm y}(\boldsymbol {\rm z})-\boldsymbol {\rm y}(\boldsymbol {\rm x}) \rVert $$相等
    - $$\lVert \boldsymbol {\rm y}(\boldsymbol {\rm z})-\boldsymbol {\rm y}(\boldsymbol {\rm x}) \rVert^2 = \underset{i}{\sum} \left[ y_i(\boldsymbol {\rm z}) - y_i(\boldsymbol {\rm x}) \right] \left[ y_i(\boldsymbol {\rm z}) - y_i(\boldsymbol {\rm x}) \right] = \underset{i}{\sum} (z_i-x_i)(z_i-x_i) \qquad {\rm for \; all \;} \boldsymbol {\rm x},\boldsymbol {\rm z} \in \mathcal{R}_0$$
    - 上式等价于 $$\boldsymbol {\rm F}^{\top}(\boldsymbol {\rm x}) \boldsymbol {\rm F}(\boldsymbol {\rm z})=\boldsymbol {\rm I} \qquad {\rm for \; all \;} \boldsymbol {\rm x},\boldsymbol {\rm z} \in \mathcal{R}_0$$
    - 上式等价于$$\boldsymbol {\rm F}(\boldsymbol {\rm x})$$是一个 **<u>常量张量</u>** ，且是一个 **<u>旋转矩阵</u>**（行列式为1的正交矩阵）

<details markdown="1"><summary markdown="0">证明：点击展开</summary>

 - 首先两边对$$x_j$$求偏导
    - $$\underset{i}{\sum} -2 F_{ij}(\boldsymbol {\rm x})(y_i(\boldsymbol {\rm z}) - y_i(\boldsymbol {\rm x}))=-2(z_j-x_j)$$
 - 再两边对$$z_k$$求偏导：
    - $$-2 F_{ij}(\boldsymbol {\rm x})F_{ik}(\boldsymbol {\rm z})= -2\delta_{jk} =\begin{cases} -2 & \text{if $j = k$ } \\ 0 & \text{if $j \neq k$ }  \end{cases}$$
    - i.e. $$F_{ij}(\boldsymbol {\rm x})F_{ik}(\boldsymbol {\rm z})= \delta_{jk}$$
    - 即得： $$\boldsymbol {\rm F}^{\top}(\boldsymbol {\rm x}) \boldsymbol {\rm F}(\boldsymbol {\rm z})=\boldsymbol {\rm I} \qquad {\rm for \; all \;} \boldsymbol {\rm x},\boldsymbol {\rm z} \in \mathcal{R}_0$$
       - 可得出$$\boldsymbol {\rm F}(\boldsymbol {\rm x})$$处处行列式为1
       - 代入$$\boldsymbol {\rm z}=\boldsymbol {\rm x}$$可得$$\boldsymbol {\rm F}^{\top}(\boldsymbol {\rm x}) \boldsymbol {\rm F}(\boldsymbol {\rm x})=\boldsymbol {\rm I}\qquad {\rm for \; all \;} \boldsymbol {\rm x}\in \mathcal{R}_0$$，即$$\boldsymbol {\rm F}(\boldsymbol {\rm x})$$处处正交
       - 两边同乘$$\boldsymbol {\rm F}(\boldsymbol {\rm x})$$，可得$$\boldsymbol {\rm F}(\boldsymbol {\rm z})=\boldsymbol {\rm F}(\boldsymbol {\rm x})\qquad {\rm for \; all \;} \boldsymbol {\rm x},\boldsymbol {\rm z} \in \mathcal{R}_0$$，即$$\boldsymbol {\rm F}(\boldsymbol {\rm x})$$是一个常量张量

</details>

 - 结论：<u>刚性形变对应的形变梯度张量是一个常旋转矩阵</u>
    - 记对所有$$\boldsymbol {\rm x} \in \mathcal{R}_0$$ ，$$\boldsymbol {\rm F}(\boldsymbol {\rm x})=\boldsymbol {\rm Q}$$，$$\boldsymbol {\rm Q}$$是一个 **<u>旋转矩阵</u>**（行列式为1的正交矩阵）
    - 则刚性形变的形式为：
       - $$\boldsymbol {\rm y}(\boldsymbol {\rm x})=\boldsymbol {\rm Q} \boldsymbol {\rm x} + \boldsymbol {\rm b}$$

## 一般形变：形变梯度张量 分解为 旋转 + stretch

