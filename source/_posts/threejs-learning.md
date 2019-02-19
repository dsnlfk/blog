---
title: threejs手册
date: 2016-11-03 11:27:21
tags:
---

### requestAnimationFrame()与setInterval()比较
- setInterval不考虑浏览器发生的事情，假如正在浏览其他网页，setInterval依旧会工作
- setInterval没有跟显示器重画同步，这可能导致较高cpu使用率

### threejs的世界组成
- 舞台：var scene = new THREE.Scene();
- 渲染器：var renderer = new THREE.WebGLRenderer();
- 相机：var camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 10000);

## Scene

### THREE.Scene()
- Scene.Add(); //在场景中添加物体
- Scene.Remove(); //在场景中删除物体
- Scene.children; // 获取场景中所有子对象的列表
- Scene.getChildByName(); //利用name属性，获取场景中某个特定物体
- Scene.traverse(cb); //传入作用于舞台子元素的函数
- scene.overrideMaterial = new THREE.MeshLambertMaterial({ color: 0xffffff }); //强制舞台材质覆盖

### 舞台雾化效果
- scene.fog = new THREE.Fog(0xffffff, 0.015, 100);//雾化  
  scene.fog = new THREE.FogExp2(0xffffff, 0.015);//雾化浓度
  
### 添加阴影
- 确保使用能对光源起作用的材质：（Threejs里有两种材质可以对光源产生反应）MeshLambertMaterial 、MeshPhongMaterial,且不要设置网格（{ wireframe: true }）；
- 渲染器设置：renderer.shadowMapEnabled = true;
- 物体设置：plane.receiveShadow = true;  
  cube.castShadow = true;  
  sphere.castShadow = true;
- 光源设置：spotLight.castShadow = true;

## Threejs提供的光源

- AmbientLight 环境光  
- PointLight 点光源，空间中一点，朝所有方向发射光线；  
- SpotLight 聚光灯光源，聚光效果，类似台灯、吊灯、手电筒等；  
- DirectionalLight 方向光，也称作无限光，从光源发出的光线可看作是平行的；  
- HemisphereLight 半球光，特殊光源，可用来创造更自然的室外光线，模拟反光面和光线微弱的天空；  
- AreaLight 面光源，可指定散发光线的平面，而不是空间中一个点；  
- LensFlare 镜头眩光,这不是一种光源，可为场景中的光源添加眩光效果；  

### PointLight属性

```javascript
var pointLight = new THREE.PointLight(0xccffcc);
- color  
- intensity 强度  
- distance 距离  
- position 位置  
- visible 是否可见  
```

### SpotLight聚光灯指定空间某个点的方法
```javascript
var target = new THREE.Object3D();
target.position = new THREE.Vector3(5,0,0);
spotlight.target = target;
```
