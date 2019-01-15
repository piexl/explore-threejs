# 3D世界-Three.js的探究与实践

## 项目需求

在开发[育空网站](http://yukon.projects.dragontrail.cn/)时我们需要在页面内使用四面体，还要增加一些交互和操作，因此使用了3D类库Three.js也经历多种波折才实现了我们最终的效果。

## 3D世界的初认识

[Three.js官方文档](https://threejs.org/docs/index.html)使用起来对于初学者来说并不优化，通过下面连个Three.js的先关资料对它的理解能更块些

![Three.js 文档结构](./imgs/threejs_components.jpg)
Three.js 文档结构：[图片来自](https://teakki.com/p/58a3ef1bf0d40775548c908f)

![Three.js 核心对象结构和基本的渲染流程](./imgs/three_render.jpg)
Three.js 核心对象结构和基本的渲染流程：[图片来自](http://ushiroad.com/3j/)

**右手坐标系**
Three.js 采用的是的右手坐标系，坐标系的原点在画布中心（canvas.width / 2, canvas.height / 2）。我们可以通过 Three.js 提供的 THREE.AxisHelper() 辅助方法将坐标系可视化。RGB颜色分别代表 XYZ 轴，如下图

![右手坐标系](./imgs/coordinate.jpg)

右手坐标系：[图片来自](http://ushiroad.com/3j/)

## 创建一个场景

**准备html,引入Three.js**

``` html

<!DOCTYPE html>
<html>
<head>
    <meta charset=utf-8>
    <title>My first three.js app</title>
    <style>
        body { margin: 0; }
        canvas { width: 100%; height: 100% }
    </style>
</head>
<body>
    <script src="https://cdn.bootcss.com/three.js/r83/three.js"></script>
</body>
</html>
```

**创建场景**

``` js
var scene = new THREE.Scene();
var camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

var renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
```

上面的代码构建了scene, camera 和 renderer。Three.js的架构支持多种camera，这里使用最常见的远景相机（PerspectiveCamera），也就是类似于人眼观察的方式。第一个属性75设置的是视角（field of view）。
第二个属性设置的是相机拍摄面的长宽比（aspect ratio）。我们几乎总是会使用元素的宽除以高，否则会出现挤压变形。
接下来的2个属性是近裁剪面（near clipping plane） 和 远裁剪面（far clipping plane）。下面这张图可以帮助你理解：

![摄像机](./imgs/camera_modle.png)

**创建立方体**

```js
var geometry = new THREE.BoxGeometry( 1, 1, 1 );
var material = new THREE.MeshBasicMaterial( { color: 0x2185D0 } );
var cube = new THREE.Mesh( geometry, material );
scene.add( cube );
```

**渲染场景**

*在大多数屏幕上，刷新率一般是60次/秒*

``` js
function animate() {
    requestAnimationFrame( animate );
    renderer.render( scene, camera );
}
animate();
```

**使立方体动起来**

将下列代码添加到animate()函数中renderer.render调用的上方：

``` js
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
```

最终时间效果如下：
<iframe src="https://codepen.io/piexl-the-selector/embed/maaQrK" width="100%" height="300px" frameborder="0" scrolling="no"> </iframe>

## 3D世界的深层了解

## 四面的实现尝试一(直接引入模型法)

**准备素材**

+ 四面体模型
+ 材质贴图

**实现方法**




## 四面的实现尝试二

## 四面的实现尝试三

## 参考链接

threejs官方文档: [https://threejs.org/docs/index.html](https://threejs.org/docs/index.html) (现在可切换中文文档了)
threejs教程:[https://teakki.com/p/58a3ef1bf0d40775548c908f](https://teakki.com/p/58a3ef1bf0d40775548c908f)
Three.js 现学现卖: [https://aotu.io/notes/2017/08/28/getting-started-with-threejs/](https://aotu.io/notes/2017/08/28/getting-started-with-threejs/)
threejs+tweenjs实现3D粒子模型切换: [https://juejin.im/post/5b8d47cce51d4538bf55e3a8](https://juejin.im/post/5b8d47cce51d4538bf55e3a8)
