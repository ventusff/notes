[toc]

## math: implicit surface

###  [[wiki]](https://en.wikipedia.org/wiki/Implicit_surface)

###  很有启发性的 [CG course note](https://people.cs.clemson.edu/~dhouse/courses/405/notes/implicit-parametric.pdf): surface: implicit form & parametric form  

- 一个球面形状的隐式形式和参数化形式：`implicit form` & `parametric form`![image-20201207201258315](media/image-20201207201258315.png)
- implicit的形式无法直接通过其生成点，但是一般可以通过test来判断点在object内还是object外，对于ray-tracing非常友好
  - ![image-20201207204020330](media/image-20201207204020330.png)
- parametric的形式可以直接通过其生成surface上的点，对于OpenGL等方法很有帮助
  - ![image-20201207204043660](media/image-20201207204043660.png)

### 形状(geometry) 与 拓扑(topology)

- 如果用mesh的数据结构来理解：
  - 拓扑相同的几个形状，顶点之间的连接关系相同(不变)，互相之间可以直接通过顶点位移来变换得到；
    - 如甜甜圈和咖啡杯
  - 拓扑不同的形状，只要顶点之间的连接关系保持不变，怎么位移顶点都无法得到
  - 当然，上述的“位移顶点位置”是一个粗糙的描述，具体在形变时是要符合一定规则的，即【<u>光滑同胚/微分同胚</u>】 [bilibili视频：[斯梅尔悖论；球内外翻转](https://www.bilibili.com/video/BV1k54y1R7J5) ]

### 流形`manifold`，卡(坐标卡)`chart`，图册`atlas`

[知乎](https://zhuanlan.zhihu.com/p/41563330)

[wiki](https://en.wikipedia.org/wiki/Atlas_(topology)#Charts)

- 同胚：`homeomorphism`
  - 同胚是两个拓扑空间`topological space`之间的函数。
  - a function $`f: X \rightarrow Y`$ between two topological spaces is a homeomorphism if:
    - $`f`$ is a `bijection`   (i.e. `one-to-one` and `onto`)
      $`f`$是一个双射，i.e.单射且满射
    - $`f`$ is a continuous function
    - the inverse function $`f^{-1}`$ is continuous
  - e.g. 咖啡杯和甜甜圈这两个拓扑空间同胚
- 流形`manifold`， 坐标卡`chart`，参数化`parameterization`，
  - `2-manifold`(`two-dimensional manifold`)二维流形的定义：
    - a subset $`\mathcal{S}`$ of $`\mathbb{R}^3`$ is a 2-manifold if
      - for every point $`\boldsymbol{p} \in \mathcal{S}`$
        <br>there is an open set $`V`$ in $`\mathbb{R}^2`$ and an open set $`W`$ in $`\mathbb{R}^3`$ containing $`\boldsymbol{p}`$ <br> such that $`U=\mathcal{S} \cap W`$ is homeomorphic to $`V`$
        <br>对于 $`\mathcal{S}`$中的任意一个点 $`\boldsymbol{p}`$ ，
        <br>都存在【$`\mathbb{R}^2`$ 中的一个开集$`V`$】(低维欧式空间中的一个开集) 和【$`\mathbb{R}^3`$中的包含点 $`\boldsymbol{p}`$ 一个开集$`W`$ 】<br>
        使得【$`\mathcal{S}`$和$`W`$ 的交集$`U`$】($`S`$的一个包含点$`p`$的开子集)与$`V`$同胚
      - 这个同胚记为$`\varphi: U \rightarrow V`$，有序对 $`(U,\varphi)`$ 叫做包含$`p`$的坐标卡
      - 人话：<br>
        $`S`$的一个开子集和低维欧式空间的一个开子集同胚，那么$`S`$就是一个流形；<br>
        从$`S`$的一个开子集到低维欧式空间的开子集的同胚叫做`chart`坐标卡
        <br>坐标卡的逆(从低维欧式空间的开子集 到 $`S`$的一个开子集的同胚)叫做`paramterization`参数化
  - `manifold`理解：局部区域线性，与低维欧式空间拓扑同胚
  - “自由度”的理解：<br>一个m维空间的中的曲线/曲面有n个自由度，其实严格数学定义指的是这个曲面/曲线是一个n维流形，与某一个n维欧式空间(局部)同胚
- `chart`
  - A `chart` for a `topological space` *M* is a `homeomorphism` $`\varphi`$ from an open subset *U* of *M* to an open subset of a Euclidean space.
    <br>一个拓扑空间的坐标卡，就是这个拓扑空间的一个开子集到一个欧式空间的开子集的同胚
  - the chart is traditionally recorded as the ordered pair $`(U,\varphi)`$ <br>坐标卡一般用有序对$`(U,\varphi)`$表示
- `image`像：
  - 设$`f`$是一个从定义域$`X`$到值域$`Y`$的一个函数
  - image of an element
    If *x* is a member of *X*, then the image of *x* under *f*, denoted *f*(*x*), is the value of *f* when applied to *x.*
  - image of a subset
    the image of subset $`A \subseteq X`$ under *f*, denoted $`f[A]`$ is the subset of *Y* which can be defined as:
    <br>$`f[A] = \{f(x) \vert x \in A\}`$
    <br>when there is no risk of confusion, $`f[A]`$ is simply written as $`f(A)`$
  - `inverse image / preimage`原像：
    <br>the preimage or inverse image of set $`B \subseteq Y`$ under *f* , denoted by $`f^{-1}[B]`$, is the subset of *X* defined by<br>
    $`f^{-1}[B]=\{x\in X \vert f(x) \in B\}`$
- 图册`atlas`
  - 图册是一族坐标卡
  - a index family $`\{(U_\alpha,\varphi_{\alpha}):\alpha \in I \}`$ of charts on *M* which `covers` *M* (that is, $`\cup_{\alpha \in I} U_{\alpha}=M`$)
  - 流形*M*上的一个图册是：
    一族*M*上的卡$`\mathcal{A}=\{(U_{\alpha}, \varphi_{\alpha})\}`$ ，使得定义域盖住了整个*M* 

### losses

- chamfer loss
  - chamfer distance
  - ![image-20201208012017960](media/image-20201208012017960.png)
  - ![image-20201208012035153](media/image-20201208012035153.png)

## implicit form / implicit field 与 parametric form 之间的转换



## learning parametric surface

- keyword
  - neural parametric surface
  - parametric surface generation/generative

---

**`"Learning Category-Specific Mesh Reconstruction from Image Collections"`**  
**[** `ECCV2018` **]** **[[paper]](https://arxiv.org/pdf/1803.07549.pdf)** **[[web]](https://akanazawa.github.io/cmr/)** **[[code]](https://github.com/akanazawa/cmr)** **[** :mortar_board: `UCB` **]**   
**[**  `Angjoo Kanazawa`, `Shubham Tulsiani`, `Alexei A. Efros`, `Jitendra Malik`  **]**  
**[** _`category-specific canonical shape template`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Motivation**
  ![image-20201207225935008](media/image-20201207225935008.png)
- **Overview**
  ![image-20201207230015167](media/image-20201207230015167.png)
  - 一张图片encode到一个latent space, 被三个模块共享
  - shape predictor，学到的是从mean shape出发的顶点的位移改变量
  - texture predictor，学到的是从输入图像的texture flow
  - camera predictor，学到的是canonical space下的camera pose

- deformation predictor事实上学到的是从一个learned mean shape的变形
  texture使用标准UV映射定义

- mesh定义在canonical frame下
    mean shape和sphere有相同的geometry
  - 相同的顶点连接性，相当于fixed topology，拓扑是固定的
    - 思考甜甜圈和咖啡杯的拓扑是一样的：通过顶点移位变形可以变形过去
    - a fixed and pre-determined mesh connectivity 连接性是固定的
  - 所谓shape predictor，其实是预测固定个数的vertices的位置改变<br>
    ![image-20201207231029039](media/image-20201207231029039.png)
  - 我们可以从uv图的坐标映射到球面坐标，再映射到mean shape上的坐标，再通过shape 变形（顶点移位）映射到当前shape上的顶点坐标

- texture predictor 事实上学到的是从单张图片出发的texture flow
  ![image-20201207232213580](media/image-20201207232213580.png)

</details>

---

**`"Learning Shape Templates with Structured Implicit Functions"`**  
**[** `ICCV2019` **]** **[[paper]](https://arxiv.org/pdf/1904.06447.pdf)**  **[** :mortar_board: `Princeton` **]** **[** :office: `Google` **]**  
**[**  `Kyle Genova`, `Forrester Cole`, ` Daniel Vlasic`, `Aaron Sarna`,  `William T. Freeman`, `Thomas Funkhouser` **]**  
**[** _`general canonical shape template`_ **]**  

learning generalized templates comprised of elements

<details>
  <summary>Click to expand</summary>

- **Motivation**
  
  - 给这类从canonical space下的shape template学出物体shape的方法，提供一种更通用于各种类别的shape template 学习方法
  - 由于现实世界的形状和拓扑变化丰富，过去的_<u>这类</u>_方法一般用a library of handmade templates
  - 本篇使用了一种基于若干个local shape elements的组合来构成shape template；<br>
    每个element是一个隐式的surface representation
    - 每个element可以当做一个高斯椭球形状
    - 这样，不同的elements位置、扁圆、大小组合，就可以组合出==<u>不同形状、不同拓扑</u>==的shape template
  - 使用10，25，100个不同的elements训练的效果<br>![image-20201207235340273](media/image-20201207235340273.png)
- 隐式的shape表征：
  - 假定每一个input shape都可以建模为一个watertight surface，由一个函数的 $`\mathcal{l}`$ level set描述（l-等值面集）；
  - 这个函数可以由N个local elements构成
  - 每个elements是一个 _scaled axis-aligned anisotropic 3D Gaussians_ 
    <br>由参数$`\theta_i`$描述，$`\theta_i`$包含$`c_i, p_i \in \mathbb{R}^3, r_i \in \mathbb{R}^3`$
    <br>![image-20201208000148898](media/image-20201208000148898.png)

</details>

---

**`"AtlasNet: A Papier-Mâché Approach to Learning 3D Surface Generation"`**  
**[** `CVPR2018` **]** **[[paper]](https://arxiv.org/pdf/1802.05384.pdf)** **[[web]](http://imagine.enpc.fr/~groueixt/atlasnet/)** **[[code]](https://github.com/ThibaultGROUEIX/AtlasNet)** **[[code-easy-to-understand]](https://github.com/ThibaultGROUEIX/AtlasNet/tree/V2.2)** **[** :mortar_board: `University` **]** **[** :office: `Adobe` **]**  
**[**  `Thibault Groueix`  **]**  
**[** _`continous 2D patches`, `learning 2-manifold parameterization`, `2-manifold generation`_ **]**  

<details>
  <summary>Click to expand</summary>

- ![image-20201208004500075](media/image-20201208004500075.png)
- **Motivation**
  - represents a surface as a collection of parametric surface elements
    <br>把一个表面表征为一组parametric surface元素的集合
- **overview**
  
  - ![image-20201208004950236](media/image-20201208004950236.png)
  - pointcloud基线，是把一个latent shape code输出为一组点
  - 本篇方法，额外输入一个从均匀单位方内采样的2D坐标点，用其来产生surface上的一个single point
    - 从点云/数据中学出这种`2-manifold`（i.e. [two-dimensional manifolds](https://www2.cs.duke.edu/courses/fall06/cps296.1/Lectures/sec-II-1.pdf)，二维流形）的parameterization
    - 属于parametric approaches 分支
    - ==**<u>这里本质上就是一个从二维均匀分布到空间二维流形分布的映射，condition on一个shape code</u>**==
  - 很容易扩展多次，来把一个3D shape表征为几个surface 元素的联合
- 局部参数化表面的生成 locally parameterized surface generation
  - 把surface看做一个广义的2-manifold（允许self-intersection & disjoint sets），考虑局部的参数化<br>
    consider a `2-manifold` $`\mathcal{S}`$, a point $`\boldsymbol{p} \in \mathcal{S}`$, a `parameterization` $`\varphi`$ of $`\mathcal{S}`$ in a local neighborhood of $`\boldsymbol{p}`$
  - 假定这个局部参数化就是从单位方 $`]0,1[^2`$ 到2-manifold $`\mathcal{S}_{\theta}`$的映射 $`\varphi_{\theta}(x)`$ : $`\mathcal{S}_\theta=\varphi_{\theta}(]0,1[^2)`$
     <br>让$`\mathcal{S}_{\theta}`$去估计/近似局部2-manifold $`S_{loc}`$
  - i.e.寻找 参数$`\theta`$来最小化目标函数$`\min \limits_{\theta} \mathcal{L}(\mathcal{S}_\theta, \mathcal{S}_{loc})+\lambda\mathcal{R}(\theta)`$
    <br>上式的$`\mathcal{L}`$是两个2-manifold之间的loss，$`\mathcal{R}`$是参数$`\theta`$的正则化项；
    <br>实践中，计算的不是两个2-manifold之间的loss，<u>而是这两个2-manifold采样出的点集的chamfer 和 earth-mover距离</u>
  - 证明了MLP+ReLU就可以产生2-manifolds
  - 证明了MLP+ReLU产生的2-manifolds can be learned to 很好地近似 target 2-manifolds
    <br>用了universal representation theorum：<br>
    Approximation capabilities of multilayer feedforward networks. *Neural Networks*, 1991

</details>

---

**`"Pix2Surf: Learning Parametric 3D Surface Models of Objects from Images"`**  
**[** `ECCV2020` **]** **[[paper]](https://arxiv.org/pdf/2008.07760.pdf)** **[[supp]](https://geometry.stanford.edu/projects/pix2surf/pub/pix2surf_supp.pdf)** **[[web]](https://geometry.stanford.edu/projects/pix2surf/)** **[[code(trained)]](https://github.com/JiahuiLei/Pix2Surf)** **[** :mortar_board: `Zhejiang University`, `Stanford`, `UCL` **]** **[** :office: `Adobe` **]**  
**[**  `Jiahui Lei`, `Srinath Sridhar`, `Niloy Mitra`, `Leonidas J. Guibas`  **]**  
**[** _`parametric 3D shape/parameterization`, `3D reconstruction`, `multi-view`, `single-view`, `surface reconstruction in NOCS`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Result**
  - 评价：可以看到学出来的曲面可以不是闭合的
  - ![image-20201207204146033](media/image-20201207204146033.png)
    ![image-20201207204206853](media/image-20201207204206853.png)
- **Motivation**
  - learning to generate 3D parametric surface representations for novel object instances, as seen from one or more views
  - 使用2D patch来作为UV parameterization，处理多个non-adjacent views，并且建立2D pixels和3D surface points之间的correspondence
  - 用implicit functions表达的surface，想要得到显式的表面，需要昂贵的后处理步骤：如Marching Cubes

- **主要贡献**
  - high-quality parametric surfaces 遵循multi view一致性
  - 生成的3D表面保留了精确的图像像素到3D表面点的correspondance，使得可以lift texture information去reconstruct 带有丰富集合与外观的 shapes

- **引用的directly reconstruct a parametric representation of a shape's surface**
  - class-specific templates  **<u>(canonical template / mean shape in canonical space)</u>**
    <br>逐个类别手动设计的shape template
    - [ECCV2018] Learning category-specific mesh reconstruction from image collections. 
    - [ICCV2019] Canonical surface mapping via geometric cycle consistency
  - general structured templates
    <br>适用于各种类别的通用shape template学习方法（应对不同的形状、拓扑）
    - [ICCV2019] Learning shape templates with structured implicit functions.
  - more generic surface representations
    - meshes deform
      - [ECCV2018] Pixel2mesh: Generating 3d mesh models from single rgb images.
      - [ICCV2019] Pixel2mesh++: Multi-view 3d mesh generation via deformation
      - [CVPR2019] 3DN: 3d deformation network.
      
    - differentiable mesh renderer + image supervision
      - [CVPR2018] Neural 3d mesh renderer
      - [2019]  Soft rasterizer: A differentiable renderer for image-based 3d reasoning
      - [2019] Pix2vex: Image-togeometry reconstruction using a smooth differentiable renderer.
      - [CVPR2019] Learning view priors for single-view 3d reconstruction.
    - ==continuous 2D patches== 本篇类似：使用2D patch来作为UV parameterization
      - [CVPR2018] Atlasnet: A papiermch approach to learning 3d surface generation. 

</details>

## learning implicit surface: implicit fields/implicit functions
### marching cubes [[explain]](http://www.cs.carleton.edu/cs_comps/0405/shape/marching_cubes.html)

---

**`"MeshSDF: Differentiable Iso-Surface Extraction"`**  
**[** `NeurIPS2020` **]** **[[paper]](https://arxiv.org/pdf/2006.03997.pdf)** **[[code]](https://github.com/cvlab-epfl/MeshSDF)** **[** :mortar_board: `EPFL` **]** **[** :office: `Neuralconcept`, `Intel` **]**  
**[**  `Edoardo Remelli`, `Pascal Fua `   **]**  
**[** _`differentiable iso-surface extraction`, `marching cubes`, `SDF`_  **]**  

[differentiable iso-surface extraction]

<details>
  <summary>Click to expand</summary>

- **Motivation**

</details>


---

**`"Learning Implicit Fields for Generative Shape Modeling"`**  
**[** `CVPR2019` **]** **[[paper]](https://openaccess.thecvf.com/content_CVPR_2019/papers/Chen_Learning_Implicit_Fields_for_Generative_Shape_Modeling_CVPR_2019_paper.pdf)** **[[code]](https://github.com/czq142857/implicit-decoder)** **[[code-improve]](https://github.com/czq142857/IM-NET)**  **[[code-pytorch]](https://github.com/czq142857/IM-NET-pytorch)** **[** :mortar_board: `SFU` **]**   
**[**  `Zhiqin Chen`, `Hao Zhang `  **]**  
**[** _`implicit shape representation`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Motivation**
  - 其实是一种类别级别的连续函数隐式的shape表征，类似occupancy networks；
    <br>输入code + one point 坐标，输出在shape 内；外；（类似SDF）
  - ![image-20201203174748033](media/image-20201203174748033.png)

</details>

---

**`"Occupancy Networks: Learning 3D Reconstruction in Function Space"`**  
**[** `CVPR2019` **]** **[[paper]](https://openaccess.thecvf.com/content_CVPR_2019/papers/Mescheder_Occupancy_Networks_Learning_3D_Reconstruction_in_Function_Space_CVPR_2019_paper.pdf)** **[[code]](https://github.com/autonomousvision/occupancy_networks)** **[** :mortar_board: `MPI,University of Tubingen ` **]** **[** :office: `Google AI Berlin` **]**  
**[**  `Lars Mescheder，Andreas Geiger `  **]**  
**[** _`continuous function occupancy, multi-resolution isosurface extraction`, `marching cubes`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Motivation**
  - 用一个隐式函数来表达占用概率，从而可以实现任意分辨率的表达<br>![image-20201203153023230](media/image-20201203153023230.png)
- **主要框架**
  - **多分辨率等值面提取技术** [Multiresolution IsoSurface Extraction (MISE)]<br>![image-20201203153114826](media/image-20201203153114826.png)

</details>

### ray-casting

- SRN也算此行列；可以微分的ray marching

---

**`"Learning to Infer Implicit Surfaces without 3D Supervision"`**  
**[** `NeuIPS2019` **]** **[[paper]](https://papers.nips.cc/paper/2019/file/bdf3fd65c81469f9b74cedd497f2f9ce-Paper.pdf)**  **[** :mortar_board: `University of Southern California` **]**   
**[**  `Shichen Liu`, ` Shunsuke Saito`, `Weikai Chen`, `Hao Li`  **]**  
**[** _`ray casting`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Motivation**
  - ![image-20201207222950762](media/image-20201207222950762.png)
  - implicit occupancy field![image-20201207195643392](media/image-20201207195643392.png)

</details>

---

**`<DVR> "Differentiable Volumetric Rendering: Learning Implicit 3D Representations without 3D Supervision"`**  
**[** `CVPR2020` **]** **[[paper]](https://arxiv.org/pdf/1912.07372.pdf)** **[[code]](https://github.com/autonomousvision/differentiable_volumetric_rendering)** **[** :mortar_board: `MPI`, `University of Tubingen` **]**   
**[** `Michael Niemeyer`, `Andreas Geiger ` **]**  
**[**  _`differentiable volumetric rendering`, `ray casting`_ **]**  

<details>
  <summary>Click to expand</summary>
- **Motivation**
  - 

</details>