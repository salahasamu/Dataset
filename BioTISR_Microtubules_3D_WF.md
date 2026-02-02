# **BioTISR Dataset: 3D Microtubules Subset Structure**

## **1\. 简介 (Introduction)**

该子数据集是 **BioTISR** (Biological Time-lapse Image Super-Resolution) 库的 **3D Microtubules (微管)** 部分。数据通过 **3D-SIM** (三维结构光照明荧光显微镜) 模式采集，旨在为开发处理 3D 体数据和时序动态的超分辨率 (ISR) 算法提供高质量基准。与 F-actin 数据类似，该数据集也侧重于在不同信噪比下的重建能力评估。

## **2\. 文件夹结构详情 (Folder Structure Details)**

根据截图显示，压缩包解压后的根目录名为 BioTISR_MT_3D，内部以 **Cell (细胞)** 为单位进行组织。

**目录树结构如下：**

BioTISR_MT_3D/ # 数据集根目录 (3D 微管数据)

├── Cell_001/ # 第 1 个细胞样本 (ROI)

│ ├── RawSIMData_level_01.mrc # \[输入\] 低激发强度原始 SIM 数据 (Low SNR)

│ ├── RawSIMData_level_02.mrc # \[参考\] 高激发强度原始 SIM 数据 (High SNR)

│ └── SIM_gt.mrc # \[真值\] 重建后的超分辨率图像 (Ground Truth)

├── Cell_002/

│ ├── RawSIMData_level_01.mrc

│ ├── RawSIMData_level_02.mrc

│ └── SIM_gt.mrc

├── ...

└── Cell_N/ # 每个文件夹包含对应的原始数据对和真值

## **3\. 文件术语与参数说明 (File Terminology & Parameters)**

每个 ROI 文件夹包含三份核心文件，对应不同的图像质量和处理阶段。

### **3.1 原始输入数据 (Raw Input)**

- **文件名**: RawSIMData_level_01.mrc / RawSIMData_level_02.mrc
- **文件格式**: **.mrc** (体数据/显微镜图像堆栈格式)。
- **内容描述**:
    - **Level_01**: 低激发光强度采集，噪声较高，作为低信噪比输入 (Low SNR Input)。
    - **Level_02**: 高激发光强度采集，信噪比较高，作为参考或高质量输入。
- **维度参数 (3D-SIM)**:
    - **相位 (Phases)**: 3
    - **方向 (Orientations)**: 5
    - **时间点 (Timepoints)**: 10
    - **Z轴 (Z-slices)**: 包含 Z 轴层面的堆栈信息（体数据）。
    - **结构**: 数据为 $N \\times M \\times T$ 的原始图像组，即每个时间点由 15 张原始条纹图组成。

### **3.2 超分辨真值数据 (Ground Truth)**

- **文件名**: SIM_gt.mrc
- **描述**: 使用传统 SIM 重建算法生成的 3D 超分辨率图像。
- **用途**: 深度学习模型训练时的**标签 (Ground Truth)**。
- **特性**: 微管结构通常比 F-actin 更细密，该真值图像已解算出微管的高频细节。

## **4\. 关键技术规格 (Technical Specifications)**

- **生物结构**: Microtubules (微管)。
- **成像模式**: 3D-SIM (Three-Dimensional Structured Illumination Microscopy)。
- **样本数量**: 包含至少 50 个不同的 ROI。
- **采集策略**: 保持曝光时间恒定，通过改变激发光强度（Excitation Intensity）来获取 Level 01 和 Level 02 数据。

## **5\. 引用 (Citation)**

如果您在研究中使用了此数据集结构，请引用：

Code snippet

@article{Qiao_BioTISR_2024,

title = {Time-lapse Image Super-resolution Neural Network with Reliable Confidence Evaluation for Optical Microscopy},

author = {Qiao, Chang and Liu, Shuran and Wang, Yuwang and Xu, Wencong and others},

journal = {bioRxiv},

year = {2024},

doi = {10.1101/2024.05.04.592503}


}
