---
layout:     post
title:      "线性表存储结构 & Java实现"
subtitle:   " Linear List"
date:       2017-12-05 13:30:00
author:     "ZJF"
header-img: "img/post-bg-2015.jpg"
catalog: false
tags:
    - 数据结构
---

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









