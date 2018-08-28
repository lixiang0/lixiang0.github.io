---
title: "darknet:cannot compile with gpu=1"
category: other
layout: post
tags: [Pytorch,dl]
date: '2018-08-28 17:26:24'
---

## 问题描述
在编译dartnet的时候设置GPU=1的时候编译出现错误：
```
compilation terminated due to -Wfatal-errors.
Makefile:91: recipe for target 'obj/crop_layer_kernels.o' failed
make: *** [obj/crop_layer_kernels.o] Error 1
/usr/include/string.h: In function ‘void* __mempcpy_inline(void*, const void*, size_t)’:
/usr/include/string.h:652:42: error: ‘memcpy’ was not declared in this scope
   return (char *) memcpy (__dest, __src, __n) + __n;
                                          ^
compilation terminated due to -Wfatal-errors.
Makefile:91: recipe for target 'obj/avgpool_layer_kernels.o' failed
make: *** [obj/avgpool_layer_kernels.o] Error 1
/usr/include/string.h: In function ‘void* __mempcpy_inline(void*, const void*, size_t)’:
/usr/include/string.h:652:42: error: ‘memcpy’ was not declared in this scope
   return (char *) memcpy (__dest, __src, __n) + __n;
                                          ^
compilation terminated due to -Wfatal-errors.
Makefile:91: recipe for target 'obj/blas_kernels.o' failed
make: *** [obj/blas_kernels.o] Error 1

```


## 解决办法：

1.正确安装cuda，并设置cuda路径
2.Makefile中添加NVCC += -D_FORCE_INLINES
例如：
```
ifeq ($(GPU), 1) 
NVCC += -D_FORCE_INLINES
COMMON+= -DGPU -I/usr/local/cuda/include/
CFLAGS+= -DGPU
LDFLAGS+= -L/usr/local/cuda/lib64 -lcuda -lcudart -lcublas -lcurand
endif
```

