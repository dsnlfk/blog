---
title: 全canvas／canvas应用开发笔记
date: 2016-08-15 20:31:13
tags:
---
"mark一下"

## 结构设计
合理的结构分层确保程序可控、易维护。

```
engine.js(引擎)
	->paragraph／1.js、2.js...(分屏)
		->material.js(零件)
			->titles.js、bg.js...
```
![](http://image.uc.cn/s/uae/g/01/readMeImgs/canvasCodeDesing.png)

### 引擎
驱动分屏；
根据场景分：时间轴驱动、行为驱动；

```
时间轴驱动：
计时器，根据定义的时间刻抛出事件，执行
paragraphs[curId].exit();
paragraphs[nextId].render();

行为驱动:
根据传递 page id 计算目标屏，执行
paragraphs[curId].exit();
paragraphs[nextId].render();
```

### 分屏
合适的时机切分，考虑切分的上下关联情况、过渡表现，分屏层要做的有：

```
为舞台添加零件 secen.addChild(material.el);
零件行为／动画；
(行为驱动项目)在正确的行为时机抛出事件，根据当前屏标示触发进入目标屏;
在合适的时机清除上一屏内容；
```

### 零件（快捷编写套路）

```
h5psd切图：自动化获取元素切图、{x,y,width,height}等信息;
fit组件：解决元素绘制所需的信息转换获取；
utils.js：业务层基本方法封装复用，(Sprict类型还需定义animation);
lia：自定义精灵图合并；
```
注意：元件颗粒化组织程度受是否整屏动效影响，如与分屏对应的‘prg’元件内含多个真正颗粒化元件；

