---
title: canvas开发笔记
date: 2016-08-15 20:31:13
tags:
---
"mark一下"

## 设计
```
engine.js(引擎)
	->paragraph／1.js、2.js...(分屏)
		->material.js(零件)
			->titles.js、bg.js...
```
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
合适的时机切分，考虑切分的上下关联性、过渡性；

```
1.为舞台添加零件 secen.addChild(material.el);
2.零件的业务coding／动画表现；
3.(行为驱动)在正确的行为时机抛出事件，根据当前屏标示触发进入目标屏;
4.在合适的时机清除上一屏内容；
```

## 元素编写
1.h5psd切图，获取图片、{x,y,width,height};
2.elefit.allin/zoonWidth/zoonHeight 转换获取；
3._.createCvEl(type, op, params);
4.Sprict类型还需定义animation；
5.元件颗粒化组织程度受是否整屏动效影响，如与分屏对应的‘prg’元件内含多个真正颗粒化元件；

## 常用utils
### loadsrc(arr, cb, cbPercent)
arr:资源数组;
cb:回调;
cbPercent:资源加载百分比;

```
function loadsrc(arr, cb, cbPercent) {
    var srcs = [];
    for (var i = 0; i < arr.length; i++) {
        srcs = srcs.concat(CONF.RESOURCE[arr[i]]);
    }
    resource.loadEssentialResource(srcs, function() {
        if (cb) {
            cb();
        }
    }, function(percent) {
        if (cbPercent) {
            cbPercent(percent);
        }
    });
}
```

### createCvEl(type, op, params) 
type: Image/Sprite...；
op: 根据适配方案获取的对象x、y、width、height；
params:动画零件凭借op参数往往不够，增加其相关属性进行合并，凭此进行实例化；

```
function createCvEl(type, op, params) {
    var o = {};
    for (var key in op) {
        o[key] = op[key];
    }
    if (params) {
        for (var k in params) {
            o[k] = params[k];
        }
    }
    var el = new yellowjs[type](o);
    el.xDef = op.x;
    el.yDef = op.y;
    return el;
}

```

### elPosLoop(el, xNum, yNum, time) 
```
function elPosLoop(el, xNum, yNum, time) {
    el.to({
        x: el.xDef + xNum,
        y: el.yDef + yNum,
    }, time).to({
        x: el.xDef - xNum,
        y: el.yDef - yNum,
    }, time).exec(function() {
        elPosLoop(el, xNum, yNum, time);
    });
}
```

### rotateLoop(el, deg, time)
```
function rotateLoop(el, deg, time) {
    el.rotation = 0;
    el.to({
        rotation: deg
    }, time).exec(function() {
        rotateLoop(el, deg, time);
    });
}
```

### setOriginCenter(el)

```
function setOriginCenter(el) {
    el.originX = el.width / 2;
    el.originY = el.height / 2;
}
```

