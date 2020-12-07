
---

**`"Learning to Infer Implicit Surfaces without 3D Supervision"`**  
**[** `NeuIPS2019` **]** **[[paper]](https://papers.nips.cc/paper/2019/file/bdf3fd65c81469f9b74cedd497f2f9ce-Paper.pdf)**  **[** :mortar_board: `University of Southern California` **]**   
**[**  `Shichen Liu`, ` Shunsuke Saito`, `Weikai Chen`, `Hao Li`  **]**  
**[** _`abcd`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Motivation**
  - implicit occupancy field![image-20201207195643392](media/image-20201207195643392.png)

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
    输入code + one point 坐标，输出在shape 内；外；（类似SDF）
  - ![image-20201203174748033](media/image-20201203174748033.png)

</details>



---

**`"Occupancy Networks: Learning 3D Reconstruction in Function Space"`**  
**[** `CVPR2019` **]** **[[paper]](https://openaccess.thecvf.com/content_CVPR_2019/papers/Mescheder_Occupancy_Networks_Learning_3D_Reconstruction_in_Function_Space_CVPR_2019_paper.pdf)** **[[code]](https://github.com/autonomousvision/occupancy_networks)** **[** :mortar_board: `MPI,University of Tubingen ` **]** **[** :office: `Google AI Berlin` **]**  
**[**  `Lars Mescheder，Andreas Geiger `  **]**  
**[** _`continuous function occupancy, multi-resolution isosurface extraction`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Motivation**
  - 用一个隐式函数来表达占用概率，从而可以实现任意分辨率的表达![image-20201203153023230](media/image-20201203153023230.png)
- **主要框架**

  - **多分辨率等值面提取技术** [Multiresolution IsoSurface Extraction (MISE)]![image-20201203153114826](media/image-20201203153114826.png)

</details>