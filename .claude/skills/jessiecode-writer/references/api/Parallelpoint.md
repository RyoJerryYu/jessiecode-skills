# Parallelpoint 平行点

## 描述

给定三个点，平行点是指使得这四个点构成平行四边形的第四个点。

*定义于：* [composition.js](./src/src_element_composition.js.md)
*继承自：* [JXG.Point](./JXG.Point.md)

## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md), JXG.GeometryElement**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Point](./JXG.Point.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **Parallelpoint**

## JessieCode 语法

```js
// 通过三个点创建平行点（构成平行四边形的第四个顶点）
P = parallelpoint(A, B, C);

// 通过一条直线和一个点创建平行点
P = parallelpoint(line, point);

// 带属性创建
P = parallelpoint(A, B, C) <<
    strokeColor: 'red',
    fillColor: 'blue',
    withLabel: true,
    name: 'P'
>>;
```

## 参数

### 方式一：三个点（构成平行四边形）

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point | 第一个点（平行四边形的起点） |
| p2 | Point | 第二个点（定义向量 v = p2 - p1） |
| p3 | Point | 第三个点（平行点 = p3 + v） |

**说明**：取欧几里得向量 v = p2 - p1，平行点由 p4 = p3 + v 确定

### 方式二：一条直线和一个点

| 参数 | 类型 | 描述 |
|------|------|------|
| l | Line | 参考直线 |
| p | Point | 起始点 |

**说明**：结果点与点 p 一起确定一条平行于直线 l 的直线

## 属性

平行点继承自 [Point](./Point.md)，因此具有点的所有属性。

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小（像素或用户坐标） |
| `sizeUnit` | String | 'screen' | 大小单位：'screen' 或 'user' |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `id` | String | 自动生成 | 元素的唯一 ID |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | false | 是否固定（不可拖动） |
| `showInfobox` | Boolean | true | 是否显示信息框 |

## 方法

平行点继承自 [Point](./Point.md)，因此具有点的所有方法。

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点 |
| `glide(line)` | line: Line | 使点在直线上滑动 |
| `free()` | 无 | 释放点 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `X(P)` | 获取点 P 的 x 坐标 | `X(P)` |
| `Y(P)` | 获取点 P 的 y 坐标 | `Y(P)` |
| `dist(P, Q)` | 计算两点距离 | `dist(A, P)` |

## 示例

### 1. 创建基本平行点

```js
// 创建三个点
A = point(0.0, 2.0);
B = point(2.0, 1.0);
C = point(3.0, 3.0);

// 创建平行点 D，使得 ABCD 构成平行四边形
D = parallelpoint(A, B, C);
```

### 2. 设置平行点样式

```js
// 创建基础点
A = point(0, 0) << withLabel: true, name: 'A' >>;
B = point(3, 1) << withLabel: true, name: 'B' >>;
C = point(2, 3) << withLabel: true, name: 'C' >>;

// 创建带样式的平行点
D = parallelpoint(A, B, C) <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 6,
    withLabel: true,
    name: 'D'
>>;

// 连接四个点形成平行四边形
AB = segment(A, B);
BC = segment(B, C);
CD = segment(C, D);
DA = segment(D, A);
```

### 3. 动态平行四边形

```js
// 创建可拖动的点
A = point(0, 0) << withLabel: true, name: 'A' >>;
B = point(3, 0) << withLabel: true, name: 'B' >>;
C = point(1, 2) << withLabel: true, name: 'C' >>;

// 平行点会随 A、B、C 的移动而自动更新
D = parallelpoint(A, B, C) <<
    withLabel: true,
    name: 'D'
>>;

// 连接成平行四边形
l1 = segment(A, B);
l2 = segment(B, C);
l3 = segment(C, D);
l4 = segment(D, A);
```

### 4. 通过直线和点创建平行点

```js
// 创建一条直线
l = line(point(0, 0), point(4, 2));

// 创建一个点
P = point(1, 3);

// 创建平行点，使得新点与 P 的连线平行于直线 l
Q = parallelpoint(l, P);
```

### 5. 多个平行点构成复杂图形

```js
// 创建基础三角形
A = point(0, 0) << withLabel: true, name: 'A' >>;
B = point(4, 0) << withLabel: true, name: 'B' >>;
C = point(2, 3) << withLabel: true, name: 'C' >>;

// 创建平行点完成平行四边形
D = parallelpoint(A, B, C) << withLabel: true, name: 'D' >>;

// 创建对角线
AC = segment(A, C);
BD = segment(B, D);

// 创建对角线交点（中点）
M = intersection(AC, BD, 0) <<
    withLabel: true,
    name: 'M'
>>;
```

### 6. 平行点与向量

```js
// 创建向量起点和终点
O = point(0, 0) << withLabel: true, name: 'O' >>;
V = point(2, 1) << withLabel: true, name: 'V' >>;

// 创建向量的箭头
arrow = arrow(O, V) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 在别处复制这个向量
P = point(3, 3) << withLabel: true, name: 'P' >>;
Q = parallelpoint(O, V, P) << withLabel: true, name: 'Q' >>;

// 复制的向量
arrow2 = arrow(P, Q) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 7. 平行点动画

```js
// 创建滑块控制角度
angle = slider(0, 2*PI, 0.01) <<
    name: '角度',
    withLabel: true
>>;

// 固定点
A = point(0, 0) << fixed: true, withLabel: true, name: 'A' >>;

// 旋转的点
B = point(function() { return 3 * cos(V(angle)); },
          function() { return 3 * sin(V(angle)); })
    << withLabel: true, name: 'B' >>;

// 另一个固定点
C = point(4, 2) << fixed: true, withLabel: true, name: 'C' >>;

// 平行点随 B 旋转
D = parallelpoint(A, B, C) << withLabel: true, name: 'D' >>;

// 连接成平行四边形
segment(A, B);
segment(B, C);
segment(C, D);
segment(D, A);
```

## 注意事项

1. **点的顺序很重要**：`parallelpoint(A, B, C)` 创建的点 D 使得向量 AB = 向量 CD
2. **动态更新**：当父点移动时，平行点会自动更新位置
3. **构造方式**：在 JessieCode 中使用 `parallelpoint` 函数创建，底层调用 `JXG.Board#create` 类型 "parallelpoint"
4. **继承属性**：平行点继承自 Point，因此可以使用点的所有属性和方法
5. **几何意义**：平行点常用于构造平行四边形、复制向量等几何操作

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Segment](./Segment.md) - 线段
- [Arrow](./Arrow.md) - 箭头
- [Midpoint](./Midpoint.md) - 中点
- [Intersection](./Intersection.md) - 交点
- [Translate](./Translate.md) - 平移点
