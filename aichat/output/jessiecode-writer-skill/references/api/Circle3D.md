# Circle3D 3D 圆

## 描述

3D 空间中的圆由圆心、法向量和半径定义。圆上所有点到圆心的距离等于半径，且位于由法向量定义的平面内。

*定义于：* [circle3d.js](./src/src_3d_circle3d.js.md)

*继承自：* [JXG.Circle3D](./JXG.Circle3D.md)

## 继承关系

**[JXG.Curve3D](./JXG.Curve3D.md), JXG.GeometryElement**
   ↳ **[JXG.Circle3D](./JXG.Circle3D.md)**
      ↳ **Circle3D**

## JessieCode 语法

```js
// 通过圆心、法向量和半径创建
circle = circle3d(center, normal, radius);

// 在 3D 视图中创建
view = view3d(...);
circle = view.create('circle3d', [center, normal, radius]);

// 带属性创建
circle = view.create('circle3d', [
    [0, 0, 0],      // 圆心
    [0, 0, 1],      // 法向量
    2               // 半径
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

| 参数组合 | 类型 | 描述 |
|----------|------|------|
| `center`, `normal`, `radius` | Point3D/Array/Function, Array/Function, Number/Function | 圆心、法向量和半径 |

### 参数说明

| 参数 | 类型 | 描述 |
|------|------|------|
| `center` | Point3D/Array/Function | 圆心坐标，可以是 Point3D 对象、长度为 3 的数组 `[x, y, z]` 或返回数组的函数 |
| `normal` | Array/Function | 法向量，长度为 4 的齐次坐标数组 `[0, x, y, z]` 或返回数组的函数 |
| `radius` | Number/Function | 半径（数字）或返回数字的函数。如果为 NaN，圆不显示。负数取绝对值 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 圆名称 |
| `center` | Object | - | 圆心属性设置 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.0 | 填充透明度 |

### 圆心属性

```js
// 显示圆心
circle = view.create('circle3d', [center, normal, radius]) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5
    >>
>>;
```

## 示例

### 1. 创建基本 3D 圆

```js
// 创建 3D 视图
view = view3d(
    [[-6, -3], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 在 xy 平面创建圆（法向量为 z 轴方向）
circle = view.create('circle3d', [
    [0, 0, 0],      // 圆心在原点
    [0, 0, 1],      // 法向量沿 z 轴
    2               // 半径为 2
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 2. 三个坐标平面上的圆

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center',
    xPlaneRear: << fillOpacity: 0.1 >>,
    yPlaneRear: << fillOpacity: 0.1 >>,
    zPlaneRear: << fillOpacity: 0.1 >>
>>;

// xy 平面上的圆（红色）
circleXY = view.create('circle3d', [
    [0, 0, 0],
    [0, 0, 1],      // z 轴法向量
    2
]) <<
    strokeColor: 'red',
    name: 'xy-plane'
>>;

// yz 平面上的圆（绿色）
circleYZ = view.create('circle3d', [
    [0, 0, 0],
    [1, 0, 0],      // x 轴法向量
    2
]) <<
    strokeColor: 'green',
    name: 'yz-plane'
>>;

// xz 平面上的圆（蓝色）
circleXZ = view.create('circle3d', [
    [0, 0, 0],
    [0, 1, 0],      // y 轴法向量
    2
]) <<
    strokeColor: 'blue',
    name: 'xz-plane'
>>;
```

### 3. 带圆心的 3D 圆

```js
// 创建带可见圆心的圆
circle = view.create('circle3d', [
    [1, 2, 3],
    [0, 0, 1],
    1.5
]) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    center: <<
        visible: true,
        name: 'C',
        strokeColor: 'red',
        fillColor: 'black',
        size: 5
    >>,
    withLabel: true,
    name: 'Circle'
>>;
```

### 4. 虚线 3D 圆

```js
// 虚线圆（用于辅助圆）
dashedCircle = view.create('circle3d', [
    [0, 0, 0],
    [0, 0, 1],
    2
]) <<
    strokeColor: 'gray',
    dash: 1,
    strokeWidth: 1
>>;
```

### 5. 动态半径的圆

```js
// 创建滑块
r = slider(0.5, 4, 0.1);

// 半径可变的圆
dynamicCircle = view.create('circle3d', [
    [0, 0, 0],
    [0, 0, 1],
    function() { return V(r); }
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 6. 偏移圆心的圆

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 圆心在 (2, 0, 0) 的圆
circle1 = view.create('circle3d', [
    [2, 0, 0],
    [0, 0, 1],
    1.5
]) <<
    strokeColor: 'red'
>>;

// 圆心在 (0, 3, 0) 的圆
circle2 = view.create('circle3d', [
    [0, 3, 0],
    [0, 0, 1],
    1.5
]) <<
    strokeColor: 'blue'
>>;

// 圆心在 (0, 0, 2) 的圆
circle3 = view.create('circle3d', [
    [0, 0, 2],
    [0, 1, 0],
    1.5
]) <<
    strokeColor: 'green'
>>;
```

### 7. 填充 3D 圆（圆盘）

```js
// 创建半透明填充圆
filledCircle = view.create('circle3d', [
    [0, 0, 0],
    [0, 0, 1],
    2
]) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    fillColor: 'lightblue',
    fillOpacity: 0.3
>>;
```

### 8. 同心 3D 圆

```js
// 多个同心圆
circle1 = view.create('circle3d', [
    [0, 0, 0],
    [0, 0, 1],
    1
]) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

circle2 = view.create('circle3d', [
    [0, 0, 0],
    [0, 0, 1],
    2
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

circle3 = view.create('circle3d', [
    [0, 0, 0],
    [0, 0, 1],
    3
]) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;
```

### 9. 与 3D 点组合

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 创建圆心和圆周上的点
center = view.create('point3d', [0, 0, 0]) <<
    name: 'C',
    size: 5
>>;

pointOnCircle = view.create('point3d', [2, 0, 0]) <<
    name: 'P',
    size: 4
>>;

// 使用动态半径（两点间距离）
circle = view.create('circle3d', [
    function() { return center.X(); },
    function() { return center.Y(); },
    function() { return center.Z(); },
    [0, 0, 1],
    function() {
        // 计算圆心和圆周上点的距离
        var dx = pointOnCircle.X() - center.X();
        var dy = pointOnCircle.Y() - center.Y();
        var dz = pointOnCircle.Z() - center.Z();
        return Math.sqrt(dx*dx + dy*dy + dz*dz);
    }
]) <<
    strokeColor: 'blue'
>>;
```

### 10. 倾斜平面上的圆

```js
// 法向量为 [1, 1, 1] 的倾斜平面上的圆
tiltedCircle = view.create('circle3d', [
    [0, 0, 0],
    [1, 1, 1],      // 倾斜法向量
    2
]) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;

// 添加法向量可视化
normalLine = view.create('line3d', [
    [0, 0, 0],
    [1, 1, 1]
]) <<
    strokeColor: 'gray',
    dash: 1,
    lastArrow: true
>>;
```

## 注意事项

1. **法向量**：法向量定义圆所在平面的方向。例如，`[0, 0, 1]` 表示 xy 平面
2. **半径取绝对值**：如果半径为负数，会自动取绝对值
3. **NaN 半径**：当半径为 NaN 时，圆不显示
4. **齐次坐标**：法向量可以使用齐次坐标 `[0, x, y, z]`
5. **动态圆**：半径可以是函数，用于创建动画或交互式圆
6. **圆心属性**：通过 `center` 属性可以控制圆心的显示和样式

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Curve3D](./Curve3D.md) - 3D 曲线
- [Line3D](./Line3D.md) - 3D 直线
- [Circle](./Circle.md) - 2D 圆
- [Arc](./Arc.md) - 圆弧
