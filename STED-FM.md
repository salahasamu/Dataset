# **STED-FM Dataset (Detailed File Structure & Parameters)**

## **1\. 简介 (Introduction)**

该数据集是 **STED-FM** (bioRxiv, 2025) 论文的配套数据。它专为 STED 显微镜图像的自监督基础模型（Self-Supervised Foundation Model）训练而设计，旨在学习鲁棒且通用的特征表示。

数据集包含 37,387 张不同尺寸的图像，这些图像被裁剪为 224x224 大小的图像块 (Crops)，总计 976,022 个图像块，全部用于 STED-FM 的预训练。此外，还提供了一个包含 238,683 个图像块的子集，每个图像块都关联了 24 种蛋白质类别中的一种。

## **2\. 数据来源与格式 (Source & Format)**

- **原始论文**: Bilodeau, A.\*, Beaupré, F.\*, et al. (2025). _A Self-Supervised Foundation Model for Robust and Generalizable Representation Learning in STED Microscopy_. bioRxiv.
- **创建者/贡献者**: Bilodeau A., Beaupré F., De Koninck P., Lavoie-Cardinal F. 等。
- **基础参数**:
    - **图像块尺寸 (Crop Size)**: **224 × 224** 像素。
    - **数据集规模**: 976,022 个图像块 (Total Crops)。
    - **标注子集**: 238,683 个图像块 (涵盖 24 种蛋白质类别)。

## **3\. 文件夹结构详情 (Folder Structure Details)**

数据集以 **tar** 归档文件形式提供。解压后，数据主要分为预处理数据 (npz)、原始数值数据 (npz) 和原始 TIFF 数据。

**归档文件列表：**

- STED-FM-dataset-crop.tar: 预处理归一化后的数据 (npz)。
- STED-FM-dataset-crops-raw.tar: 原始数值数据 (npz)。
- STED-FM-dataset-crops-tiff-raw.tar: 原始 TIFF 图像文件。

**NPZ 文件内部结构：**

对于 STED-FM-dataset-crop.tar 和 STED-FM-dataset-crops-raw.tar 中的 .npz 文件，包含以下键值 (Keys)：

- image: 图像数据数组。
- metadata: 相关的元数据信息。

## **4\. 关键文件术语与参数说明 (Key Terminology & Parameters)**

根据描述，各文件包的具体规格如下：

### **4.1 预处理数据 (Preprocessed)**

- **文件名**: STED-FM-dataset-crop.tar
- **格式**: **.npz**
- **描述**: 包含已经过预处理以进行归一化 (Normalization) 的图像块。
- **用途**: 直接用于深度学习模型的训练输入。

### **4.2 原始数值数据 (Raw Values)**

- **文件名**: STED-FM-dataset-crops-raw.tar
- **格式**: **.npz**
- **描述**: 包含图像的原始像素值 (Raw Values)。
- **用途**: 适用于需要自定义预处理流程的研究。

### **4.3 原始 TIFF 数据 (Raw TIFF)**

- **文件名**: STED-FM-dataset-crops-tiff-raw.tar
- **格式**: **.tif**
- **描述**: 以通用 TIFF 格式存储的原始图像块。
- **用途**: 用于可视化或兼容仅支持标准图像格式的软件工具。

## **5\. 类别概览 (Category Overview)**

数据集提供了一个特定子集，用于分类或监督学习任务：

1.  **Labeled Subset**: 包含 238,683 个图像块。
2.  **Protein Classes**: 涵盖 **24** 种不同的蛋白质类别 (具体蛋白质名称需参考元数据或论文原文)。

## **6\. 引用 (Citation)**

在使用此数据集时，请引用以下信息：

Code snippet

@article{Bilodeau_bioRxiv_2025,

author = {Bilodeau, Anthony and Beaupr{\\'e}, Fr{\\'e}d{\\'e}ric and Chabbert, Julia and Bellavance, Jean-Michel and Lessard, K. and Desch{\\^e}nes, Andr{\\'e}anne and Bernatchez, R. and De Koninck, Paul and Gagn{\\'e}, Christian and Lavoie-Cardinal, Flavie},

title = {A Self-Supervised Foundation Model for Robust and Generalizable Representation Learning in STED Microscopy},

journal = {bioRxiv},

year = {2025},

publisher = {Cold Spring Harbor Laboratory}


}
