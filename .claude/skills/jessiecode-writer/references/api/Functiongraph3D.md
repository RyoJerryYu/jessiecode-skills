# Functiongraph3D 3D 函数图像

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 函数图像可视化映射 (x, y) → f(x, y)。该图像是一个 [Curve3D](./Curve3D.md) 元素。

*定义于：* [surface3d.js](./src/src_3d_surface3d.js.md)
*继承自* [ParametricSurface3D](./ParametricSurface3D.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Curve](./JXG.Curve.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **[Curve](./Curve.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **[ParametricSurface3D](./ParametricSurface3D.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **Functiongraph3D**

## JessieCode 语法

```js
// Functiongraph3D 元素没有直接构造函数
// 需要在 3D 视图中创建

// 基本语法（在 3D 视图中）
// view.create('functiongraph3d', [F, rangeX, rangeY], options)

// F(x,y) 是返回数字的函数（或 JessieCode 字符串）
// rangeX 是包含 x 范围上下界的数组
// rangeY 是包含 y 范围上下界的数组
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| F | Function/String | 函数 F(x, y)，返回一个数字（或 JessieCode 字符串） |
| rangeX | Array | 包含 x 范围下界和上界的数组 |
| rangeY | Array | 包含 y 范围下界和上界的数组 |

## 构造函数

| 构造函数属性 | 构造函数名称和描述 |
| --- | --- |
| | **[Functiongraph3D](./Functiongraph3D.md#constructor)** | 一个 3D 函数图像由函数 *F: R² → R* 定义 |

### 说明

此元素没有直接构造函数。要创建此元素的实例，必须调用 [JXG.Board#create](./JXG.Board.md#create)，类型为 "functiongraph3d"。

可能的父数组组合：

| 参数 | 描述 |
|------|------|
| **F** | F(x,y) 是返回数字的函数（或 JessieCode 字符串） |
| **rangeX** | 包含 x 范围下界和上界的数组 |
| **rangeY** | 包含 y 范围下界和上界的数组 |

### 抛出异常

- 抛出：{Exception} 如果无法使用给定的父对象构造元素，则抛出异常

## 属性

Functiongraph3D 继承自 ParametricSurface3D，因此拥有 ParametricSurface3D 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeWidth` | Number | 1 | 线宽 |
| `stepsU` | Number | 20 | U 方向的步数 |
| `stepsV` | Number | 20 | V 方向的步数 |
| `fillColor` | String | '#aaaaaa' | 填充颜色 |
| `fillOpacity` | Number | 0.5 | 填充透明度 |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `visible` | Boolean | true | 是否可见 |

## 示例

### 1. 基本 3D 函数图像

```js
// 定义范围
box = [-5, 5];

// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [box, box, box]
) <<
    xPlaneRear: {visible: false},
    yPlaneRear: {visible: false}
>>;

// 函数 F(x, y) = sin(x * y / 4)
F = (x, y) => sin(x * y / 4);

// 创建 3D 函数图像
surface = view.create('functiongraph3d', [
    F,
    box,  // x 范围
    box   // y 范围
]) <<
    strokeWidth: 0.5,
    stepsU: 70,
    stepsV: 70
>>;
```

### 2. 二次曲面

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    xPlaneRear: {visible: false},
    yPlaneRear: {visible: false}
>>;

// 抛物面 z = x² + y²
paraboloid = view.create('functiongraph3d', [
    (x, y) => x * x + y * y,
    [-3, 3],
    [-3, 3]
]) <<
    fillColor: 'blue',
    fillOpacity: 0.7,
    strokeColor: 'white'
>>;
```

### 3. 正弦波曲面

```js
// 创建 3D 视图
view = view3d(
    [-8, -4], [10, 10],
    [[-2 * PI, 2 * PI], [-2 * PI, 2 * PI], [-2, 2]]
);

// 正弦波 z = sin(x) * cos(y)
wave = view.create('functiongraph3d', [
    (x, y) => sin(x) * cos(y),
    [-2 * PI, 2 * PI],
    [-2 * PI, 2 * PI]
]) <<
    fillColor: 'cyan',
    fillOpacity: 0.8,
    stepsU: 50,
    stepsV: 50
>>;
```

### 4. 动态范围的函数图像

```js
// 创建滑块控制范围
s = slider([-5, 4], [4, 4], [1, 5, 10]) << name: '范围' >>;

// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-6, 6], [-6, 6], [-6, 6]]
);

// 动态范围的函数
surface = view.create('functiongraph3d', [
    (x, y) => sin(x * x + y * y),
    () => [-V(s), V(s)],  // x 范围由滑块控制
    () => [-V(s), V(s)]   // y 范围由滑块控制
]) <<
    fillColor: 'orange',
    fillOpacity: 0.6
>>;
```

### 5. 马鞍面（双曲抛物面）

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]
) <<
    xPlaneRear: {visible: true, fillOpacity: 0.1},
    yPlaneRear: {visible: true, fillOpacity: 0.1},
    zPlaneRear: {visible: true, fillOpacity: 0.1}
>>;

// 马鞍面 z = x² - y²
saddle = view.create('functiongraph3d', [
    (x, y) => x * x - y * y,
    [-3, 3],
    [-3, 3]
]) <<
    fillColor: 'purple',
    fillOpacity: 0.7,
    strokeColor: 'black',
    strokeWidth: 0.5
>>;
```

### 6. 高斯函数（钟形曲面）

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [0, 1.5]]
);

// 高斯函数 z = e^(-(x² + y²))
gaussian = view.create('functiongraph3d', [
    (x, y) => exp(-(x * x + y * y)),
    [-3, 3],
    [-3, 3]
]) <<
    fillColor: 'green',
    fillOpacity: 0.8,
    stepsU: 60,
    stepsV: 60
>>;
```

### 7. 多个函数图像比较

```js
// 创建 3D 视图
view = view3d(
    [-8, -4], [10, 10],
    [[-3, 3], [-3, 3], [-3, 3]]
);

// 不同的二次函数
f1 = view.create('functiongraph3d', [
    (x, y) => x * x + y * y,
    [-2, 2], [-2, 2]
]) << fillColor: 'red', fillOpacity: 0.5 >>;

f2 = view.create('functiongraph3d', [
    (x, y) => 2 * (x * x + y * y),
    [-2, 2], [-2, 2]
]) << fillColor: 'blue', fillOpacity: 0.5 >>;

f3 = view.create('functiongraph3d', [
    (x, y) => 0.5 * (x * x + y * y),
    [-2, 2], [-2, 2]
]) << fillColor: 'green', fillOpacity: 0.5 >>;
```

### 8. 参数化函数族

```js
// 创建滑块控制参数
n = slider([1, 4], [4, 4], [1, 1, 10]) << name: 'n' >>;

// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-2, 2], [-2, 2], [-2, 2]]
);

// 函数族 z = (x² + y²)^n
family = view.create('functiongraph3d', [
    (x, y) => pow(x * x + y * y, V(n) / 2),
    [-2, 2],
    [-2, 2]
]) <<
    fillColor: 'yellow',
    fillOpacity: 0.7
>>;
```

### 9. 三角函数组合

```js
// 创建 3D 视图
view = view3d(
    [-8, -4], [10, 10],
    [[-PI, PI], [-PI, PI], [-2, 2]]
);

// z = sin(x) + sin(y)
sum = view.create('functiongraph3d', [
    (x, y) => sin(x) + sin(y),
    [-PI, PI],
    [-PI, PI]
]) <<
    fillColor: 'pink',
    fillOpacity: 0.8,
    strokeColor: 'red'
>>;
```

### 10. 带网格线的曲面

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-3, 3], [-3, 3], [-2, 2]]
);

// 创建函数图像，增加网格线密度
surface = view.create('functiongraph3d', [
    (x, y) => sin(x) * sin(y),
    [-3, 3],
    [-3, 3]
]) <<
    strokeWidth: 1,
    stepsU: 40,  // U 方向更多步数
    stepsV: 40,  // V 方向更多步数
    fillColor: 'lightblue',
    fillOpacity: 0.6
>>;
```

## 注意事项

1. **函数定义**：函数 F 必须接受两个参数 (x, y) 并返回一个数字
2. **动态范围**：范围可以是函数，用于创建动画效果
3. **性能**：增加 stepsU 和 stepsV 会使曲面更平滑，但会增加计算量
4. **透明度**：使用 fillOpacity 可以调整曲面的透明度，便于观察内部结构
5. **3D 视图**：Functiongraph3D 必须在 3D 视图（view3d）中创建
6. **不连续点**：对于有不连续点的函数，需要小心处理

## 相关元素

- [Curve3D](./Curve3D.md) - 3D 曲线
- [ParametricSurface3D](./ParametricSurface3D.md) - 参数化曲面（父类）
- [View3D](./View3D.md) - 3D 视图
- [Slider](./Slider.md) - 滑块（控制参数）
