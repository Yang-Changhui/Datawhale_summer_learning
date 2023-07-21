# Datawhale暑期夏令营CV-学习笔记一

## AI环境配置

#### **1.安装**

· Miniconda: https://docs.conda.io/en/latest/miniconda.html

· Visual Studio Code: https://code.visualstudio.com/

#### 2.镜像源选择

校园网联合镜像站   https://help.mirrors.cernet.edu.cn/

#### 3.云端环境的使用

· 百度飞桨 AI Studio https://aistudio.baidu.com/aistudio/index

· 阿里天池 PAI DSW https://tianchi.aliyun.com/notebook-ai

· Kaggle https://www.kaggle.com/code

· Google Colab https://colab.research.google.com/

· Sagemaker Studio Lab https://studiolab.sagemaker.aws/

## CV任务

### 基于脑PET图像的疾病预测挑战赛

#### 基于logistic回归进行分类：

##### 1.数据准备

首先，我们需要导入一些必要的Python库来处理图像数据和构建模型。以下是导入的库：

我们使用`glob`库来获取文件路径，`numpy`用于数值计算，`pandas`用于数据处理，`nibabel`用于加载和处理医学图像数据，`OrthoSlicer3D`用于图像可视化，`Counter`用于计数统计。

##### 2.数据预处理

使用np.random.shuffle()打乱数据集

##### 3.特征提取

对于深度学习任务，特征提取是非常重要的一步。在本例中，我们定义了一个函数`extract_feature`，用于从脑PET图像中提取特征。

`extract_feature`函数从文件路径加载PET图像数据，并从中随机选择10个通道。然后，它计算了一系列统计特征，如非零像素数量、零像素数量、平均值、标准差等。最后，函数根据文件路径判断样本类别，并将提取到的特征和类别作为返回值。

##### 4.模型训练

在这一步骤中，我们将利用`extract_feature`函数提取训练集和测试集的特征，并使用逻辑回归模型对训练集进行训练。

在这里，我们通过循环将特征提取过程重复进行30次，这是为了增加训练样本的多样性。然后，我们使用逻辑回归模型`LogisticRegression`来训练数据。在训练完成后，模型已经学习到了从特征到类别的映射关系。

在`scikit-learn`（sklearn）中，除了逻辑回归（Logistic Regression）之外，还有许多其他的机器学习模型可以用于分类任务中，以下是一些常用于分类任务的机器学习模型：

1. 支持向量机（Support Vector Machines，SVM）：用于二分类和多分类问题，通过构建一个超平面来区分不同类别的样本。
2. 决策树（Decision Trees）：适用于二分类和多分类问题，通过对特征空间进行划分来分类样本。
3. 随机森林（Random Forests）：基于多个决策树的集成算法，用于二分类和多分类问题，提高了模型的泛化能力。
4. K最近邻算法（K-Nearest Neighbors，KNN）：根据最近邻样本的类别来分类新样本，适用于二分类和多分类问题。
5. 朴素贝叶斯（Naive Bayes）：基于贝叶斯定理的分类方法，适用于文本分类等问题。
6. 多层感知器（Multi-layer Perceptrons，MLP）：一种人工神经网络，用于解决复杂的分类问题。
7. 卷积神经网络（Convolutional Neural Networks，CNN）：专用于处理图像和视觉数据的神经网络，在图像分类任务中表现出色。

这些模型在分类任务中有不同的应用场景和性能表现，取决于数据集的特征、样本数量和问题的复杂性。在实际应用中，通常需要根据数据集的特点和具体任务来选择合适的分类模型，并进行模型调参和性能评估，以达到最佳的分类效果。

##### 5.预测

在这一步骤中，我们使用训练好的逻辑回归模型对测试集进行预测，并将预测结果进行投票，选出最多的类别作为该样本的最终预测类别。最后，我们将预测结果存储在CSV文件中并提交结果。

具体来说，我们使用了`Counter`来统计每个样本的30次预测结果中最多的类别，并将结果存储在`test_pred_label`列表中。然后，我们将样本ID和对应的预测类别存储在一个DataFrame中，并将其按照ID排序后保存为CSV文件，这样我们就得到了最终的结果提交文件。

###### 代码地址：https://aistudio.baidu.com/aistudio/projectdetail/6563065