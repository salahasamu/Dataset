# **BioTISR Dataset: 3D F-actin (Lifeact) Subset Structure**

## **1\. 简介 (Introduction)**

该数据集是 **BioTISR** (Biological Time-lapse Image Super-Resolution) 库的 **3D F-actin (F-肌动蛋白)** 子集。数据通过 **3D-SIM** (三维结构光照明荧光显微镜) 模式采集，旨在为开发处理 3D 体数据和时序动态的超分辨率 (ISR) 算法提供高质量的生物图像基准。该数据集特别关注在不同信噪比下的时序重建能力。

## **2\. 文件夹结构详情 (Folder Structure Details)**

该数据集被分卷压缩（例如 1-20, 21-35, 36-50），解压后内部以 **Cell (细胞/ROI)** 为单位进行组织。

**目录树结构如下：**

BioTISR_F-actin_3D_XX-XX/ # 数据集分卷根目录 (如 1-20)

├── Cell_001/ # 第 1 个细胞样本 (ROI)

│ ├── RawSIMData_level_01.mrc # \[输入\] 低激发强度原始数据 (Low SNR)

│ ├── RawSIMData_level_02.mrc # \[参考\] 高激发强度原始数据 (High SNR)

│ └── SIM_gt.mrc # \[真值\] 重建后的超分辨率图像 (Ground Truth)

├── Cell_002/

│ ├── RawSIMData_level_01.mrc

│ ├── RawSIMData_level_02.mrc

│ └── SIM_gt.mrc

├── ...

└── Cell_N/ # 每个分卷包含多个 Cell 文件夹

## **3\. 文件术语与参数说明 (File Terminology & Parameters)**

每个 ROI 文件夹包含三份核心文件，对应不同的图像质量和处理阶段。

### **3.1 原始输入数据 (Raw Input)**

- **文件名**: RawSIMData_level_01.mrc / RawSIMData_level_02.mrc
- **文件格式**: **.mrc** (通用体数据/显微镜图像堆栈格式)。
- **内容描述**:
    - **Level_01**: 在低激发光强度下采集，噪声较高，用于模拟低光照条件下的**输入 (Input)**。
    - **Level_02**: 在高激发光强度下采集，信噪比较高，可作为参考或高质量输入。
- **维度参数 (3D-SIM)**:
    - 包含 **3 相位 (Phases)** $\\times$ **5 方向 (Orientations)** 的原始条纹图。
    - 包含 **10 个时间点 (Timepoints)** 的时序数据。
    - 由于是 3D-SIM，数据包含 Z 轴层面的堆栈信息。

### **3.2 超分辨真值数据 (Ground Truth)**

- **文件名**: SIM_gt.mrc
- **描述**: 使用传统 SIM 重建算法生成的超分辨率图像。
- **用途**: 深度学习模型训练时的**标签 (Ground Truth)**。
- **特性**: 空间分辨率高于 Raw 数据，已解算出精细的 F-actin 纤维结构。

## **4\. 关键技术规格 (Technical Specifications)**

- **生物样本**: F-actin (F-肌动蛋白)，使用 Lifeact 标记。
- **成像模式**: 3D-SIM (Three-Dimensional Structured Illumination Microscopy)。
- **数据量**: 包含至少 50 个不同的 ROI（从截图的文件名 36-50 可推断总数至少为 50）。
- **采集策略**: 保持曝光时间恒定，通过改变激发光强度（Excitation Intensity）来获取 Level 01 和 Level 02 数据。

## **5\. 引用 (Citation)**

如果您在研究中使用了此数据集结构，请引用以下论文：

Code snippet

@article{Qiao_BioTISR_2024,

title = {Time-lapse Image Super-resolution Neural Network with Reliable Confidence Evaluation for Optical Microscopy},

author = {Qiao, Chang and Liu, Shuran and Wang, Yuwang and Xu, Wencong and others},

journal = {bioRxiv},

year = {2024},

doi = {10.1101/2024.05.04.592503}


}
