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


![png](output_2_0.png)



```python

```


```python
arr[1,0]
```




    219




```python

```
