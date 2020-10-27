## object aware representations

 - keyword:
    - **blockGAN被引**
    - **SRN被引中带object**

---

**`<ROOTS> "Learning to Infer 3D Object Models from Images"`**  
**[** `2018` **]** **[[paper]](https://www.ijcai.org)** **[[code]](https://www.github.com)** **[** :mortar_board: `Rutgers University` **]** **[** :office: `company` **]**  
**[**  `Chang Chen, Fei Deng, Sungjin Ahn` **]**  
**[** _`completelatentspace`, `GAN`_ **]**  

main preliminary: GQN

<details>
  <summary>Click to expand</summary>
![image-20201027191207023](media/image-20201027191207023.png)




- **前景背景区分方式**： 通过其`Scene Encoder`；类似yolov3的逻辑；
  
  - 把3D 空间分为 $`N_{max}=N_x \times N_y \times N_z`$ 个cell，每个最多检测1个物体（类似Yolo，扩展到三维）；
  - 检测是否有一个物体其中心落在了cell内；如果有，那么回归出一个连续量 $`\boldsymbol{z}_{ijk}^{where} \in \mathbb{R}^3`$ 来specify坐标
  - 具体做法：把一系列context 观测 $`\mathcal{C}=\{(\boldsymbol{x}_c, \boldsymbol{y}_c)\}`$ encode into a Geometric Volume Feature Map 三维体素特征空间 $`\boldsymbol{r} \in \mathbb{R}^{N_x \times N_y \times N_z \times d}`$ ，逐个cell infer 是否有物体以及中心点坐标
  
    - GVFM需要把一系列partial observation aggregate起来；
    - ① 对$`\mathcal{C}`$ 计算一个order-invariant summary $`\psi`$ ：$`\psi=\sum_{c=1}^{\lvert\mathcal{C} \rvert} \psi_{\mathcal{c}}=\sum_{c=1}^{\lvert\mathcal{C} \rvert} f_\psi(x_c, y_c)`$  
    - ② 对 $`\psi`$ 应用一个3D transposed convolution 来把 scene-level 表征$`\psi`$ split 成单个的$`\boldsymbol{r}_ijk`$ slots
- **主要贡献**
  - 第一个调查GAN模型的"complete representations"
  - 用CR-GAN来学习完整的表达，使用一种两通路的模式(`reconstruction path` + `generation path`)
  - CR-GAN可以利用`unlabeled data`来`self supervision`，使得生成的质量更好
  - 即使对于**unseen**的dataset，对于**wild conditions**，CR-GAN可以产生高质量的**multi view**图片

</details>