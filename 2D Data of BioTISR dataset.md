# **2D Data of BioTISR dataset**

## **1\. 简介 (Introduction)**

**BioTISR** (Biological Time-lapse Image Super-Resolution) 是一个大规模生物图像超分辨率数据集。该数据集旨在解决现有超分辨算法缺乏高质量、动态（Time-lapse）生物训练数据的问题。

它包含 **2D** 和 **3D** 的时序图像对，涵盖网格蛋白小窝 (CCPs)、微管、线粒体等多种生物结构。其核心特点是提供了同一视场下不同激发光强度（即不同信噪比）的原始图像及其对应的高质量超分辨真值。

## **2\. 数据来源与格式 (Source & Format)**

- **原始论文**: Qiao, C., et al. (2024). _bioRxiv_. "Time-lapse Image Super-resolution Neural Network..."
- **数据发布页**: [Zenodo Link](https://doi.org/10.5281/zenodo.13843670)
- **文件格式**:
    - **图像数据**: **.mrc** (一种常用于电镜和显微成像的体素数据格式，包含多维堆栈信息)。
    - **压缩包**: 按生物样本类型分类的 .zip 文件。

## **3\. 文件夹结构详情 (Folder Structure Details)**

数据集根目录包含按生物结构分类的压缩包（如 BioTISR_CCPs.zip）。解压后，内部按 **细胞 (Cell)** 为单位组织，每个细胞文件夹内包含不同信噪比等级的输入数据和对应的真值。

**通用目录结构：**

Plaintext

BioTISR_\[Structure_Name\]/ # 例如: BioTISR_CCPs/

│

├── Cell_001/ # 第 1 个感兴趣区域 (ROI/Cell)

│ ├── RawSIMData_level_01.mrc # \[输入\] 低信噪比原始 SIM 数据 (Low SNR)

│ ├── RawSIMData_level_02.mrc # \[参考\] 中等信噪比原始 SIM 数据 (Mid SNR)

│ ├── RawSIMData_level_03.mrc # \[参考\] 高信噪比原始 SIM 数据 (High SNR)

│ └── SIM_gt.mrc # \[真值\] 重建后的超分辨率图像 (Ground Truth)

│

├── Cell_002/

│ ├── RawSIMData_level_01.mrc

│ ├── RawSIMData_level_02.mrc

│ ├── RawSIMData_level_03.mrc

│ └── SIM_gt.mrc

│

├── ...

│

└── Cell_N/ 

**注意**: 截图显示通常有 3 个等级 (level_01 至 level_03)。这对应了描述中提到的“通过增加激发光强度采集多组原始图像”。通常 level_01 用作低质量输入，level_03 或由其重建的图像用作高质量参考。

## **4\. 关键文件术语与参数说明 (Key Terminology & Parameters)**

BioTISR 的原始数据是多维张量，具体维度取决于成像模式（TIRF-SIM, Nonlinear SIM 或 3D-SIM）。

### **4.1 原始输入数据 (Raw Input)**

- **文件名**: RawSIMData_level_{XX}.mrc
- **描述**: 原始结构光照明 (SIM) 图像堆栈。
- **维度结构 (Dimensions)**:

根据成像模式，.mrc 文件内部包含以下维度序列：

- - **标准 2D (GI/TIRF-SIM)**: 3 相位 (Phases) × 3 方向 (Orientations) × 20 时间点 (Timepoints) = **180 帧**。
    - **非线性 2D (Nonlinear SIM)**: 5 相位 × 5 方向 × 10 时间点 = **250 帧**。
    - **3D (3D-SIM)**: 3 相位 × 5 方向 × 10 时间点 = **150 帧/层** (需乘以 Z 轴层数)。
- **用途**: 深度学习模型的输入 (Input)。通常模型需要利用相位和方向信息来重建超分辨图像。

### **4.2 超分辨真值 (Ground Truth)**

- **文件名**: SIM_gt.mrc
- **描述**: 经过传统算法（如 HiFi-SIM 或 FairSIM 等）重建后的高信噪比超分辨率图像。
- **来源**: 基于高激发光强度（如 level_03）的原始数据计算得出。
- **用途**: 训练时的标签 (Target)。

## **5\. 类别概览 (Category Overview)**

数据集包含以下主要子集：

1.  **BioTISR_CCPs**: 网格蛋白小窝 (Clathrin-Coated Pits) 2. **BioTISR_F-actin**: 丝状肌动蛋白 (线性 SIM 模式) 3. **BioTISR_F-actin_nonlinear**: 丝状肌动蛋白 (非线性 SIM 模式，分辨率更高) 4.  **BioTISR_Lysosomes**: 溶酶体 5. **BioTISR_Microtubules**: 微管 6. **BioTISR_Mitochondria**: 线粒体 (可能包含 OMM 外膜)

## **6\. 引用 (Citation)**

在使用此数据集时，请引用以下信息：

Code snippet

@article{Qiao_BioRxiv_2024,

author = {Qiao, Chang and Liu, Shuran and Wang, Yuwang and Xu, Wencong and others},

title = {Time-lapse Image Super-resolution Neural Network with Reliable Confidence Evaluation for Optical Microscopy},

journal = {bioRxiv},

year = {2024},

doi = {10.1101/2024.05.04.592503},

publisher = {Cold Spring Harbor Laboratory}


}
