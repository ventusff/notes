# multi-view GAN(image generation)

- keywords
  - GAN 3d scene multi view
  - GAN multi view geometry
  - multi view image generation from graph

---

**`"CR-GAN: Learning Complete Representations for Multi-view Generation"`**  
**[** `IJCAI 2018` **]** **[[paper]](https://www.ijcai.org/Proceedings/2018/0131.pdf)** **[** :mortar_board: `University X` **]** **[** :office: `company Y` **]**  
**[**  John Doe  **]**  
**[** _`complete latent space`, `GAN`_, _`encoder-decoder`_  **]**  

<details>
  <summary>Click to expand</summary>

- **主要贡献**
  
  - 第一个调查GAN模型的"complete representations"
  - 用CR-GAN来学习完整的表达，使用一种两通路的模式(`reconstruction path` + `generation path`)
  - CR-GAN可以利用`unlabeled data`来`self supervision`，使得生成的质量更好
  - 即使对于**unseen**的dataset，对于**wild conditions**，CR-GAN可以产生高质量的**multi view**图片
  
- **之前的GAN-based方法**：encoder-decoder+discriminator
  
  
  - |                  ![img](media/56666611.png)                  |
    | :----------------------------------------------------------: |
    | 相比于之前的GAN-based方法，多了一条`generation path`，试图补全z space |
    
  - encoder把图片map到一个latent space，然后操作embedding，然后decoder生成新视角
  
  - [CVPR 2017] [[paper]](https://openaccess.thecvf.com/content_cvpr_2017/papers/Tran_Disentangled_Representation_Learning_CVPR_2017_paper.pdf) <DR-GAN> Disentangled Representation Learning GAN for Pose-Invariant Face Recognition
  
  - [2017]  Multi-view image generation from a single-view. 
  
  - **_之前的GAN-based方法的问题_**：
  
  
    - 学到的都是“不完整”的表征，对于"unseen"data\无边界的data的泛化性很差
    - ==**思考**==：encoder网络学到的大概率就是不完整的表征；这也是为什么用auto-decoder而不是encoder-decoder
  
- **proposal**
  - 除了`reconstruction path`外，引入另一条`generation path`来 从随机采样的sample 创建view-specific images
  - 两条path **共享**同样的G参数：在生成通路学到的G 会引导reconstruction path中的E和D的学习，反过来也是一样
  - E is force to be G的逆向过程，使得学到的**representation可以span the entire Z space**  
  - 更重要的是，两通路的学习过程可以很容易地利用**有label、无label**的数据，对于自监督学习而言，从而大大丰富了Z space，对于自然的生成来说。
  
- **discriminators** 
  
  
  - ![img](media/57229841-1603684635887.png)
  - **==问题==** ：原来这些GAN-based方法中的discriminator都是干什么用的？单纯只是增加图像的细节程度？
  - DR-GAN中：discriminator有两个任务：① id 分类。discriminator输出一个分类输出。② pose分类。分类器输出。

</details>