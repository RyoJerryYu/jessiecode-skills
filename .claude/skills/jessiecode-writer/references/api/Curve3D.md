# Curve3D 3D 曲线

## 描述

3D 曲线可以通过参数映射或离散数据集定义。一般来说，3D 曲线是从 R 到 R³ 的映射，t 映射到 (x(t), y(t), z(t))。图像在区间 [a, b] 上绘制。

*定义于：* [curve3d.js](./src/src_3d_curve3d.js.md)

*继承自：* [Curve](./Curve.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   ↳ **[JXG.Curve](./JXG.Curve.md)**
      ↳ **[Curve](./Curve.md)**
         ↳ **Curve3D**

## JessieCode 语法

```js
// 参数曲线（三个函数）
curve = curve3d(fx, fy, fz, range);

// 参数曲线（一个向量函数）
curve = curve3d(f, range);

// 数据点曲线
curve = curve3d(xArray, yArray, zArray);

// 在 3D 视图中创建
view = view3d(...);
curve = view.create('curve3d', [fx, fy, fz, [tMin, tMax]]);

// 带属性创建
curve = view.create('curve3d', [
    function(t) { return cos(t); },
    function(t) { return sin(t); },
    function(t) { return t; },
    [0, 2*PI]
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

### 方式一：三个函数

| 参数 | 类型 | 描述 |
|------|------|------|
| `fx` | Function | x 坐标函数 `x(t)` |
| `fy` | Function | y 坐标函数 `y(t)` |
| `fz` | Function | z 坐标函数 `z(t)` |
| `range` | Array/Function | 参数范围 `[tMin, tMax]` 或返回数组的函数 |

### 方式二：一个向量函数

| 参数 | 类型 | 描述 |
|------|------|------|
| `f` | Function | 向量函数，返回 `[x, y, z]` 数组 |
| `range` | Array/Function | 参数范围 `[tMin, tMax]` |

### 方式三：三个数组

| 参数 | 类型 | 描述 |
|------|------|------|
| `xArray` | Array | x 坐标数组 |
| `yArray` | Array | y 坐标数组 |
| `zArray` | Array | z 坐标数组 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 曲线名称 |
| `firstArrow` | Boolean/Object | false | 起点箭头 |
| `lastArrow` | Boolean/Object | false | 终点箭头 |

## 示例

### 1. 基本 3D 螺旋线

```js
// 创建 3D 视图
view = view3d(
    [[-6, -3], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 螺旋线（圆柱螺旋）
helix = view.create('curve3d', [
    function(t) { return cos(t); },
    function(t) { return sin(t); },
    function(t) { return t / PI; },
    [0, 4*PI]
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 2. 简化写法

```js
// 使用函数引用简化
helix = view.create('curve3d', [cos, sin, function(t) { return t / PI; }, [0, 4*PI]]) <<
    strokeColor: 'blue'
>>;
```

### 3. 向量函数形式

```js
// 使用向量函数
helix = view.create('curve3d', [
    function(t) { return [cos(t), sin(t), t / PI]; },
    [0, 4*PI]
]) <<
    strokeColor: 'blue'
>>;
```

### 4. 圆锥螺旋线

```js
// 圆锥螺旋线（半径随高度增加）
conicalHelix = view.create('curve3d', [
    function(t) { return t * cos(t); },
    function(t) { return t * sin(t); },
    function(t) { return t; },
    [0, 4*PI]
]) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 5. 环面螺旋线（圆环螺旋）

```js
// 环面螺旋线
torusKnot = view.create('curve3d', [
    function(t) {
        return (2 + 0.5 * cos(3*t)) * cos(2*t);
    },
    function(t) {
        return (2 + 0.5 * cos(3*t)) * sin(2*t);
    },
    function(t) {
        return 0.5 * sin(3*t);
    },
    [0, 2*PI]
]) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;
```

### 6. 3D 利萨茹曲线

```js
// 3D 利萨茹曲线
lissajous3D = view.create('curve3d', [
    function(t) { return sin(3*t); },
    function(t) { return sin(4*t); },
    function(t) { return sin(5*t); },
    [0, 2*PI]
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 7. 数据点 3D 曲线

```js
// 数据点
xData = [0, 1, 2, 3, 4, 5];
yData = [0, 1, 4, 9, 16, 25];
zData = [0, 1, 8, 27, 64, 125];

// 连接数据点的 3D 曲线
dataCurve = view.create('curve3d', [xData, yData, zData]) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;

// 显示数据点
for (i = 0; i < 6; i = i + 1) {
    view.create('point3d', [xData[i], yData[i], zData[i]]) <<
        size: 4,
        strokeColor: 'red'
    >>;
}
```

### 8. 动态 3D 曲线

```js
// 创建滑块
tMax = slider(0.1, 4*PI, 0.1);

// 长度可变的螺旋线
dynamicHelix = view.create('curve3d', [
    cos,
    sin,
    function(t) { return t / PI; },
    function() { return [0, V(tMax)]; }
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 9. 带箭头的 3D 曲线

```js
// 有向 3D 曲线
directedCurve = view.create('curve3d', [
    function(t) { return t; },
    function(t) { return t * t; },
    function(t) { return t * t * t; },
    [-2, 2]
]) <<
    lastArrow: << type: 7, size: 10 >>,
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 10. 虚线 3D 曲线

```js
// 虚线 3D 曲线（用于辅助线）
dashedCurve = view.create('curve3d', [
    function(t) { return cos(t); },
    function(t) { return sin(t); },
    function(t) { return 0; },
    [0, 2*PI]
]) <<
    strokeColor: 'gray',
    dash: 1,
    strokeWidth: 1
>>;
```

### 11. 参数曲线组合

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 圆（z=0 平面）
circle1 = view.create('curve3d', [
    function(t) { return 2 * cos(t); },
    function(t) { return 2 * sin(t); },
    function(t) { return 0; },
    [0, 2*PI]
]) <<
    strokeColor: 'red'
>>;

// 圆（z=2 平面）
circle2 = view.create('curve3d', [
    function(t) { return 2 * cos(t); },
    function(t) { return 2 * sin(t); },
    function(t) { return 2; },
    [0, 2*PI]
]) <<
    strokeColor: 'blue'
>>;

// 连接两个圆的螺旋线
helix = view.create('curve3d', [
    function(t) { return 2 * cos(t); },
    function(t) { return 2 * sin(t); },
    function(t) { return t / (2*PI) * 2; },
    [0, 2*PI]
]) <<
    strokeColor: 'green'
>>;
```

### 12. 8 字形曲线（双纽线）

```js
// 8 字形曲线
figureEight = view.create('curve3d', [
    function(t) { return sin(t); },
    function(t) { return sin(t) * cos(t); },
    function(t) { return 0; },
    [0, 2*PI]
]) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;
```

### 13. 球面螺旋线

```js
// 球面螺旋线（在球面上缠绕）
sphericalHelix = view.create('curve3d', [
    function(t) {
        return cos(t) * cos(0.1*t);
    },
    function(t) {
        return sin(t) * cos(0.1*t);
    },
    function(t) {
        return sin(0.1*t);
    },
    [0, 20*PI]
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 14. 曲线动画

```js
// 相位滑块
phase = slider(0, 2*PI, 0.1);

// 旋转的椭圆
rotatingEllipse = view.create('curve3d', [
    function(t) {
        var p = V(phase);
        return 2 * cos(t) * cos(p) - sin(t) * sin(p);
    },
    function(t) {
        var p = V(phase);
        return 2 * cos(t) * sin(p) + sin(t) * cos(p);
    },
    function(t) { return 0; },
    [0, 2*PI]
]) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

## 注意事项

1. **参数范围**：必须指定参数范围 `[tMin, tMax]`，默认不会自动设置
2. **数组曲线**：使用数组时，曲线会依次连接各数据点
3. **函数形式**：可以使用三个独立函数或一个返回数组的向量函数
4. **平滑度**：复杂曲线可能需要更多的采样点
5. **箭头**：使用 `firstArrow` 和 `lastArrow` 可以添加方向指示
6. **性能**：长曲线或复杂函数可能影响渲染性能

## 相关元素

- [Curve](./Curve.md) - 2D 曲线
- [Line3D](./Line3D.md) - 3D 直线
- [Circle3D](./Circle3D.md) - 3D 圆
- [Point3D](./Point3D.md) - 3D 点
