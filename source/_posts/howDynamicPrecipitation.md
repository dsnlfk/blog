---
title: 动画效果如何沉淀的思考！
date: 2016-09-07 14:20:42
tags:
---

### 开篇
在以往的开发经历中，某些动画效果开发过一次，有重复使用的情况，而以往复用有痛点：

```
翻找之苦；
代码耦合之苦；
以上两点也造成他人使用之苦；
```
为了能便于他人，或他人的便于我使用，总需要一些约定／共识，思考如下，期待有更好的姿势！

### 存放的姿势
```
so，是有沉淀的需求;
但，就性质来讲不同于目前的活动组组件生态性质;
是一种很效果类型的，使用率不可估计的可能低的，是根据个人主观判断／欲望／驱动进行考虑沉淀的;
所以我觉得是根据自己驱动，沉淀维护在自己的名称空间gitlab下；
```

### 动画效果的沉淀需要考虑什么问题：
```
1.视觉展示；
视觉展示应该如何做：在README.md中做好gif图展示；

2.便捷获取；
便捷获取：按yo actcmp的脚手架编写动效组件，方面自己／他人bower install 获取；
```

### 即时这样，还会有什么问题：
```
1.重复使用时，有很高的业务修改概率的情况:
(1)为业务而修改，建议把bower下来的代码耦合进你的业务里去修改；
(2)发现能抽象修改的建议，则跟维护者提issue，在组件层面迭代；
```
[一个例子](http://git.ucweb.local/linfk/rain/tree/master)