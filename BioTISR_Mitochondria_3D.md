**BioTISR Dataset: 3D Mitochondria Subset Structure**

**1\. 简介 (Introduction)**

该子数据集是 **BioTISR** (Biological Time-lapse Image Super-Resolution) 库的 **3D Mitochondria (线粒体)** 部分。数据通过 **3D-SIM** (三维结构光照明荧光显微镜) 模式采集。该数据集旨在提供高质量的时序生物超分辨率 (SR) 图像，用于研究线粒体在三维空间中的复杂动态（如分裂与融合）。

**2\. 文件夹结构详情 (Folder Structure Details)**

根据截图显示，数据集被分卷压缩为三个部分：1-20, 21-40, 41-60。这意味着该子集包含总计 **60** 个不同的 ROI（细胞样本），比文档中提到的“至少 50 个”更多。

解压后，内部以 **Cell (细胞)** 为单位进行组织：

**目录树结构如下：**

Plaintext

BioTISR_Mitochondria_3D_XX-XX/ # 数据集分卷根目录 (如 1-20)

├── Cell_001/ # 第 1 个细胞样本 (ROI)

│ ├── RawSIMData_level_01.mrc # \[输入\] 低激发强度原始 SIM 数据 (Low SNR)

│ ├── RawSIMData_level_02.mrc # \[参考\] 高激发强度原始 SIM 数据 (High SNR)

│ └── SIM_gt.mrc # \[真值\] 重建后的超分辨率图像 (Ground Truth)

├── Cell_002/

│ ├── RawSIMData_level_01.mrc

│ ├── RawSIMData_level_02.mrc

│ └── SIM_gt.mrc

├── ...

└── Cell_060/ # 总计 60 个 ROI (根据分卷文件名推断)

**3\. 文件术语与参数说明 (File Terminology & Parameters)**

每个 ROI 文件夹包含三份核心文件，对应不同的图像质量和处理阶段。

**3.1 原始输入数据 (Raw Input)**

- **文件名**: RawSIMData_level_01.mrc / RawSIMData_level_02.mrc
- **文件格式**: **.mrc** (体数据/显微镜图像堆栈格式)。
- **内容描述**:
    - **Level_01**: 低激发光强度采集，噪声较高，作为深度学习模型的**低质量输入 (Low SNR Input)**。
    - **Level_02**: 高激发光强度采集，信噪比较高，作为参考或高质量输入。
- **维度参数 (3D-SIM)**:
    - **相位 (Phases)**: 3
    - **方向 (Orientations)**: 5
    - **时间点 (Timepoints)**: 10
    - **Z轴 (Z-slices)**: 包含 Z 轴层面的堆栈信息（3D 体数据）。
    - **结构**: 数据为 $N \\times M \\times T$ 的原始图像组，即每个时间点由 15 张原始条纹图组成。

**3.2 超分辨真值数据 (Ground Truth)**

- **文件名**: SIM_gt.mrc
- **描述**: 使用传统 SIM 重建算法生成的 3D 超分辨率图像。
- **用途**: 深度学习模型训练时的**标签 (Ground Truth)**。
- **特性**: 线粒体是双层膜结构的细胞器，在 3D-SIM 下表现为中空的管状或网状结构，GT 图像应清晰展示这些拓扑细节。

**4\. 关键技术规格 (Technical Specifications)**

- **生物结构**: Mitochondria (线粒体)，通常指 Outer Mitochondrial Membrane。
- **成像模式**: 3D-SIM (Three-Dimensional Structured Illumination Microscopy)。
- **样本数量**: 包含 **60** 个不同的 ROI（文件名显示至 41-60）。
- **采集策略**: 保持曝光时间恒定，通过改变激发光强度（Excitation Intensity）来获取 Level 01 和 Level 02 数据。

**5\. 引用 (Citation)**

如果您在研究中使用了此数据集结构，请引用：

Code snippet

@article{Qiao_BioTISR_2024,

title = {Time-lapse Image Super-resolution Neural Network with Reliable Confidence Evaluation for Optical Microscopy},

author = {Qiao, Chang and Liu, Shuran and Wang, Yuwang and Xu, Wencong and others},

journal = {bioRxiv},

year = {2024},

doi = {10.1101/2024.05.04.592503}

}