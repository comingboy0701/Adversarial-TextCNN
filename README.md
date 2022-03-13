## 对抗训练简介
本实验简单的实现了FGSM、PGD、Free
详细的介绍可以参考[实验报告](documents/实验报告.pdf) 。

## 数据集

数据集是[TextCNN作者](https://github.com/649453932/Chinese-Text-Classification-Pytorch) 从[THUCNews](http://thuctc.thunlp.org/) 中抽取了20万条新闻标题，已上传至github，文本长度在20到30之间。一共10个类别，每类2万条。

类别：财经、房产、股票、教育、科技、社会、时政、体育、游戏、娱乐。

数据集划分：

|数据集|数据量|
|:--------:|:--------:|
|训练集|18万|
|验证集|1万|
|测试集|1万|

## 机器配置

GPU: 16G V100

其他: 16核CPU128G内存


## 效果

|对抗训练方法|acc|micro-precison|micro-recall|micro-f1|训练时间|epoch(20)|Test loss|实验配置|
| :--------: | :--------: | :--------: | :--------: | :--------: | :--------: | :--------: | :--------: | :--------: |
|Base TextCNN|89.18%|0.8924|0.8918|0.8919|1分23秒|3|0.34|early stop|
|FGSM|90.87%|0.9089|0.9087|0.9086|5分11秒|6|0.3|epsilon=0.1,early stop|
|PGD|89.81%|0.8989|0.8981|0.8982|5分12秒|4|0.33|epsilon=0.1,K=3,alpha=0.1,early stop|
|Free|88.07%|0.8817|0.8807|0.8808 |3分51秒|3|0.39|epsilon=0.1,M=3,early stop|


## 使用说明
```
# 代码说明：
# 1.训练的入口程序是run.py
# 2.对抗训练的父类是BaseModel，没有实现任何的对抗训练的方法，也就是Baseline TextCNN
# 3.公用的方法均放在了父类BaseModel中，子类实现了各自计算扰动的方法和更新的流程
# 4.各对抗训练的流程对应的Model文件中有完整的注释


# 训练并测试：
# Base TextCnn，at_type不配置的化，默认是Base
python run.py --at_type=Base

# FGSM
python run.py --at_type=FGSM

# PGD
python run.py --at_type=PGD

# Free
python run.py --at_type=Free
```
