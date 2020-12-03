[toc] 

## 关键词：NeRF引用中 带 encoder

---

**`"GRF: LEARNING A GENERAL RADIANCE FIELD FOR
3D SCENE REPRESENTATION AND RENDERING"`**  
**[** `ICLR2021` **]** **[[paper]](https://arxiv.org/pdf/2010.04595.pdf)** **[[code]](https://github.com/alextrevithick/GRF)** **[** :mortar_board: `Oxford` **]** **[** :office: `company` **]**  
**[**  `Bo Yang`  **]**  
**[** _`encoder-decoder`_ **]**  

<details>
  <summary>Click to expand</summary>

- **Motivation**
  - NeRF + encoder-decoder结构
  - 用一个**<u>single forward pass</u>** infer出novel scene representations
    - encoder输入：2D images + camera poses + intrinsics
    - encoder输出：neural radiance fieilds
- 主要做法

  - 为每一个light ray (pixel) 提取general features
  - 把features重投影到query 3D point p上
  - 然后从p的feature infer出RGB和volume density
  - **关键在于**：对于任意同一个点，从不同的角度看来的feature是始终一样的，因此不同view的这个点渲染出的RGB和volume density也会保持一致![image-20201202175634941](media/image-20201202175634941.png)
- 构成：四个部件，连接起来，端到端的训练

  - 对每一个2D pixel的feature extractor
  - 一个reprojector，从2D feature到3D空间

    - 做了一个简单的假设：<u>一个像素的feature，是对这个ray上的每一个点的描述</u>
    - 所以就是把一个query 3D point重投影到每一个输入view上，来从每一个输入view对应点的2D feature得到这个3D point的feature
    - 如果重投影的点落在图像内，那就选最近邻的像素的feature
    - 如果在图像外，就给一个零向量
  - 一个aggregator，得到一个3D点的general features

    - 这里的挑战性在于：Input images的长度是可变的，并且没有顺序；因此，通过reprojector获取到的2D features也是没有顺序、任意尺寸的
    - 因此把这里定义为一个注意力聚集过程
  - 一个neural renderer，来infer出那个点的外观和几何

</details>

## 关键词：NeRF引用中带encoder-decoder或auto-encoder

## 关键词：DVR引用中 + generative / generic / generalize / category