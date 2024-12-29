# 环境配置

1. 请将ViT-B-32.pkl放在JCLIP目录下
2. Dataset目录存放TrainSet，TestSet。其中valid.txt取TrainSet中的10张图作为验证集。valid_b.txt在valid.txt的基础上增加了Stanford-cars，若要使用，请将Stanford-cars数据集下载放到TrainSet目录下。

# 文件介绍

提供了在A榜使用的模型。

- train.py
- train.sh
- test.py

由于B榜的测试集添加了car但没有训练集。原有的效果不好，因此B榜的结果为clip微调。

- clip_ft.py

- train_clip_ft.py

- test_clip_ft.py

# 思路介绍

## A榜

使用了Cross-Modal Few-Shot Learning with Multimodal Models中的办法作为基础并进行模型修改。

在该方法中，图片和图片的描述均作为分类器的样本，但是两种样本的是否同样重要。当我们只使用图片，相比于图片+图片的描述，降了一个点；只使用图片的描述，则完全不行。因此，在B榜准备尝试，将图片和图片的描述分别计算loss，然后赋予不同权重相加。以期望通过loss对模型输入图片和图片的描述样本的重要程度。

但因car没有样本，最终未使用。

## B榜

在descri_class_google.txt，我们通过使用google翻译对类别的描述进行适当的补充。对于那些常见的事物，clip模型有着较高的识别率。对于少见的事物，我们尝试提供一些有辨别力的特征描述，以提高识别率。
