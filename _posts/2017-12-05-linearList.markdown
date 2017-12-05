---
layout:     post
title:      "线性表的存储结构 & Java实现"
subtitle:   " Linear List"
date:       2017-12-05 13:30:00
author:     "ZJF"
header-img: "img/post-bg-2015.jpg"
catalog: false
tags:
    - 数据结构
---

* 我个人对线性表的理解是:存储有限且`有序`数据元素的容器,简单的说就是个有序列表

线性表的存储方式有两种:顺序存储 链式存储,同样是存储数据,两种数据结构在操作数据时的效率还是有一定的差异

本文主要分享我觉得比较重要、常用的内容   `系统学习请看书^_^`


```java
	//新增元素
    public boolean add(E var1) {
        this.ensureCapacity(this.size + 1);
        this.elementData[this.size++] = var1;
        return true;
    }

    //检查数组容量并在必要时扩容
    public void ensureCapacity(int var1) {
        ++this.modCount;
        int var2 = this.elementData.length;
        if(var1 > var2) {
            Object[] var3 = this.elementData;
            int var4 = var2 * 3 / 2 + 1;
            if(var4 < var1) {
                var4 = var1;
            }

            this.elementData = Arrays.copyOf(this.elementData, var4);
        }

    }
```









