---

**`< layout-conditional 2.5D scene synthesis >"End-to-End Optimization of Scene Layout"`**  
**[** `CVPR2020(oral)` **]** **[[paper]](https://arxiv.org/pdf/2007.11744.pdf)** **[[code]](https://github.com/aluo-x/3D_SLN)** **[[video]](https://www.youtube.com/watch?v=1GQ8IkI6ZJM)** **[[web]](http://3dsln.csail.mit.edu/)** **[** :mortar_board: `MIT: CSAIL, CMU, Stanford` **]**   
**[**  `Andrew Luo, Zhoutong Zhang, Jiajun Wu, Joshua B. Tenenbaum  `  **]**  
**[** _`conditional scene synthesis`, `2.5D`,`variational generative model`， `graph-based variational auto-encoders`_ **]**  

<details>
  <summary>Click to expand</summary>


| ![image-20201028170115727](media/image-20201028170115727.png) |
| ------------------------------------------------------------ |
| scene generation + refinement                                |




- **Motivation**
  
  - Traditional scene graph based image generation (e.g. *[CVPR2018] sg2im*)
  
    - 在image space中建模物体关系(而不是scene space)
    - 没有显式的3D物体概念（只有像素）
  - Layout Generation (e.g. *[SIGGRAPH2018] Deep Convolutional Priors for Indoor Scene Synthesis*)
  
    - no spatial-conditioning
    - auto-regressive 自回归 (slow)
  
      - [ ] what?
  - 核心issues
  
    - scene space下的3D关系
    - 解耦的布局、形状、图像构成
    - 基于2.5D+语义目标的object locations的refinement
  
      - [ ] what?
- **主要贡献**
  - 3D-SLN model 可以从一个scene graph生成**diverse and accurate** scene layouts 
  - 3D scene layouts 可以用 2.5D+语义信息 finetune
  - 对于layout synthesis和image synthesis很有用
- **数据集/数据特征**

  - 物体3D model 是直接从SUNCG数据集中 retrive的；选择类别内最相似的bbox
  - layout的数据结构：
- **layout generator的网络架构**

| ![image-20201028170249809](media/image-20201028170249809.png) |
| ------------------------------------------------------------ |
| 测试时，scene graph + 从一个learned distribution 采样latent code => generate scene layout <br>训练时，input scene graph + GT layout 先通过encoder提取出其layout latent  (学出一个distribution)，然后用提取出的layout latent + input scene graph 生成predicted layout |



- **refinement (finetune) 过程**

| ![image-20201028170332920](media/image-20201028170332920.png) |
| ------------------------------------------------------------ |
|                                                              |


- **效果**

  - 2.5D vs. 2D

    - ![image-20201028170455621](media/image-20201028170455621.png)
  - diverse layout from the same scene graph

    - ![image-20201028171028235](media/image-20201028171028235.png)
  - diverse layout generation

    - ![image-20201028170542200](media/image-20201028170542200.png)
- **思考**

  - 我们的idea基本就是true-3D multi-view version of the paper
  - 更多的注重用生成模型做表征提取
  - 物体不是来自于一个3D model dataset，而是来自于构建好的三维表征

    - 思考：事实上我们的重点并不在这里，理论上物体也可以来自于3D model dataset，强调的只是从一对关系+自由度中产生不同的pair-wise relationships
  - 它的scene layout把物体的一些特征和关系特征揉在一起，我们是分开的

    - 它的问题就是，因为其实没有把物体解耦出来/没有表征物体。<br>因此假设图给定了，我们只是想移动一下物体，如果用它的框架来做，在移动过程中物体的形状、外观也会改变（因为并没有解耦；）
    - 或者说，因为它是直接从3d model 数据集中retrive出来的model，其实学到的并不是机器人所处的当前场景
    - 思考/启发：像某些论文(如*Towards Unsupervised Learning of Generative Models for 3D Controllable Image Synthesis*)一样，其实我们也可以做一步从一个大的latent code先map出若干个物体的过程

      - -> 这个过程也许可以反过来用于<u>graph embedding learning 图表示学习/图表示浓缩</u>

</details>