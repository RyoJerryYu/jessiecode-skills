# Perpendicular 垂线

<!-- USAGE_FREQUENCY: core -->

## 描述

垂线是通过一个不在给定直线上的点，且与该直线垂直的直线（或线段）。

## JessieCode 语法

```js
// 通过直线和点创建垂线
perp = perpendicular(line, point);

// 带属性创建
perp = perpendicular(l, P) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line | 参考直线 |
| point | Point | 垂线经过的点 |

## 属性

垂线继承自 Line/Segment，因此拥有 Line 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |

## 相关函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `perpendicular(line, point)` | 创建垂线 | `perpendicular(l, P)` |
| `perpendicularpoint(line, point)` | 创建垂足点 | `perpendicularpoint(l, P)` |
| `perpendicularsegment(line, point)` | 创建垂线段 | `perpendicularsegment(l, P)` |

## 示例

### 1. 创建基本垂线

```js
// 参考直线
A = point(0, 2);
B = point(2, 1);
l = line(A, B);

// 外部点
P = point(3, 3);

// 垂线
perp1 = perpendicular(l, P);

// 垂足
foot = perpendicularpoint(l, P);
```

### 2. 三角形的高

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 从 C 到 AB 的高
hC = perpendicular(pol.borders[0], C);

// 垂足
Hc = perpendicularpoint(pol.borders[0], C);

// 高线段
heightC = segment(C, Hc) <<
    strokeColor: 'red',
    dash: 1
>>;
```

### 3. 垂线段（点到直线的距离）

```js
// 直线
l = line(point(0, 0), point(4, 2));

// 外部点
P = point(2, 3);

// 垂线段（最短距离）
perpSeg = perpendicularsegment(l, P) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 显示距离
distText = text(1, 4, function() {
    return "Distance = " + L(perpSeg).toFixed(2);
});
```

### 4. 动态垂线

```js
// 可移动的直线
A = point(-2, 0);
B = point(2, 1);
l = line(A, B);

// 可移动的点
P = point(1, 2);

// 动态垂线
perp = perpendicular(l, P);

// 垂足
foot = perpendicularpoint(l, P);

// 显示垂直关系
rightAngle = angle(A, foot, P) <<
    radius: 0.5,
    type: 'square'
>>;
```

### 5. 三角形垂心

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 三条高
hA = perpendicular(pol.borders[1], A);
hB = perpendicular(pol.borders[2], B);
hC = perpendicular(pol.borders[0], C);

// 垂心（高的交点）
H = intersection(hA, hB, 0);

// 标记垂心
H = point(H) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 6,
    name: 'H'
>>;
```

### 6. 点到直线的距离公式演示

```js
// 直线 ax + by + c = 0
// 点 (x₀, y₀)
// 距离 d = |ax₀ + by₀ + c| / √(a² + b²)

// 创建直线
A = point(-3, 0);
B = point(3, 2);
l = line(A, B);

// 外部点
P = point(0, 3);

// 垂线段
perpSeg = perpendicularsegment(l, P) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 显示距离
distText = text(-3, 4, function() {
    return "d = " + L(perpSeg).toFixed(3);
});
```

### 7. 垂直平分线

```js
// 线段
A = point(-2, -1);
B = point(2, 1);
s = segment(A, B);

// 中点
M = midpoint(A, B);

// 垂直平分线
perpBisector = perpendicular(s, M);

// 验证：垂直平分线上的点到 A 和 B 等距
P = glider(perpBisector);
text(0, 3, function() {
    return "PA = " + dist(P, A).toFixed(2) + ", PB = " + dist(P, B).toFixed(2);
});
```

### 8. 矩形构造

```js
// 基础线段
A = point(-2, -1);
B = point(2, -1);
base = segment(A, B);

// 在 A 点的垂线
perpA = perpendicular(base, A);

// 在 B 点的垂线
perpB = perpendicular(base, B);

// 矩形高度
h = 3;

// 圆确定高度
circleA = circle(A, h);
circleB = circle(B, h);

// 交点
D = intersection(perpA, circleA, 0);
C = intersection(perpB, circleB, 0);

// 完成矩形
rect = polygon(A, B, C, D) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;
```

### 9. 垂足轨迹

```js
// 固定直线
l = line(point(-4, 0), point(4, 0));

// 圆上的动点
c = circle(point(0, 2), 2);
P = glider(c);

// 垂足
foot = perpendicularpoint(l, P);

// 垂足的轨迹
// 垂足会在直线 l 上移动
```

### 10. 点到线段的最短距离

```js
// 线段
A = point(-2, 0);
B = point(2, 0);
s = segment(A, B);

// 外部点
P = point(0, 2);

// 垂足
foot = perpendicularpoint(s, P);

// 检查垂足是否在线段上
// 如果垂足在线段外，最短距离是到端点的距离

// 垂线段
perpSeg = perpendicularsegment(s, P) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

## 注意事项

1. **唯一性**：过直线外一点有且仅有一条垂线
2. **最短距离**：点到直线的最短距离是垂线段的长度
3. **垂足**：垂线与直线的交点称为垂足
4. **垂直符号**：可以使用 `Angle` 元素的 `type: 'square'` 来标记直角

## 相关元素

- [Line](./Line.md) - 直线
- [Segment](./Segment.md) - 线段
- [Parallel](./Parallel.md) - 平行线
- [Intersection](./Intersection.md) - 交点
- [Angle](./Angle.md) - 角度（用于标记直角）
