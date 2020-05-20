# **Task01**：赛题理解

## 一、数据理解

### 1.现有数据        

​	训练集是30000张门牌号照片，测试集10000张门牌号照片，并且通过json文件给出了每张照片数字部分的位置，标签，照片名称。

![](D:\17.github\1.datawhale_CV\Datawhale_CV\图片\Task01\JSON.jpg)

 	门牌号是由2-4位数字构成的，因此这个问题将变成一个识别变长图像的问题。



|                                                              | 标签 | 字符数 |
| ------------------------------------------------------------ | ---- | ------ |
| ![](https://github.com/zr8910/Datawhale_CV/tree/master/%E5%9B%BE%E7%89%87/Task01/000031.png) | 43   | 2      |
| ![](D:\17.github\1.datawhale_CV\Datawhale_CV\图片\Task01\000030.png) | 638  | 3      |
| ![](D:\17.github\1.datawhale_CV\Datawhale_CV\图片\Task01\000078.png) | 1922 | 4      |

### 2. 解题思路

​	1.读取json，通过json中位置信息截图图片中的字符的信息

​	2.通过将变长识别的问题转换成定长识别的问题		

```python
import json
import numpy as np
import cv2
import matplotlib.pyplot as plt
train_json = json.load(open('D:/15.study/Datawhale_CV/input/train.json'))
```


```python
# 将数据标注转换成整形
def parse_json(d):
    arr=np.array([
        d['top'],
        d['height'],
        d['left'],
        d['width'],
        d['label']
    ])
    arr=arr.astype(int)
    return arr

img=cv2.imread('D:/15.study/Datawhale_CV/input//train/000000.png')
arr=parse_json(train_json['000000.png'])
```


```python
plt.figure(figsize=(10,10))
plt.subplot(1,arr.shape[1]+1,1)
plt.imshow(img)
plt.xticks([]);plt.yticks([])
for idx in range(arr.shape[1]):
    plt.subplot(1,arr.shape[1]+1,idx+2)
    # 根据json中给出的图像位置截取图片的数字
    plt.imshow(img[arr[0,idx]:arr[0,idx]+arr[1,idx],arr[2,idx]:arr[2,idx]+arr[3,idx]])
    plt.title(arr[4,idx])  # 将标签作为突破标题
    plt.xticks([]);plt.yticks([])
```

![](D:\17.github\1.datawhale_CV\Datawhale_CV\图片\Task01\output_2_0.png)
