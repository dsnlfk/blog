---
title: 设计模式
date: 2016-10-08 21:49:52
tags:
---

### 装饰者模式
- 为对象动态加入行为  
- 用于一开始不能确定对象的全部功能时  
- 装饰者模式经常会形成一条长长的装饰链  
- 框架开发中发挥的作用：框架中提供稳定方便移植的功能，个性化功能可以在框架之外动态装饰上去,这可以避免为了让框架有更多的功能,而去使用一些if、else语句预测用户的实际需要。

```javascript
//AOP装饰者函数——污染了原型
Function.prototype.before=function(beforefn){
    var _self=this;
    return function(){
        beforefn.apply(this,arguments);
        return _self.apply(this,arguments);
    }
};
Function.prototype.after=function(afterfn){
    var _self=this;
    return function(){
        var ret=_self.apply(this,arguments);
        afterfn.apply(this,arguments);
        return ret;
    }
};

//AOP装饰者函数——不污染原型
var before=function(fn,beforefn){
    return function(){
        beforefn.apply(this,arguments);
        fn.apply(this,arguments);
    }
}
```