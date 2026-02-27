# Incenter 内心

## 描述

内心是三角形内切圆的圆心，由三角形的三个顶点定义。内心是三角形三条角平分线的交点，到三角形三边的距离相等。

参考：https://mathworld.wolfram.com/Incenter.html

## JessieCode 语法

```js
// 基本语法 - 通过三角形的三个顶点创建内心
I = incenter(p1, p2, p3);

// 带属性创建
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'I'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point | 三角形的第一个顶点 |
| p2 | Point | 三角形的第二个顶点 |
| p3 | Point | 三角形的第三个顶点 |

**注意**：三个点不能共线，否则无法构成三角形。

## 属性

内心继承自 Point，拥有点的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `sizeUnit` | String | 'screen' | 大小单位：'screen' 或 'user' |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | true | 内心通常固定（由三角形决定） |

## 方法

内心继承自 Point，拥有点的所有方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点（内心通常不可移动） |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `X(I)` | 获取内心 I 的 x 坐标 | `X(I)` |
| `Y(I)` | 获取内心 I 的 y 坐标 | `Y(I)` |
| `dist(P, Q)` | 计算两点距离 | `dist(I, A)` |

## 示例

### 1. 创建基本内心

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 创建内心
I = incenter(A, B, C);

// 显示内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'I'
>>;
```

### 2. 内心与内切圆

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(1, 3);

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5
>>;

// 内切圆（需要计算内心到边的距离）
// 使用 incircle 直接创建内切圆
incircle = incircle(A, B, C);
```

### 3. 内心与角平分线

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'I'
>>;

// 角平分线（从顶点到内心并延长）
bisectorA = line(A, I);
bisectorB = line(B, I);
bisectorC = line(C, I);

// 设置样式
bisectorA << strokeColor: 'blue', dash: 1 >>;
bisectorB << strokeColor: 'green', dash: 1 >>;
bisectorC << strokeColor: 'orange', dash: 1 >>;
```

### 4. 动态三角形

```js
// 可移动的顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 内心随三角形变化
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5
>>;

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightgray',
    fillOpacity: 0.3
>>;

// 显示内心坐标
coordText = text(-3, 4, function() {
    return "Incenter: (" + I.X().toFixed(2) + ", " + I.Y().toFixed(2) + ")";
});
```

### 5. 内心的性质演示

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(1, 3);

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'I'
>>;

// 内心到三边的垂足
footAB = perpendicularpoint(I, line(A, B));
footBC = perpendicularpoint(I, line(B, C));
footCA = perpendicularpoint(I, line(C, A));

// 显示垂足
footAB << visible: true, strokeColor: 'blue' >>;
footBC << visible: true, strokeColor: 'blue' >>;
footCA << visible: true, strokeColor: 'blue' >>;

// 内心到三边的距离（内切圆半径）
r1 = segment(I, footAB) << strokeColor: 'gray', dash: 1 >>;
r2 = segment(I, footBC) << strokeColor: 'gray', dash: 1 >>;
r3 = segment(I, footCA) << strokeColor: 'gray', dash: 1 >>;

// 验证距离相等
distText = text(-4, 4, function() {
    d1 = dist(I, footAB);
    d2 = dist(I, footBC);
    d3 = dist(I, footCA);
    return "d1=" + d1.toFixed(3) + ", d2=" + d2.toFixed(3) + ", d3=" + d3.toFixed(3);
});
```

### 6. 内心与外接圆对比

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightgray',
    fillOpacity: 0.3
>>;

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'I'
>>;

// 内切圆
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    dash: 1
>>;

// 外心（需要其他方法创建）
// circumcenter = ...

// 外接圆
// circumcircle = ...
```

### 7. 特殊三角形的内心

```js
// 等边三角形
A1 = point(0, 0);
B1 = point(4, 0);
C1 = point(2, 2 * sqrt(3));
I1 = incenter(A1, B1, C1) <<
    strokeColor: 'red',
    size: 5,
    name: 'I1'
>>;
tri1 = polygon(A1, B1, C1) <<
    fillColor: 'lightblue',
    fillOpacity: 0.3
>>;

// 等腰三角形
A2 = point(6, 0);
B2 = point(10, 0);
C2 = point(8, 4);
I2 = incenter(A2, B2, C2) <<
    strokeColor: 'blue',
    size: 5,
    name: 'I2'
>>;
tri2 = polygon(A2, B2, C2) <<
    fillColor: 'lightgreen',
    fillOpacity: 0.3
>>;

// 直角三角形
A3 = point(0, -5);
B3 = point(3, -5);
C3 = point(0, -2);
I3 = incenter(A3, B3, C3) <<
    strokeColor: 'orange',
    size: 5,
    name: 'I3'
>>;
tri3 = polygon(A3, B3, C3) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.3
>>;
```

### 8. 内心的轨迹

```js
// 固定两个顶点
A = point(-2, 0);
B = point(2, 0);

// 第三个顶点在直线上移动
C = point(0, 3);
path = line(-3, 3, 3, 3);  // y=3 的直线
C_glider = glider(path);

// 内心
I = incenter(A, B, C_glider) <<
    strokeColor: 'red',
    size: 3,
    trace: true  // 开启轨迹
>>;

// 三角形
tri = polygon(A, B, C_glider) <<
    fillColor: 'lightgray',
    fillOpacity: 0.3
>>;
```

## 注意事项

1. **三点不共线**：三个顶点不能共线，否则无法构成三角形
2. **内心位置**：内心始终在三角形内部
3. **角平分线交点**：内心是三角形三条角平分线的交点
4. **等距离性质**：内心到三角形三边的距离相等（等于内切圆半径）
5. **唯一性**：每个三角形有且仅有一个内心

## 相关元素

- [Incircle](./Incircle.md) - 内切圆
- [Bisector](./Bisector.md) - 角平分线
- [Circumcenter](./Circumcenter.md) - 外心
- [Centroid](./Centroid.md) - 重心
- [Orthocenter](./Orthocenter.md) - 垂心
