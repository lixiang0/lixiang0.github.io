---
title: "opencv中如何合并多张图片到一张图片中"
category: other
layout: post
tags: opencv
date: '2018-6-24 18:00:24'
---


今天遇到一个问题，需要将多张图片放到一张中，并且还需要添加padding。
首先介绍思路：

- 将待合成的图片尺寸resize到一致
- 根据待合成图片的长宽确定合并的起始结束点
- 输出图片

```
path='./img/'
imgs1=['picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg']
imgs2=['picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg','picasso.jpg']
# Load origin image
img=cv2.imread('./origin.png')

#合成的初始位置与边界padding=50
#合成的图片之间padding=5
#待合成图片长宽都为200
h,w=200,200
for i in range(len(imgs1)):
	temp=cv2.resize(cv2.imread(path+imgs1[i]),(h,w))
	cv2.putText(temp, imgs1[i].split('.')[0], (10, 180), cv2.FONT_HERSHEY_SIMPLEX, 0.4, (255, 255, 255), 1)
	img[50:h+50,(i*w+i*5)+50:((i+1)*w+i*5)+50]=temp
for i in range(len(imgs2)):
	temp=cv2.resize(cv2.imread(path+imgs2[i]),(h,w))
	cv2.putText(temp, imgs2[i].split('.')[0], (10, 180), cv2.FONT_HERSHEY_SIMPLEX, 0.4, (255, 255, 255), 1)
	img[h+50+5:2*h+50+5,(i*w+i*5)+50:((i+1)*w+i*5)+50]=temp

#load and write image
cv2.imwrite('result.jpg',img)
cv2.imshow('img',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```