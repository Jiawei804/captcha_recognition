# captcha recognition

## 项目环境依赖

- python==3.9
- tensorflow==2.10
- captcha-0.5.0
- matplotlib==3.7.3
- numpy==1.24.3
- scikit-learn==1.2.2

## 快速开始

1. 执行create_captcha.ipynb文件，生成足够数量的样本。
2. 执行captcha_recognition.ipynb文件。

## 模型介绍

使用ResNet50模型，在模型输出上先做了平均值池化降维，再接入两层全连接层，最后并行经过4个全连接层得到4个预测结果，为了符合标签值的形状，在其后使用concatenate和reshape作为辅助，这两层没有任何参数。

![model](C:/Users/DELL/Desktop/%E6%9C%BA%E5%99%A8%E8%A7%86%E8%A7%89%E5%A4%A7%E4%BD%9C%E4%B8%9A/model.png)

- 使用Imagenet预训练权重，进行全量微调。
- 对图像采用了归一化，足够大的样本集来让模型得到更好的效果。
- Adam优化器，初始学习率为0.001

## 训练曲线

![learning_curves](C:/Users/DELL/Desktop/%E6%9C%BA%E5%99%A8%E8%A7%86%E8%A7%89%E5%A4%A7%E4%BD%9C%E4%B8%9A/learning_curves.png)

- 模型在训练集和验证集上取得了很好的效果。
- 前几轮训练在验证集上收敛较慢，之后逐步上升。
- 验证集上的最高准确率高达96.17%。
- 在全新数据集上的准确率达到86.6%，增加数据集的大小，也许能够缩小这一差距。