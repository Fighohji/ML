## CNN

- 处理影像辨识

- CNN无法处理图像比例变化或者旋转，需要做数据增强（可以使用spatial transformer layer）

- 图形增强（augment）技巧

  - `transforms.RandomResizedCrop(size, scale=(0.08, 1.0), ratio=(3/4, 4/3))`

    - `size`：裁剪后缩放到的目标尺寸，可以是一个整数或一个二元组。
    - `scale`：随机裁剪区域的面积占原图面积的比例范围，默认值为 `(0.08, 1.0)`，即裁剪区域的面积可以在 8% 到 100% 之间变化。
    - `ratio`：随机裁剪区域的宽高比范围，默认值为 `(3/4, 4/3)`，即裁剪区域的宽高比可以在 3/4 到 4/3 之间变化。

  - `transforms.Resize((128, 128))`

  - `RandomHorizontalFlip(p=0.5)`

    以50%的概率随机水平翻转图像。这有助于增强模型对水平翻转的不变性。

  - `ColorJitter(brightness=0.5)`

    随机改变图像的亮度，范围为原亮度的50%


  - `RandomRotation(5)`

    随机旋转图像，角度在 -5 到 +5 度之间

  - `transforms.AutoAugment($policy)`
    - `policy`：
    - `AutoAugmentPolicy.IMAGENET`:适用于一般的自然图像分类任务
    - `AutoAugmentPolicy.CIFAR10`:适用于小尺寸（32x32 像素）的图像分类任务
    - `AutoAugmentPolicy.SVHN`:适用于街景数字识别任务

- 一层CNN

  ```python
  ## input 3 * x * x
  nn.Conv2d(3, 32, 3, 1, 1), ## kernel size = 3, stride = 1, padding = 1
  ## 32 * x * x
  nn.BatchNorm2d(32),
  nn.ReLU(),
  nn.MaxPool2d(2, 2, 0), ## kernel size = 2, stride = 2, padding = 0，最大池化或者均值池化，也可以不用
  ## 32 * (x / 2) * (x / 2)
  ```

  