# 恶意WebURL检测系统 - 项目说明文档
# 源码获取：https://mbd.pub/o/bread/YZWclppsag==

## 📋 项目概述

本项目是一个基于机器学习和深度学习的恶意WebURL检测系统，能够自动识别和分类恶意URL请求，保护Web应用安全。

### 🎯 项目目标

- 开发高效的恶意URL检测算法
- 解决数据不平衡问题，提高检测准确率
- 提供易于使用的Web服务接口
- 支持实时URL安全检测

## 🏗️ 技术架构

### 核心技术栈

- **编程语言**: Python 3.11
- **深度学习框架**: PyTorch 2.0.0
- **机器学习库**: scikit-learn 1.3.0
- **Web框架**: Flask
- **前端技术**: HTML, CSS, JavaScript

### 模型架构

#### 1. 深度学习模型

- **VGGFWithResidualF**: 改进的VGG网络架构，包含残差连接
- **输入特征**: 1000维TF-IDF特征（3-gram分词）
- **网络结构**:
  - 输入层 → 128维全连接层
  - 残差块1（128维）
  - 256维全连接层
  - 残差块2（256维）
  - 128维 → 64维 → 输出层

#### 2. 机器学习模型

- **逻辑回归 (LR)**: 传统机器学习方法
- **XGBoost**: 梯度提升决策树

## 📊 数据集

### 数据来源

- **正常请求**: 1,294,531条正常Web请求
- **恶意请求**: 48,065条恶意URL样本

### 恶意请求类型

- SQL注入攻击
- 跨站脚本攻击 (XSS)
- 路径遍历攻击
- 命令注入攻击
- 其他Web安全威胁

### 数据预处理

- URL解码处理
- 3-gram特征提取
- TF-IDF向量化
- 数据平衡处理

## 🔧 项目文件结构

```
Identifying-Malicious-WebURLs-Based-on-Machine-Learning-and-Deep-Learning/
├── dataset/                          # 数据集文件夹
│   ├── goodqueries.txt              # 正常请求数据
│   ├── badqueries.txt               # 恶意请求数据
│   └── readme                       # 数据集说明
├── 深度学习模型文件/
│   ├── Deeplearing_VGGFWithResidualFnet_Web.py    # 残差网络训练
│   ├── Deeplearing_VGGFnet_Web.py                 # VGG网络训练
│   ├── Deeplearing_FCnet_Web.py                   # 全连接网络训练
│   └── DeeplearingforWeb.py                       # 深度学习主程序
├── 机器学习模型文件/
│   ├── LRforWeb.py                   # 逻辑回归训练
│   └── XboostforWeb.py               # XGBoost训练
├── Web应用文件/
│   ├── Weburl_test_app.py            # Flask Web应用
│   ├── templates/index.html          # 前端页面
│   └── static/                       # 静态资源
├── 改进的训练脚本/
│   ├── improved_training.py          # 完整改进训练脚本
│   ├── medium_training.py            # 中等规模训练脚本
│   └── quick_training.py             # 快速验证脚本
├── 模型文件/
│   ├── model.pth                     # 原始模型权重
│   ├── medium_model.pth              # 改进模型权重
│   ├── quick_model.pth               # 快速训练模型
│   ├── medium_vectorizer.pkl         # 特征提取器
│   ├── FCnet_model.onnx              # ONNX格式模型
│   └── VGGnet_model.onnx             # ONNX格式模型
├── 评估图表/
│   ├── medium_confusion_matrix.png   # 混淆矩阵
│   ├── medium_training_curves.png    # 训练曲线
│   ├── confusion_matrix.png          # 原始混淆矩阵
│   └── convergence_plot.png          # 收敛曲线
└── 工具脚本/
    ├── Load_test_model.py            # 模型加载测试
    └── test_predict.py               # 预测测试
```

## 🚀 快速开始

### 环境要求

- Python 3.8+
- PyTorch 2.0.0
- scikit-learn 1.3.0
- Flask
- 其他依赖见requirements.txt

### 安装步骤

1. **克隆项目**

```bash
git clone <项目地址>
cd Identifying-Malicious-WebURLs-Based-on-Machine-Learning-and-Deep-Learning
```

1. **安装依赖**

```bash
pip install -r requirements.txt
```

1. **训练模型**

```bash
# 快速训练验证
python quick_training.py

# 中等规模训练
python medium_training.py

# 完整训练
python improved_training.py
```

1. **启动Web服务**

```bash
python Weburl_test_app.py
```

1. **访问应用**
   打开浏览器访问: <http://localhost:5000>

## 📈 性能指标

### 改进模型性能（中等规模训练）

- **总体准确率**: 97.28%
- **AUC Score**: 0.9932
- **正常请求检测**: 精确率95%，召回率99%
- **恶意请求检测**: 精确率99%，召回率95%

### 训练过程指标

- **训练轮数**: 30个epoch
- **最终训练准确率**: 99.39%
- **验证准确率**: 97.28%
- **训练损失**: 0.0187
- **验证损失**: 0.1119

## 🔍 技术特点

### 1. 数据不平衡解决方案

- **加权采样**: 使用WeightedRandomSampler平衡数据分布
- **加权损失函数**: 正样本权重调整
- **平衡数据集**: 正常和恶意请求1:1比例

### 2. 模型优化策略

- **残差连接**: 解决深度网络梯度消失问题
- **批归一化**: 提高训练稳定性和收敛速度
- **Dropout**: 防止过拟合，提高泛化能力
- **学习率调度**: 动态调整学习率优化训练过程

### 3. 特征工程

- **3-gram分词**: 捕获URL中的序列模式
- **TF-IDF向量化**: 提取有区分度的特征
- **特征降维**: 选择最重要的1000个特征

## 🌐 Web服务接口

### API端点

- **URL**: `http://localhost:5000/predict`
- **方法**: POST
- **Content-Type**: application/json

### 请求格式

```json
{
    "queries": [
        "http://example.com",
        "http://google.com", 
        "http://example.com/admin.php?id=1'--",
        "http://malicious-site.com/evil.exe"
    ]
}
```

### 响应格式

```json
{
    "predictions": [0, 0, 1, 1],
    "probabilities": [0.02, 0.08, 0.89, 0.95],
    "status": "success"
}
```

## 🛠️ 开发指南

### 模型训练流程

1. **数据准备**: 加载和预处理数据集
2. **特征提取**: 使用TF-IDF进行特征工程
3. **模型构建**: 定义深度学习网络架构
4. **训练配置**: 设置优化器、损失函数、学习率
5. **模型训练**: 执行训练过程并监控指标
6. **模型评估**: 在测试集上评估性能
7. **模型保存**: 保存训练好的模型和特征提取器

### 代码结构说明

- **训练脚本**: 包含完整的训练流程和评估指标
- **Web应用**: 提供用户界面和API接口
- **工具脚本**: 辅助测试和验证功能
- **配置文件**: 模型参数和超参数设置

## 📊 实验结果分析

### 模型对比

| 模型类型       | 准确率     | 优点            | 缺点         |
| ---------- | ------- | ------------- | ---------- |
| 逻辑回归       | 85%     | 训练快速，解释性强     | 特征工程要求高    |
| XGBoost    | 88%     | 处理非线性关系强      | 参数调优复杂     |
| 原始深度学习     | 90%     | 自动特征学习        | 数据不平衡敏感    |
| **改进深度学习** | **97%** | **高准确率，鲁棒性强** | **训练时间较长** |

### 性能提升关键

1. **数据平衡**: 解决了27:1的数据不平衡问题
2. **模型架构**: 残差网络提高了特征提取能力
3. **训练策略**: 加权损失和采样器优化了学习过程

![Web界面](/1.png)
