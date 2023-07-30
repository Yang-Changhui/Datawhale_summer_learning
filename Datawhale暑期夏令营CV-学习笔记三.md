# Datawhale暑期夏令营CV-学习笔记三

### 使用PaddleClas套件进行脑PET图像分析和疾病预测

#### 1.数据集准备

**由于nii文件较少，所以可以将nii文件改成jpg文件，增加数据量，将nii文件的每个通道都保存一个图片。**

#### 2.数据划分

**在模型进行训练时，我们需要划分训练集，验证集和测试集，可以按8：1：1的比例进行划分。**

#### 3.模型训练

##### 模型选择：

**PP-HGNet(High Performance GPU Net) 是百度飞桨视觉团队自研的更适用于 GPU 平台的高性能骨干网络，该网络在 VOVNet 的基础上使用了可学习的下采样层（LDS Layer），融合了 ResNet_vd、PPHGNet 等模型的优点，该模型在 GPU 平台上与其他 SOTA 模型在相同的速度下有着更高的精度。在同等速度下，该模型高于 ResNet34-D 模型 3.8 个百分点，高于 ResNet50-D 模型 2.4 个百分点，在使用百度自研 SSLD 蒸馏策略后，超越 ResNet50-D 模型 4.7 个百分点。与此同时，在相同精度下，其推理速度也远超主流 VisionTransformer 的推理速度**

#### 4.基于 Python 预测引擎推理

**基于训练的模型，对每张图片进行预测，并进行标签的分类。**

#### 5.对每个类别的预测结果进行投票

**由于对测试集的nii文件进行了jpg文件的划分，所以需要对每一个nii文件划分的所有jpg文件进行预测投票，选择票数多的作为该nii文件的标签。**

参考链接：https://aistudio.baidu.com/aistudio/projectdetail/6549820?channelType=0&channel=0

