**DL-SMLM Dataset (Detailed File Structure & Parameters)**

**1\. 简介 (Introduction)**

该数据集是 **DL-SMLM** (Scientific Data, 2025) 论文的配套数据。它专为单分子定位显微镜 (SMLM) 的深度学习算法设计，提供了从低分辨率宽场图像到高分辨率定位图像的成对数据。

数据涵盖了网格蛋白小窝 (CCPs)、微管 (Microtubules)、内质网 (ER) 和线粒体 (Mitochondria) 等多种生物结构。

**2\. 数据来源与格式 (Source & Format)**

- **原始论文**: Zhao, X., et al. (2025). _Scientific Data_.
- **成像设备**: Hamamatsu ORCA-Fusion BT sCMOS 相机。
- **基础参数**:
    - **像素尺寸 (Pixel Size)**: 原始宽场图像为 **130 nm** (bin=2)。
    - **转换因子 (Conversion Factor)**: 0.23 electrons/count。
    - **暗电流偏移 (Dark Offset)**: 100。

**3\. 文件夹结构详情 (Folder Structure Details)**

数据集根目录包含按生物结构分类的压缩包（如 CCPs.zip, ER-sec61β.zip 等）。解压后，内部按 **细胞 (Cell)** 为单位组织。

**通用目录结构：**

Plaintext

\[Structure_Name\]/ # 例如: CCPs/ 或 Microtubules/

├── cell1/ # 第 1 个细胞的数据

│ ├── WF_raw.tif # \[输入\] 100帧原始宽场图像堆栈 (16-bit)

│ ├── WF1.tif # \[参考\] 宽场叠加图 (32-bit, 文件名数字对应细胞编号)

│ ├── SR1.tif # \[目标\] 超分辨率重建图 (32-bit, 文件名数字对应细胞编号)

│ └── SR_locs.csv # \[真值\] 单分子定位坐标表

├── cell2/

│ ├── WF_raw.tif

│ ├── WF2.tif

│ ├── SR2.tif

│ └── SR_locs.csv

├── ...

└── cellN/

**4\. 关键文件术语与参数说明 (Key Terminology & Parameters)**

根据 data information.txt 文件，各文件的具体技术规格如下：

**4.1 原始输入数据 (Input)**

- **文件名**: WF_raw.tif
- **描述**: 原始宽场荧光图像堆栈 (Widefield Stack)。
- **尺寸 (Size)**: **256 × 256** 像素。
- **序列长度**: **100 Frames** (100 帧)。
- **曝光时间**: 50 ms。
- **数据类型**: **16-bit** 整数。
- **用途**: 深度学习模型的输入张量 (Input Tensor)，维度通常为 (1, 100, 256, 256) 或 (100, 256, 256)。

**4.2 宽场参考图 (Reference)**

- **文件名**: WF{X}.tif (例如 WF1.tif)
- **描述**: 宽场叠加图像 (Sum Image)，由 100 帧 Raw 数据叠加而成。
- **数据类型**: **32-bit** 浮点数 (为了防止叠加溢出)。
- **用途**: 代表衍射受限条件下的图像质量，常用于可视化对比或跨模态（WF → SR）任务的输入。

**4.3 超分辨目标数据 (Ground Truth)**

- **文件名**: SR{X}.tif (例如 SR1.tif)
- **描述**: 超分辨率重建图像 (Super-Resolution Image)。
- **放大倍率 (Amplification)**: **8×** (相对于宽场图像)。
- **尺寸 (Size)**: **2048 × 2048** 像素 (256 × 8)。
- **像素尺寸**: **16.25 nm** (130 nm / 8)。
- **数据类型**: **32-bit**。
- **用途**: 训练时的标签 (Label/Target)。

**4.4 定位坐标数据 (Localization Data)**

- **文件名**: SR_locs.csv
- **描述**: 通过 ThunderSTORM 等软件生成的原始定位数据。
- **用途**: 如果需要生成非 8 倍放大的图像，或使用不同的渲染半径，可以利用此文件重新生成 SR 图像。

**5\. 类别概览 (Category Overview)**

根据您的截图，数据集包含以下 6 个主要子集：

1.  **CCPs**: 网格蛋白小窝 (Clathrin-Coated Pits)
2.  **ER-sec61β**: 内质网膜 (ER membrane)
3.  **ER-KDEL**: 内质网腔 (ER lumen)
4.  **Microtubules**: 微管
5.  **OMM-tomm20**: 线粒体外膜 (Outer Mitochondrial Membrane)
6.  **IMM-cox8a**: 线粒体内膜 (Inner Mitochondrial Membrane)

**6\. 引用 (Citation)**

在使用此数据集时，请引用以下信息：

Code snippet

@article{Zhao_ScientificData_2025,

author = {Zhao, X. and Yang, T. and Pan, T. and Gu, L. and Xu, T. and Ji, W.},

title = {Single molecule localization super-resolution dataset for deep learning with paired low-resolution images},

journal = {Scientific Data},

volume = {12},

year = {2025},

note = {Data parameters derived from data information.txt}

}