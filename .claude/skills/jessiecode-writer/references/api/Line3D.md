# Line3D 3D 直线

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 直线由两个点定义，或由一个点和一个方向向量定义。

*定义于：* [linspace3d.js](./src/src_3d_linspace3d.js.md)

*继承自：* [JXG.GeometryElement3D](./JXG.GeometryElement3D.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   ↳ **[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)**
      ↳ **Line3D**

## JessieCode 语法

```js
// 通过两个点创建直线
line = line3d(point1, point2);

// 通过点、方向向量和范围创建
line = line3d(point, direction, range);

// 在 3D 视图中创建
view = view3d(...);
line = view.create('line3d', [point1, point2]);

// 带属性创建
line = view.create('line3d', [
    [1, 2, 3],
    [4, 5, 6]
]) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    straightFirst: true,
    straightLast: true
>>;
```

## 参数

### 方式一：两个点

| 参数 | 类型 | 描述 |
|------|------|------|
| `point1` | Point3D/Array/Function | 第一个点，可以是 Point3D 对象、长度为 3 的数组或返回数组的函数 |
| `point2` | Point3D/Array/Function | 第二个点，可以是 Point3D 对象、长度为 3 的数组或返回数组的函数 |

### 方式二：点、方向、范围

| 参数 | 类型 | 描述 |
|------|------|------|
| `point` | Point3D/Array/Function | 直线上的点 |
| `direction` | Array/Function | 方向向量，长度为 3 的数组或返回数组的函数 |
| `range` | Array/Function | 范围 `[r1, r2]`，可以是数字或函数。使用 `[-Infinity, Infinity]` 表示无限直线 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 直线名称 |
| `straightFirst` | Boolean | false | 是否在第一个点方向无限延伸 |
| `straightLast` | Boolean | false | 是否在第二个点方向无限延伸 |
| `point1` | Object | - | 第一个点的属性设置 |
| `point2` | Object | - | 第二个点的属性设置 |
| `point` | Object | - | 定义点的属性设置（点 + 方向方式） |
| `lastArrow` | Boolean/Object | false | 是否在终点显示箭头 |
| `firstArrow` | Boolean/Object | false | 是否在起点显示箭头 |

### 定义点属性

```js
// 显示定义点
line = view.create('line3d', [point1, point2]) <<
    point1: <<
        visible: true,
        strokeColor: 'red',
        size: 5,
        name: 'A'
    >>,
    point2: <<
        visible: true,
        strokeColor: 'blue',
        size: 5,
        name: 'B'
    >>
>>;
```

## 示例

### 1. 创建基本 3D 直线

```js
// 创建 3D 视图
view = view3d(
    [[-6, -3], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 通过两个点创建直线
line1 = view.create('line3d', [
    [1, 3, 3],
    [-3, -3, -3]
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 2. 显示定义点

```js
// 显示定义直线的两个点
line = view.create('line3d', [
    [1, 2, 2],
    [-2, -1, -1]
]) <<
    point1: <<
        visible: true,
        name: 'A',
        size: 5,
        strokeColor: 'red'
    >>,
    point2: <<
        visible: true,
        name: 'B',
        size: 5,
        strokeColor: 'blue'
    >>
>>;
```

### 3. 无限延伸的直线

```js
// 有限线段（默认）
segment = view.create('line3d', [A, B]);

// 无限延伸的直线
infiniteLine = view.create('line3d', [A, B]) <<
    straightFirst: true,
    straightLast: true
>>;

// 射线（从 A 向 B 方向延伸）
ray = view.create('line3d', [A, B]) <<
    straightFirst: false,
    straightLast: true
>>;
```

### 4. 通过点、方向、范围创建

```js
// 点 A
A = view.create('point3d', [1, 2, 2]) << name: 'A' >>;

// 通过点、方向向量、范围创建直线
line = view.create('line3d', [
    A,
    [0, 0, 1],        // z 轴方向
    [-2, 4]           // 范围
]) <<
    strokeColor: 'blue'
>>;
```

### 5. 使用 3D 点创建直线

```js
view = view3d(
    [[-6, -3], [8, 8]],
    [[-3, 3], [-3, 3], [-3, 3]]
) <<
    axesPosition: 'center'
>>;

// 创建两个 3D 点
A = view.create('point3d', [0, 0, 0]) <<
    name: 'A',
    size: 5
>>;

B = view.create('point3d', [2, 1, 1]) <<
    name: 'B',
    size: 5
>>;

// 通过两个点创建直线（可拖动）
line1 = view.create('line3d', [A, B]) <<
    fixed: false,
    straightFirst: true,
    straightLast: true,
    dash: 2
>>;
```

### 6. 与现有直线组合

```js
view = view3d(
    [[-6, -3], [8, 8]],
    [[-3, 3], [-3, 3], [-3, 3]]
) <<
    depthOrder: << enabled: true >>,
    projection: 'parallel'
>>;

// 第一条直线
A = view.create('point3d', [-2, 0, 1]) << size: 2 >>;
B = view.create('point3d', [-2, 0, 2]) << size: 2 >>;
line1 = view.create('line3d', [A, B]) <<
    strokeColor: 'blue',
    straightFirst: true,
    straightLast: true
>>;

// 通过点和平行于另一条直线创建
C = view.create('point3d', [2, 0, 1]) << size: 2 >>;
line2 = view.create('line3d', [C, line1, [-Infinity, Infinity]]) <<
    strokeColor: 'red'
>>;
```

### 7. 虚线 3D 直线

```js
// 虚线（用于辅助线）
dashedLine = view.create('line3d', [
    [0, 0, 0],
    [3, 3, 3]
]) <<
    strokeColor: 'gray',
    dash: 1,
    strokeWidth: 1
>>;

// 点线
dottedLine = view.create('line3d', [
    [0, 0, 0],
    [3, 0, 0]
]) <<
    strokeColor: 'orange',
    dash: 2
>>;
```

### 8. 带箭头的 3D 直线（向量）

```js
// 向量（末端箭头）
vector = view.create('line3d', [
    [0, 0, 0],
    [2, 2, 2]
]) <<
    lastArrow: << type: 7, size: 10 >>,
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 两端箭头
biVector = view.create('line3d', [
    [-2, -2, -2],
    [2, 2, 2]
]) <<
    firstArrow: << type: 7 >>,
    lastArrow: << type: 7 >>,
    strokeColor: 'blue'
>>;
```

### 9. 动态 3D 直线

```js
// 创建滑块
a = slider(0, 3, 0.1);

// 一个点随滑块移动
P = view.create('point3d', [
    function() { return V(a); },
    0,
    0
]) << name: 'P' >>;

// 固定点
Q = view.create('point3d', [0, 1, 0]) << name: 'Q' >>;

// 直线随 P 点移动
dynamicLine = view.create('line3d', [P, Q]) <<
    strokeColor: 'blue'
>>;
```

### 10. 坐标轴平行直线

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 平行于 x 轴的直线
lineX = view.create('line3d', [
    [0, 2, 2],
    [1, 2, 2]      // 方向向量
]) <<
    strokeColor: 'red',
    straightFirst: true,
    straightLast: true
>>;

// 平行于 y 轴的直线
lineY = view.create('line3d', [
    [2, 0, 2],
    [2, 1, 2]
]) <<
    strokeColor: 'green',
    straightFirst: true,
    straightLast: true
>>;

// 平行于 z 轴的直线
lineZ = view.create('line3d', [
    [2, 2, 0],
    [2, 2, 1]
]) <<
    strokeColor: 'blue',
    straightFirst: true,
    straightLast: true
>>;
```

### 11. 空间对角线

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-3, 3], [-3, 3], [-3, 3]]
) <<
    axesPosition: 'center',
    xPlaneRear: << fillOpacity: 0.1 >>,
    yPlaneRear: << fillOpacity: 0.1 >>,
    zPlaneRear: << fillOpacity: 0.1 >>
>>;

// 立方体的空间对角线
diagonal1 = view.create('line3d', [
    [-3, -3, -3],
    [3, 3, 3]
]) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

diagonal2 = view.create('line3d', [
    [-3, -3, 3],
    [3, 3, -3]
]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 12. 直线相交

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 创建两条相交直线
line1 = view.create('line3d', [
    [-3, 0, 0],
    [3, 0, 0]
]) <<
    strokeColor: 'red',
    straightFirst: true,
    straightLast: true
>>;

line2 = view.create('line3d', [
    [0, -3, 0],
    [0, 3, 0]
]) <<
    strokeColor: 'blue',
    straightFirst: true,
    straightLast: true
>>;

// 创建交点
intersection = view.create('point3d', [0, 0, 0]) <<
    name: 'O',
    size: 5,
    strokeColor: 'black'
>>;
```

## 注意事项

1. **无限延伸**：使用 `straightFirst: true` 和 `straightLast: true` 创建无限延伸的直线
2. **射线**：只设置 `straightLast: true` 创建从 point1 向 point2 方向的射线
3. **线段**：默认情况下（`straightFirst: false, straightLast: false`）创建线段
4. **方向向量**：使用点 + 方向方式时，直线从 `point + r1*direction` 到 `point + r2*direction`
5. **深度排序**：设置 `depthOrder: << enabled: true >>` 正确处理 3D 直线的遮挡关系
6. **定义点**：通过 `point1` 和 `point2` 属性可以控制定义点的显示和样式

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Curve3D](./Curve3D.md) - 3D 曲线
- [Axis3D](./Axis3D.md) - 3D 单轴
- [Arrow](./Arrow.md) - 箭头
- [Line](./Line.md) - 2D 直线
