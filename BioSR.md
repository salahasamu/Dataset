**BioSR Dataset (Detailed File Structure)**

**1\. 简介 (Introduction)**

该数据集是 **BioSR** (Nature Methods, 2021) 论文的配套数据。BioSR 是一个用于光学显微镜图像超分辨率 (Super-Resolution, SR) 重建的大规模基准数据集，旨在评估和开发基于深度学习的超分辨率算法。

本数据集包含了成对的低分辨率 (Low-Resolution, LR) 和高分辨率 (High-Resolution, HR) 荧光显微镜图像。这些数据覆盖了多种生物结构（如微管、内质网、F-肌动蛋白等）以及不同的信噪比水平，旨在支持超分辨率模型的训练、保真度评估以及在不同成像条件下的鲁棒性测试。

**2\. 数据来源与格式 (Source & Format)**

- **原始论文**: Qiao, C., Li, D., et al. (2021). _Nature Methods_.
- **文件格式**: **.mrc** (Medical Research Council)。
    - 这是一种标准的电子显微镜和高级光学显微镜图像存储格式，支持多维图像堆栈 (Stack)。
    - 在本数据集中，.mrc 文件通常包含重建一幅 SIM 图像所需的原始相位图序列（如 9 张或 15 张 Raw images），或者是重建后的 3D/2D 图像。
- **配套工具**: 补充文件中提供了 Matlab (.m) 和 Python (.py) 的 .mrc 文件读取脚本。

**3\. 文件夹结构详情 (Folder Structure Details)**

数据集根目录包含按生物结构分类的压缩包（F-actin.zip, ER.zip 等）以及补充文件。

**3.1 线性 F-肌动蛋白 (F-actin)**

- **特点**: 拥有最完整的噪声等级序列（Level 01 至 Level 12），适合精细的抗噪性能测试。
- **结构**:

Plaintext

F-actin/

├── Cell_008/

│ ├── RawSIMData_gt.mrc # 用于生成 Ground Truth 的原始高信噪比相位数据

│ ├── SIM_gt.mrc # 经过重建算法生成的 Ground Truth 图像

│ ├── RawSIMData_level_01.mrc # 噪声极大（极低 SNR）的原始输入数据

│ ├── ... # (中间等级 02-11)

│ └── RawSIMData_level_12.mrc # 噪声较小（高 SNR）的原始输入数据

└── Cell_...

**3.2 非线性 F-肌动蛋白 (F-actin_Nonlinear)**

- **特点**: 包含两个版本的 Ground Truth (a 和 b)，噪声等级为 Level 01 至 Level 09。
- **结构**:

Plaintext

F-actin_Nonlinear/

├── Cell_044/

│ ├── SIM_gt_a.mrc # Ground Truth 重建图像 (版本 A)

│ ├── SIM_gt_b.mrc # Ground Truth 重建图像 (版本 B)

│ ├── RawSIMData_gt.mrc # 原始 Ground Truth 相位数据

│ ├── RawSIMData_level_01.mrc

│ ├── ...

│ └── RawSIMData_level_09.mrc

└── Cell_...

**3.3 微管 (Microtubules) 与 网格蛋白小窝 (CCPs)**

- **特点**: 两者结构相似，噪声等级均为 Level 01 至 Level 09。
- **结构**:

Plaintext

Microtubules/ (或 CCPs/)

├── Cell_045/

│ ├── SIM_gt.mrc # Ground Truth 重建图像

│ ├── RawSIMData_gt.mrc # Ground Truth 对应的原始相位数据

│ ├── RawSIMData_level_01.mrc

│ ├── ...

│ └── RawSIMData_level_09.mrc

└── Cell_...

**3.4 内质网 (ER)**

- **特点**: 结构最为复杂。与其他类别不同，ER 的 **Ground Truth 也被分为了多个等级** (level_01 至 level_06)，且分为三个子文件夹存储。
- **结构**:

Plaintext

ER/

├── Cell_009/

│ ├── RawGTSIMData/ # Ground Truth 对应的原始相位数据组

│ │ ├── RawGTSIMData_level_01.mrc

│ │ └── ... (至 level_06)

│ ├── GTSIM/ # Ground Truth 重建图像组

│ │ ├── GTSIM_level_01.mrc

│ │ └── ... (至 level_06)

│ └── RawSIMData/ # 低信噪比（输入用）原始相位数据组

│ ├── RawSIMData_level_01.mrc

│ └── ... (至 level_06)

└── Cell_...

**3.5 补充文件 (Supplementary Files)**

- **文件名**: Supplementary Files for BioSR.zip
- **内容**:
    - **IO_MRC_MATLAB/**: read_mrc.m, write_mrc.m (Matlab 读写脚本)。
    - **IO_MRC_Python/**: read_mrc.py (Python 读取脚本)。
    - **OTF_File/**: 包含光学传递函数文件（如 TIRF_OTF2D_488.mrc）及相关读取脚本。这对物理模型驱动的重建算法至关重要。
    - **imaging_conditions.xlsx**: 记录了成像的具体参数。

**4\. 关键文件术语说明 (Key Terminology)**

- **RawSIMData**: 指未经重建算法处理的原始显微镜采集数据 (Raw Phase Images)。对于 SIM 显微镜，这通常是一个包含多张（如 9 张或 15 张）不同相位和角度的图像堆栈。这是算法的**输入**。
- **Ground Truth (GT)**:
    - **RawSIMData_gt / RawGTSIMData**: 采集条件最优（高光子数、低噪声）时的原始数据。
    - **SIM_gt / GTSIM**: 利用上述最优原始数据，经过传统重建算法计算得到的最终高分辨率图像。这是深度学习模型的**训练目标 (Target)**。
- **Level_XX**: 代表不同的信噪比 (SNR) 水平。level_01 通常代表噪声最大、信号最弱的情况，数字越大信号越好。

**5\. 数据集用途 (Usage)**

1.  **端到端 SIM 重建 (End-to-End SIM Reconstruction)**:

利用 RawSIMData 作为输入，训练网络直接输出 SIM_gt，实现从原始数据到超分辨图像的直接映射。

1.  **物理模型辅助重建**:

结合 OTF_File 中的光学传递函数，开发基于物理模型的深度学习网络（如展开网络 Unrolling Networks）。

1.  **不同噪声水平下的鲁棒性验证**:

利用 level_01 到 level_12 的细粒度数据，绘制算法性能随信噪比变化的曲线。

**6\. 引用 (Citation)**

Code snippet

@dataset{BioSR_Dataset_2020,

author = {Qiao, Chang and Li, Di},

title = {BioSR: a biological image dataset for super-resolution microscopy},

publisher = {Figshare},

year = {2020},

url = {https://doi.org/10.6084/m9.figshare.13264793.v9}

}