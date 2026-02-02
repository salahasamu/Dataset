# **BioTISR Dataset (Detailed File Structure)**

## **1\. 简介 (Introduction)**

BioTISR (Biological Time-lapse Image Super-Resolution) 是一个专为**时序 (Time-lapse)** 光学显微镜图像超分辨率重建设计的基准数据集。它是此前发布的 **BioSR** 数据集的扩展版本，旨在为社区提供高质量的生物时序超分辨图像，以激发计算超分辨率方法的进一步发展。

该数据集目前涵盖了 **2D** 和 **3D** 的时序图像对 (Image Pairs)，包含了低分辨率 (LR) 和高分辨率 (HR) 图像。数据来源于多种生物结构，并利用了不同的 SIM (Structured Illumination Microscopy) 成像模式采集，特别关注图像在时间维度上的动态变化。

## **2\. 数据来源与格式 (Source & Format)**

- **原始论文**: Qiao, C., Liu, S., Wang, Y., Xu, W., et al. "Time-lapse Image Super-resolution Neural Network with Reliable Confidence Evaluation for Optical Microscopy." _bioRxiv_ (2024).
- **成像系统**: 自研 Multi-SIM 系统。
- **文件格式**:
    - 原始数据通常为多维图像堆栈。补充文件中提供了读取 **.mrc** 文件的脚本，表明数据主要以 MRC 格式存储。
    - **维度定义**: 数据通常以 N-phase × M-orientation × T-timepoint (N个相位 × M个方向 × T个时间点) 的形式组织。

## **3\. 数据集结构详情 (Dataset Structure Details)**

数据集根据维度 (2D/3D) 和生物样本类型进行分类。对于每个感兴趣区域 (ROI)，数据是在恒定曝光时间下，通过增加激发光强度来获取不同信噪比的图像组。

### **3.1 2D 数据集 (2D Dataset)**

- **样本类型 (5种)**:
    - 网格蛋白小窝 (Clathrin-coated pits)
    - 溶酶体 (Lysosomes)
    - 线粒体外膜 (Outer mitochondrial membrane)
    - 微管 (Microtubules)
    - F-肌动蛋白 (F-actin)
- **成像模式与参数**:
    - **GI/TIRF-SIM 模式**: (N=3, M=3, T=20)。
    - **Nonlinear SIM 模式**: (N=5, M=5, T=10)。
- **数据量**: 每个样本至少采集 50 个 ROI，每个 ROI 包含 **3 组**不同光强（信噪比）的原始数据。
- **下载链接**: [Zenodo Record](https://doi.org/10.5281/zenodo.13843670)

### **3.2 3D 数据集 (3D Dataset)**

- **样本类型 (3种)**:
    - 线粒体外膜 (Outer mitochondrial membrane)
    - 微管 (Microtubules)
    - F-肌动蛋白 (F-actin)
- **成像模式与参数**:
    - **3D-SIM 模式**: (N=3, M=5, T=10)。
- **数据量**: 每个 ROI 包含 **2 组**不同光强（信噪比）的原始数据。
- **特别说明 (Quota Limitations)**:
    - 由于存储配额限制，部分原始上传的数据为 **宽场 (Wide-field, WF)** 图像（由 15 张原始图像平均得到，N=1, M=1, T=10）。
    - 随着配额扩展，**Raw SIM** 数据（原始相位图）已逐步更新。
- **下载链接与结构**:
    - **F-actin**:
        - WF input: [Link](BioTISR_F-actin_3D_WF.md)
        - Raw SIM input: [Link](https://doi.org/10.5281/zenodo.13994464)
    - **Microtubules**:
        - WF input: [Link](BioTISR_Microtubules_3D_WF.md)
        - Raw SIM input: [Link](BioTISR_Microtubules_3D.md)
    - **Mitochondria**:
        - WF input: [Link](BioTISR_Mitochondria_3D_WF.md)
        - Raw SIM input: [Link](BioTISR_Mitochondria_3D.md)

## **4\. 关键文件术语说明 (Key Terminology)**

- **Raw Images (N×M×T)**:
    - 重建超分辨图像所需的原始相位数据序列。
    - 例如，对于 3D-SIM，需要 3 个相位 × 5 个方向 = 15 张原始图来重建一个时间点的 3D 图像。
- **WF Input (Wide-field)**:
    - 宽场图像，通常作为低分辨率 (LR) 输入的一种形式或对比基准。在 3D 数据集的早期版本中，它是通过对 15 张 Raw SIM 图像取平均获得的。
- **ROI (Region of Interest)**:
    - 感兴趣区域。为了保证数据的多样性，每个样本采集了至少 50 个不同的细胞区域。

## **5\. 数据集用途 (Usage)**

1.  **时序超分辨率算法开发 (Time-lapse SR Development)**:

利用 T-dimension (时间维度) 的信息开发更稳定的视频超分辨算法，减少帧间闪烁。

2.  **置信度评估 (Confidence Evaluation)**:

正如论文标题所示，该数据集特别适合用于训练和验证能够输出“可靠置信度”的网络，评估重建结果的真实性。

3.  **多模态成像研究**:

涵盖了从 TIRF（全内反射荧光）到 3D-SIM 的多种成像模式，适用于研究不同物理模型下的重建算法。

## **6\. 引用 (Citation)**

Code snippet

@article{Qiao_BioTISR_2024,

author = {Qiao, Chang and Liu, Shuran and Wang, Yuwang and Xu, Wencong and others},

title = {Time-lapse Image Super-resolution Neural Network with Reliable Confidence Evaluation for Optical Microscopy},

journal = {bioRxiv},

year = {2024},

doi = {10.1101/2024.05.04.592503},

url = {https://doi.org/10.1101/2024.05.04.592503}


}
