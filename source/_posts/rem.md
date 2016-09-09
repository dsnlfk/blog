---
title: rem页面适配思路剖析
date: 2016-09-09 15:45:33
tags:
---

### rem是什么
rem是一个半相对单位，它相对的是html(或body)元素的font-size值，例如有html { font-size: 10px; }，则1rem = 10px。

### rem适配理解
当html元素的font-size是根据设备宽度自适应时，使用rem的页面也就会有自适应的特性。  

```  
适配计算：window.innerWidth / 640 * 1000；  
辅助理解：640 ／ 640 = 1px , 320 ／ 640 = 0.5px;  
*1000: 增加页面精度表现，导致rem编写时，(元素值／1000)rem；
```
### 0.64rem的理解
0.64rem能刚好满屏(设计稿640px)的本质在于经过 html.fontSize 单位转化后(的px)等于window.innerWidth；  
为达到上面效果，把设计稿640作为单位运算的条件如下：  

```
实际值(window.innerWidth) / 设计值(640) = rem转化的px / 编码采用设计值  
rem转化的px = 编码采用设计值 * (实际值(window.innerWidth) / 设计值(640))
```