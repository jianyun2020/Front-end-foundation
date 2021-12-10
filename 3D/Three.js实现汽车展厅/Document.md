# 场景(scene)

右手笛卡尔坐标系

# 相机(camera)

- `PerspectiveCamera`：透视相机，符合物理世界近大远小
- `OrthographicCamera`：正交相机，远近大小一样

```js
/**
 * fov: 视场角
 * aspect: 视场宽高比（一般用 画布宽/画布高 即可）
 * near: 能看多近
 * far: 能看多远
*/
PerspectiveCamera(fov: Number, aspect: Number, near: Number, far: Number)

```

# 渲染器(renderer)

将`camera`在`scene`里看到的内容渲染/绘制到画布上

# 几何体(geometry)

3D世界里的所有物体都是点组成面，面组成几何体。

另外我们一般说的3d模型就是一个或多个几何体，只是有的3d模型文件里除了包含几何体还可以包含一些额外的信息，比如贴图，材质等...需要在读取模型文件时解析出来

# 灯光(light)

3d引擎在没有手动创建光的情况下会默认有个环境光，不然你什么都看不到。常见的灯光有以下几种类型:

- *AmbientLight*：环境光，没有方向全局打亮，不会产生明暗
- *DirectionLight*：平行光，参考日光
- *PointLight*：点光源，参考灯泡
- *SpotLight*：聚光灯，参考舞台聚光灯

# 贴图(texture)

想象一下你手里有一个立方体，你用一张A4纸包裹上立方体的所有面，并在上面画画。你画的内容就是贴图。有一些类型的贴图会和光照发生反应。

# 材质(material)

延续贴图里的想象，你用白卡纸画画，还是用油纸画画，呈现出来的质感是不同的对不对，这就是材质！下面五个球的颜色都是一样的，而材质从左至右分别是：

- *MeshBasicMaterial*: 基础材质，不受光照影响
- *MeshStandardMaterial*：PBR标准材质
- *MeshPhongMaterial*：高光材质，适用于陶瓷，烤漆类质感
- *MeshToonMaterial*：卡通材质，俗称三渲二
- *MeshStandardMaterial*：PBR标准材质模拟金属反射

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ac95cf7bdfb847f6ac2dda4dcf0fd63d~tplv-k3u1fbpfcp-watermark.awebp)

