---
layout:     post
title:      "线性表的存储结构 & Java实现"
subtitle:   " Linear List "
date:       2017-12-05 13:30:00
author:     "ZJF"
header-img: "img/post-bg-2015.jpg"
catalog: false
tags:
    - 数据结构
---

* 我个人对线性表的理解是:存储有限且`有序`数据元素的容器,简单的说就是个有序列表

线性表的存储方式有两种:顺序存储 链式存储,同样是存储数据,两种存储结构在操作数据时的效率还是有一定的差异

本文主要分享我觉得比较重要、常用的内容 

## 线性表的顺序存储结构 

顺序存储结构指的是:开辟一段连续的地址空间依次存储数据元素,这种物理结构带来的好处就是对线性表中的数据进行随机随机存取操作的效率很高,因为可以首地址推算出操作元素的地址而无序遍历整表
时间性能为 O(1)

弊端也很明显,当需要在线性表插入删除元素时,需要将当前元素位置到表尾的所有元素进行移动,时间性能为 O(n)

Java中顺序存储的实现有数组和ArrayList,因为顺序存储需要开辟连续的地址空间,所以如果开始设计的表长较小就容易出错,例如数组越界

ArrayList在使用数组作为存储容器的基础上实现了动态扩容的功能,实现如下:
```java
public class ArrayList<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, Serializable {
    private static final long serialVersionUID = 8683452581122892189L;
    private transient Object[] elementData;
    private int size;

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
}
```











