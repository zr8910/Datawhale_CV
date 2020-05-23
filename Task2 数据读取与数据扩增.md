# Task2 数据读取与数据扩增

##  一、图像读取

###  1.读取图像的方法

#### 方法一：利用PIL中的Image函数，这个函数读取出来不是array格式这时候需要用 np.asarray(im) 或者np.array（）函数。

```python
from PIL import Image
import numpy as np

I=Image.open('./input/train/000000.png')
I.show()
```

#### 方法二：利用opencv-python接口

```python
import cv2
I=cv2.imread('./input/train/000000.png')
print(I)
```

## 2.图像识别的问题

图像识别训练的样本往往都是照片，照片受到光线色彩角度的影响，训练样本的时候要考虑将这些干扰的特征因素去除，这样的话才能增加模型的泛化能力。

在深度学习中增加模型的泛化能力主要是数据扩增，数据扩增可以从颜色、尺度、样本空间进行扩增。

### 3. 常用的数据扩增方法

- transforms.CenterCrop      对图片中心进行裁剪      

- transforms.ColorJitter      对图像颜色的对比度、饱和度和零度进行变换      

- transforms.FiveCrop     对图像四个角和中心进行裁剪得到五分图像     

- transforms.Grayscale      对图像进行灰度变换    

- transforms.Pad        使用固定值进行像素填充     

- transforms.RandomAffine      随机仿射变换    

- transforms.RandomCrop      随机区域裁剪     

- transforms.RandomHorizontalFlip      随机水平翻转     

- transforms.RandomRotation     随机旋转     

- transforms.RandomVerticalFlip     随机垂直翻转 

  本题是对门牌号进行识别，因此不能采用翻转扩增，会造成数据的不准确。



