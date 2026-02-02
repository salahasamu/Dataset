**BioSR+ Dataset (Detailed File Structure & Parameters)**

**1\. 简介 (Introduction)**

该数据集是 **BioSR / BioSR+** (Nature Biotechnology, 2023) 论文的配套数据。它专为解决活细胞超分辨率成像中的光毒性与光漂白问题而设计，重点提供了**多信噪比等级 (Multi-SNR Levels)** 的成对数据。

数据采用结构光照明 (SIM) 模式采集，覆盖了从极低光照（模拟高速成像）到高光照（高质量参考）的 8 个信号等级，旨在训练“合理化深度学习 (rationalized deep learning)”算法，使其能从低质量原始数据中重建高质量超分辨图像。

**2\. 数据来源与格式 (Source & Format)**

- **原始论文**: Qiao, C., et al. (2023). _Nature Biotechnology_.
- **成像设备**: 结构光照明显微镜 (SIM, Structured Illumination Microscopy)。
- **基础参数**:
    - **文件格式**: **.mrc** (Medical Research Council 格式，常用于电镜和 SIM 原始数据堆栈)。
    - **数据内容**: 包含原始的相移图像堆栈 (Raw Phase Images) 和 重建后的真值图像 (Reconstructed GT)。
    - **文件大小**: 单个文件通常为 **2.4 MB** (提示：这通常意味着特定的张量尺寸，如 512x512 float32 堆栈)。

**3\. 文件夹结构详情 (Folder Structure Details)**

数据集根目录按生物结构分类（如 CCPs）。内部按 **细胞 (Cell)** 为单位组织，每个细胞下分 **等级 (Level)** 存储。

**通用目录结构：**

Plaintext

\[Structure_Name\]/ # 例如: CCPs/

├── Cell_001/ # 第 1 个细胞/视野的数据

│ ├── Level_01/ # \[极低信噪比\] 模拟高速/低光照条件

│ │ ├── RawSIMData.mrc # \[输入\] 原始 SIM 图像堆栈

│ │ └── RawSIMData_gt.mrc # \[目标\] SIM 重建图像 (Ground Truth)

│ ├── Level_02/ # \[低信噪比\]

│ │ ├── RawSIMData.mrc

│ │ └── RawSIMData_gt.mrc

│ ├── ...

│ └── Level_08/ # \[高信噪比\] 高质量参考条件

│ ├── RawSIMData.mrc

│ └── RawSIMData_gt.mrc

├── Cell_002/

│ ├── ...

└── Cell_N/

**4\. 关键文件术语与参数说明 (Key Terminology & Parameters)**

根据 .mrc 格式及 SIM 成像原理，文件规格说明如下：

**4.1 原始输入数据 (Input)**

- **文件名**: RawSIMData.mrc
- **描述**: 原始结构光照明数据堆栈 (Raw SIM Stack)。
- **内容**: 包含不同相位和角度的原始图像（通常为 9 帧：3个角度 × 3个相位）。
- **特点**: 随 Level 不同，图像含有的泊松噪声 (Poisson Noise) 强度不同。Level_01 噪声最大。
- **用途**: 深度学习模型的**输入 (Input)**。模型需利用这组相移图像进行超分辨重建。

**4.2 超分辨/真值数据 (Ground Truth)**

- **文件名**: RawSIMData_gt.mrc
- **描述**: 对应的超分辨率重建图像 (Reconstructed SIM Image)。
- **算法**: 通常由传统的 SIM 重建算法（如 Wiener-SIM 或 Hessian-SIM）基于高质量数据生成的。
- **用途**: 训练时的**标签 (Target)**。
- **注意**: 在某些实验设置中，所有 Level 的输入可能都对应同一个高信噪比的 GT；或者该文件代表该 Level 下的最佳重建结果，具体取决于训练策略（通常推荐使用 Level_08 的重建结果作为低 Level 输入的 GT）。

**5\. 类别概览 (Category Overview)**

根据数据集结构，主要包含以下 5 类亚细胞结构：

1.  **CCPs**: 网格蛋白小窝 (Clathrin-Coated Pits) - 点状结构。
2.  **ER**: 内质网 (Endoplasmic Reticulum) - 复杂网状结构。
3.  **F-actin**: F-肌动蛋白 - 密集纤维结构。
4.  **Microtubules**: 微管 - 线状结构。
5.  **Myosin-IIA**: 肌球蛋白 IIA - 点状或短棒状结构。

**6\. 引用 (Citation)**

在使用此数据集时，请引用以下信息：

Code snippet

@article{Qiao_NatBiotech_2023,

author = {Qiao, Chang and Li, Di and Liu, Yong and others},

title = {Rationalized deep learning super-resolution microscopy for sustained live imaging of rapid subcellular processes},

journal = {Nature Biotechnology},

volume = {41},

pages = {369--380},

year = {2023},

publisher = {Nature Publishing Group},

doi = {10.1038/s41587-022-01471-3}

}