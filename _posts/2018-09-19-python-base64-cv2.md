---
title: "python将base64字符串转换为cv2中的numpy.ndarray"
category: python
layout: post
tags: [python]
date: '2018-09-19 10:20:24'
---


在开发过程中，android作为客户端，flask作为服务端。图片的通信通过base64字符串的形式进行，所以在服务器端通常需要进行解码。

解码过程中核心的包包括：```cv2 io base64 imageio```.


下面是使用方法：
```
from imageio import imread
import cv2
import io
import base64
bstring='R0lGODlhEAAQAMQAAORHHOVSKudfOulrSOp3WOyDZu6QdvCchPGolfO0o/XBs/fNwfjZ0frl3/zy7////wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACH5BAkAABAALAAAAAAQABAAAAVVICSOZGlCQAosJ6mu7fiyZeKqNKToQGDsM8hBADgUXoGAiqhSvp5QAnQKGIgUhwFUYLCVDFCrKUE1lBavAViFIDlTImbKC5Gm2hB0SlBCBMQiB0UjIQA7'
# reconstruct image as an numpy array
img = imread(io.BytesIO(base64.b64decode(bstring)))
cv2_img = cv2.cvtColor(img, cv2.COLOR_RGB2BGR)
cv2.imshow("reconstructed.jpg", cv2_img)
cv2.waitKey(0)
```
