---
layout:     post
title:      "Java并发笔记(二)"
subtitle:   "同步容器|并发容器|ConcurrentHashMap"
date:       2018-06-01 13:30:00
author:     "ZJF"
header-img: "img/post-bg-unix-linux.jpg"
catalog: false
tags:
    - Java核心技术
---

* Java的类库提供了一系列与并发相关的容器类,有和同步相关的同步容器,也有和并发相关的并发容器,本文挑几个典型的介绍一下原理

## 同步容器
学习Java集合类的时候大家都应该接触过一个“古老的”容器类Vector,这个容器类几乎已经不被项目开发使用了,起码我的一年多工作经历中没见过有代码中用这个容器,这里主要是以Vector为例介绍一下同步容器的一些特性,和使用小细节,不记录过多篇幅了.

一同步容器类实现线程安全的方式一般是:将类中的变量(状态)封装起来,并对开放给外部的public方法进行同步加锁.
* 这些同步容器的暴露的方法都是线程安全的,但是不代表我们使用它写出来的代码是线程安全的
一个典型的例子就是迭代(遍历)容器内的元素,或者这种针对容器内元素下标进行操作的代码


## 并发容器

先从两个点比较一下ConcurrentHashMap的优势吧,不然我们为什么要使用它呢?
* 在并发场景下ConcurrentHashMap相对于HashMap的安全性更高
* 在并发场景下ConcurrentHashMap相对于HashTable的性能更好

HashMap不是线程安全的这个大家都知道,或者说HashMap设计的时候可能就没往并发的场景上考虑,没有同步机制的数据结构性能肯定是比较快的.
HashTable就比较古老了,像我这种刚毕业的时候直接用JDK1.8的...根本接触不到,而且这个类也已经不被推荐使用了,但是作为对比学习设计思路还是好的.

并发笔记(一)里面也总结了,如果要变成的线程安全的,肯定需要相应的同步机制,像HashTable就是使用了synchronized代码块进行同步来确保并发场景下的安全性,但是缺点也很明显,同步的代发范围太大了,有一些方法直接在方法声明上就用了synchronized,这就大大降低了并发场景下的读取性能.

ConcurrentHashMap在保证线程安全的前提下提高性能的方式主要是
* 减少同步覆盖的范围,采用分段锁
* 使用volatile、final以及CAS等技术

接下来直接看代码!
```java
	/**
     * Creates a new, empty map with the default initial table size (16).
     */
    public ConcurrentHashMap() {
    }
```


```java
final V putVal(K key, V value, boolean onlyIfAbsent) {
        if (key == null || value == null) throw new NullPointerException();
        int hash = spread(key.hashCode());
        int binCount = 0;
        for (Node<K,V>[] tab = table;;) {
            Node<K,V> f; int n, i, fh;
            if (tab == null || (n = tab.length) == 0)
                tab = initTable();
            else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {
                if (casTabAt(tab, i, null,
                             new Node<K,V>(hash, key, value, null)))
                    break;                   // no lock when adding to empty bin
            }
            else if ((fh = f.hash) == MOVED)
                tab = helpTransfer(tab, f);
            else {
                V oldVal = null;
                synchronized (f) {
                    if (tabAt(tab, i) == f) {
                        if (fh >= 0) {
                            binCount = 1;
                            for (Node<K,V> e = f;; ++binCount) {
                                K ek;
                                if (e.hash == hash &&
                                    ((ek = e.key) == key ||
                                     (ek != null && key.equals(ek)))) {
                                    oldVal = e.val;
                                    if (!onlyIfAbsent)
                                        e.val = value;
                                    break;
                                }
                                Node<K,V> pred = e;
                                if ((e = e.next) == null) {
                                    pred.next = new Node<K,V>(hash, key,
                                                              value, null);
                                    break;
                                }
                            }
                        }
                        else if (f instanceof TreeBin) {
                            Node<K,V> p;
                            binCount = 2;
                            if ((p = ((TreeBin<K,V>)f).putTreeVal(hash, key,
                                                           value)) != null) {
                                oldVal = p.val;
                                if (!onlyIfAbsent)
                                    p.val = value;
                            }
                        }
                    }
                }
                if (binCount != 0) {
                    if (binCount >= TREEIFY_THRESHOLD)
                        treeifyBin(tab, i);
                    if (oldVal != null)
                        return oldVal;
                    break;
                }
            }
        }
        addCount(1L, binCount);
        return null;
    }
```

















