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
  - 应用展示：scene graph based layout synthesis + exemplar based image synthesis
- **数据集/数据特征/数据定义**

  - 物体3D model 是直接从SUNCG数据集中 retrive的；选择类别内最相似的bbox
  - scene graph定义：==与我们类似==

    - scene graph `y`由一组triplets构成，$`(o_i, p, o_j)`$
    - $`o_i`$代表第i-th物体的type(索引embedding) + attributes(索引embedding), $`p`$代表空间关系(索引embedding)
  - 本文中layout的数据结构/物理含义：

    - each element $`y_i`$ in layout $`y`$ 定义是一个 7-tuple，代表物体的bbox和竖直轴旋转：$$`y_i=(min_{X_i}, min_{Y_i}, min_{Z_i}, max_{X_i}, max_{Y_i}, max_{Z_i}, \omega_i )`$$
  - 本文中latent space的定义：

    - [box_emdding, angle_ambedding] (因为是VAE，所以还分了mean, var)
- **主要组件**

  - conditional (on scene graph) layout synthesizer

    - 产生的而是3D scene layout；<br>每个物体都有3D bbox + 竖直轴旋转
    - 把传统2D scene graph数据增强为3D scene graph，把每个物体关系编码到三维空间
  - 集成了一个differentiable renderer来只用scene的2D投影来refine 最终的layout

    - 给定一张semantics map和depth map，可微分渲染器来**optimize over** the synthesized layout去**拟合**给定的输入，通过**<u>analysis-by-synthesis</u>** fashion
- **layout generator的网络架构**

| ![image-20201028170249809](media/image-20201028170249809.png) |
| ------------------------------------------------------------ |
| <u>**测试**</u>时，scene graph + 从一个learned distribution 采样latent code => generate scene layout <br><u>**训练**</u>时，input scene graph + GT layout 先通过encoder提取出其layout latent  (学出一个distribution)，然后用提取出的layout latent + input scene graph 生成predicted layout |


- **encoder**

```mermaid
graph LR
	subgraph scene_graph[input scene graph]
	relationships["relationships (索引)"]
	obj_type["object type (索引)"]
	obj_attr["object attribute (索引)"]
	end
	subgraph encoder
	obj_vecs
	angle_vecs
	pred_vecs
	boxes_vecs
	new_obj_vecs[object vector after GCN]
	GCN((GCN))
	obj_vecs --> obj_vecs2
	boxes_vecs --> obj_vecs2
	angle_vecs --> obj_vecs2
	obj_vecs2 --> GCN
	pred_vecs --> GCN
	GCN --> new_obj_vecs
	new_obj_vecs -.box_mean_var.-> bbox_latent
	new_obj_vecs -.angle_mean_var.-> angle_latent
	end
	subgraph ground truth layout
	bbox_gt["min_x<br>min_y<br>min_z<br>max_x<br>max_y<br>max_z"]
	angles_gt["angle"]
	end
	obj_type -.torch.Embedding.-> obj_vecs
	obj_attr -.torch.Embedding.-> obj_vecs
	relationships -.torch.Embedding.-> pred_vecs
	angles_gt -.torch.Embedding.-> angle_vecs
	bbox_gt -.nn.Linear.-> boxes_vecs
	z["z [mean, var]"]
	bbox_latent --> z
	angle_latent --> z
```

 - **decoder**（注意：也可以先GCN然后再拼接z到GCN之后的object vectors）

```mermaid
graph LR
	subgraph scene_graph[input scene graph]
	obj_type["object type (索引)"]
	obj_attr["object attribute (索引)"]
	relationships["relationships (索引)"]
	end
	subgraph layout_latent[layout latent code]
	bbox_emb["bbox embedding 48维隐向量"]
	angle_emb["rotation embedding 16维隐向量"]
    z["z [mean, var]"]
    bbox_emb --> z
    angle_emb --> z
	end
	subgraph decoder
	edge_emb[edge vector]
	GCN(("GCN"))
	obj_vecs[object vector]
	new_obj_vecs[object vector after GCN]
	edge_emb --> GCN
	obj_vecs --> GCN
	GCN --> new_obj_vecs
	end
    z --> obj_vecs
    obj_type -.torch.Embedding.-> obj_vecs
    obj_attr -.torch.Embedding.-> obj_vecs
    relationships -.torch.Embedding.-> edge_emb
    layout["layout <br>[min_x<br>min_y<br>min_z<br>max_x<br>max_y<br>max_z<br>angle]"]
	new_obj_vecs -.box_net.-> layout
	new_obj_vecs -.angle_net.-> layout
```


- **对encoder/decoder结构的思考**
  - 它为***物体的位置、角度赋予随机变量***，然后在graph condition下回归出每个物体的layout
- 但是事实上，应该是先有了约束，再在约束下***为边关系赋予随机变量***（隐关节自由度）
  
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

    - 我们的idea就是在已经知道scene graph的情况下，加入layout latent code.

      - 后面着重考虑scene graph的提取，以及考虑在不同视角下得到的不同2D scene graph描述怎么转化为3D（A->to the left of B）
  - 更多的注重用生成模型做表征提取
  - 物体不是来自于一个3D model dataset，而是来自于构建好的三维表征

    - 思考：事实上我们的重点并不在这里，理论上物体也可以来自于3D model dataset，强调的只是从一对关系+自由度中产生不同的pair-wise relationships
  - ~~它的scene layout把物体的一些特征和关系特征揉在一起，我们是分开的~~<br>它的scene graph定义和我们非常相似
- 或者说，因为它是直接从3d model 数据集中retrive出来的model，其实学到的并不是机器人所处的当前场景
    - ==思考==：像某些论文(如*Towards Unsupervised Learning of Generative Models for 3D Controllable Image Synthesis*)一样，其实我们可以做一步从一个大的latent code先map出若干个物体的过程
    
  - -> 这个过程也许可以反过来用于<u>graph embedding learning 图表示学习/图表示浓缩</u>

</details>