**BioTISR Dataset: 3D F-actin (Lifeact) Subset Structure**

**1\. 简介 (Introduction)**

该子数据集是 **BioTISR** 库的一部分，专门针对 **3D F-actin (F-肌动蛋白)** 结构。数据是通过 **3D-SIM** (三维结构光照明荧光显微镜) 模式采集的，旨在支持时序图像超分辨率 (Time-lapse ISR) 算法的开发，特别是处理 3D 体积数据。

**2\. 文件夹结构详情 (Folder Structure Details)**

数据集根目录为 BioTISR_Lifeact_3D，内部按 **细胞 (Cell)** 为单位进行组织。每个细胞文件夹包含不同信噪比（激发强度）的原始数据和对应的超分辨真值。

**目录树示例如下：**

Plaintext

BioTISR_Lifeact_3D/ # 数据集根目录 (F-actin 3D数据)

├── Cell_001/ # 第 1 个细胞样本

│ ├── RawSIMData_level_01.mrc # \[输入\] 低激发强度原始 SIM 数据 (Low SNR)

│ ├── RawSIMData_level_02.mrc # \[参考\] 高激发强度原始 SIM 数据 (High SNR)

│ └── SIM_gt.mrc # \[真值\] 重建后的超分辨率图像 (Ground Truth)

├── Cell_002/

│ ├── RawSIMData_level_01.mrc

│ ├── RawSIMData_level_02.mrc

│ └── SIM_gt.mrc

├── Cell_003/

│ ├── ...

├── ...

└── Cell_N/

**3\. 文件术语与参数说明 (File Terminology & Parameters)**

根据 BioTISR 的采集策略，每个 ROI（即每个 Cell 文件夹）包含不同激发光强度的数据。

**3.1 原始输入数据 (Raw Input)**

- **文件名**: RawSIMData_level_01.mrc / RawSIMData_level_02.mrc
- **文件格式**: **.mrc** (一种常用于电镜和 3D 显微镜的体数据格式)。
- **内容描述**:
    - **Level_01**: 低激发光强度采集的原始图像。通常噪声较高，作为深度学习模型的**低质量输入 (Input)**。
    - **Level_02**: 高激发光强度采集的原始图像。信噪比更高，可作为参考或高质量输入。
- **维度参数 (3D-SIM)**:
    - 数据包含 **3 相位 (Phases)** × **5 方向 (Orientations)**。
    - 包含了 **10 个时间点 (Timepoints)** 的时序数据。
    - 由于是 3D 数据，每个文件内部应当包含 Z 轴层面的堆栈信息。

**3.2 超分辨真值数据 (Ground Truth)**

- **文件名**: SIM_gt.mrc
- **描述**: 经过算法（通常是传统的 SIM 重建算法）重建后的超分辨率图像。
- **用途**: 训练时的 **标签 (Target/Ground Truth)**。
- **特性**: 相比 Raw 数据，该图像的空间分辨率更高，且已经从多相位/多方向的原始条纹数据中解算出了生物结构。

**4\. 关键技术规格 (Technical Specifications)**

- **生物结构**: F-actin (通过 Lifeact 标记)。
- **成像模式**: 3D-SIM (Three-Dimensional Structured Illumination Microscopy)。
- **采集策略**: 保持曝光时间恒定，通过改变激发光强度获得 level_01 和 level_02。

**5\. 引用 (Citation)**

在使用此数据结构时，请引用：

Code snippet

@article{Qiao_BioTISR_2024,

title = {Time-lapse Image Super-resolution Neural Network with Reliable Confidence Evaluation for Optical Microscopy},

author = {Qiao, Chang and Liu, Shuran and Wang, Yuwang and Xu, Wencong and others},

journal = {bioRxiv},

year = {2024},

doi = {10.1101/2024.05.04.592503}

}