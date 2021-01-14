---
note_type: paper_reading
title: works in <strong>canonical spaces</strong>
title_cn: 标准正视图空间的有关研究
---

* TOC
{:toc}

---

## NOCS(Normalized Object Coordinate Space) 系列

 - **[[NOCS]](https://geometry.stanford.edu/projects/NOCS_CVPR2019/)** NOCS for Pose Estimation [CVPR2019]
 - **[[X-NOCS]](https://geometry.stanford.edu/projects/xnocs/)** Two-intersection NOCS for shape reconstruction [NeurIPS2019]
 - **[[ANCSH]](https://articulated-pose.github.io/)** Articulated Pose Estimation [CVPR2020]
 - **[[S-NOCS]](https://geometry.stanford.edu/projects/pix2surf/)** Shape reconstruction in NOCS with Surfaces (This work) [ECCV2020]
 - **[[T-NOCS]](https://geometry.stanford.edu/projects/caspr/)** NOCS along Time Axis [arXiv2020 Pre-print]

---

**`<NOCS> "Normalized Object Coordinate Space for Category-Level 6D Object Pose and Size Estimation"`**  
**[** `CVPR2019` **]** **[[paper]](https://geometry.stanford.edu/projects/NOCS_CVPR2019/pub/NOCS_CVPR2019.pdf)** **[[supp]](https://geometry.stanford.edu/projects/NOCS_CVPR2019/pub/NOCS_CVPR2019_Supp.pdf)** **[[code]](https://github.com/hughw19/NOCS_CVPR2019)** **[[web]](https://geometry.stanford.edu/projects/NOCS_CVPR2019/)** **[** :mortar_board: `Stanford`, `Princeton University`  **]** **[** :office: `Facebook`, `Google` **]**  
**[**  `He Wang`, `Srinath Sridhar`, `Jingwei Huang`, `Julien Valentin`, `Shuran Song`, `Leonidas J. Guibas`  **]**  
**[** _`abcd`_ **]**  

<details markdown="1">
  <summary markdown="0">Click to expand</summary>

- **Motivation**

</details>

---

**`<X-NOCS>"Multiview Aggregation for Learning Category-Specific Shape Reconstruction"`**  
**[** `NeurIPS2019` **]** **[[paper]](https://geometry.stanford.edu/projects/xnocs/pub/xnocs.pdf)** **[[code]](https://github.com/drsrinathsridhar/xnocs/blob/master/README.md#2-download-the-datasets-see-below-for-details)** **[[web]](https://geometry.stanford.edu/projects/xnocs/)** **[** :mortar_board: `Stanford` **]** **[** :office: `Google`, `Facebook` **]**  
**[**  `Srinath Sridhar`, `Davis Rempe`, `Julien Valentin`, `Sofien Bouaziz`, `Leonidas J. Guibas`  **]**  
**[** _`abcd`_ **]**  

<details markdown="1">
  <summary markdown="0">Click to expand</summary>

- **Motivation**

</details>

---

**`<ANCSH> "Category-Level Articulated Object Pose Estimation"`**  
**[** `CVPR2020` **]** **[[paper]](https://articulated-pose.github.io/paper.pdf)** **[[code]](https://github.com/dragonlong/articulated-pose)** **[[web]](https://articulated-pose.github.io/)** **[** :mortar_board: `Virginia Tech`, `Stanford`, `Columbia University` **]** **[** :office: `Google` **]**  
**[**  `Xiaolong Li`, `He Wang`, `Li Yi`, `Leonidas Guibas`, `A. Lynn Abbott`, `Shuran Song`  **]**  
**[** _`abcd`_ **]**  

<details markdown="1">
  <summary markdown="0">Click to expand</summary>

- **Motivation**

</details>

## learning a canonical representation from non-canonical data

- GIRAFFE
- spectralGAN
- Deep Implicit Templates for 3D Shape Representation
  - 文中的regularizations loss中的point-wise regularizations，通过惩罚变形场前后的整体的位置变化，保证尽量学到一种所有shape统一、和canonical pose对齐的表征