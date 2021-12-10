# 场景(scene)

右手笛卡尔坐标系

# 相机(Camera)

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