# Intersection 交点

## 描述

交点是两个一维元素（如直线、圆、曲线等）相交的点。当两个元素有多个交点时，可以使用索引参数选择具体的交点。

## JessieCode 语法

```js
// 基本语法 - 两条直线的交点
P = intersection(line1, line2, 0);

// 直线与圆的交点
P = intersection(line, circle, 0);

// 两个圆的交点
P = intersection(circle1, circle2, 0);

// 带属性创建
P = intersection(l1, l2, 0) <<
    strokeColor: 'red',
    size: 5
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| el1 | Line/Circle/Curve/Polygon | 第一个元素 |
| el2 | Line/Circle/Curve/Polygon | 第二个元素 |
| i | Number/Function | 交点索引（0 或 1） |

### 可相交的元素组合

| 元素 1 | 元素 2 | 说明 |
|--------|--------|------|
| Line | Line | 两条直线（1 个交点） |
| Line | Circle | 直线与圆（0-2 个交点） |
| Circle | Circle | 两个圆（0-2 个交点） |
| Line | Curve | 直线与曲线 |
| Circle | Curve | 圆与曲线 |
| Curve | Curve | 两条曲线 |
| Polygon | Polygon | 两个多边形 |

### 交点索引

| 索引 | 描述 |
|------|------|
| 0 | 使用正平方根（第一个交点） |
| 1 | 使用负平方根（第二个交点） |

## 属性

交点继承自 Point，因此拥有 Point 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `visible` | Boolean | true | 是否可见 |

## 方法

交点继承自 Point，拥有 Point 的所有方法：

| 方法 | 描述 |
|------|------|
| `X()` | 获取 x 坐标 |
| `Y()` | 获取 y 坐标 |
| `move(dx, dy)` | 移动点 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `X(P)` | 获取点 P 的 x 坐标 | `X(P)` |
| `Y(P)` | 获取点 P 的 y 坐标 | `Y(P)` |

## 示例

### 1. 两条直线的交点

```js
// 创建两条直线
A = point(0, 0);
B = point(4, 4);
l1 = line(A, B);

C = point(0, 4);
D = point(4, 0);
l2 = line(C, D);

// 创建交点
P = intersection(l1, l2, 0);

// 标记交点
P = intersection(l1, l2, 0) <<
    strokeColor: 'red',
    size: 6,
    face: '[]'
>>;
```

### 2. 直线与圆的交点

```js
// 创建圆
O = point(0, 0);
c = circle(O, 2);

// 创建直线
A = point(-3, 1);
B = point(3, 1);
l = line(A, B);

// 创建两个交点
P1 = intersection(l, c, 0);
P2 = intersection(l, c, 1);

// 隐藏无交点时的点
// 当直线与圆不相交时，交点可能不可见
```

### 3. 两个圆的交点

```js
// 创建两个圆
c1 = circle(point(-1, 0), 2);
c2 = circle(point(1, 0), 2);

// 创建交点
P1 = intersection(c1, c2, 0);  // 上方交点
P2 = intersection(c1, c2, 1);  // 下方交点

// 创建连心线
l = line(c1.center, c2.center);

// 创建公共弦
chord = segment(P1, P2);
```

### 4. 垂直平分线构造

```js
// 线段
A = point(-2, -1);
B = point(2, 1);
s = segment(A, B);

// 以 A、B 为圆心创建两个圆
c1 = circle(A, L(s));
c2 = circle(B, L(s));

// 交点
P1 = intersection(c1, c2, 0);
P2 = intersection(c1, c2, 1);

// 垂直平分线
perpBisector = line(P1, P2);

// 中点
M = intersection(perpBisector, s, 0);
```

### 5. 三角形的高

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 从 C 到 AB 的垂线
altC = perpendicular(pol.borders[0], C);

// 垂足（交点）
Hc = intersection(altC, pol.borders[0], 0);

// 高线段
heightC = segment(C, Hc);
```

### 6. 动态交点

```js
// 可移动的点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 直线
l1 = line(A, B);
l2 = line(B, C);

// 交点（随点移动而更新）
P = intersection(l1, l2, 0);

// 显示交点坐标
coordText = text(0, 4, function() {
    return "P = (" + P.X().toFixed(2) + ", " + P.Y().toFixed(2) + ")";
});
```

### 7. 圆的切线交点

```js
// 圆
O = point(0, 0);
c = circle(O, 2);

// 外部点
P = point(4, 0);

// 以 OP 中点为圆心创建圆
M = midpoint(O, P);
c2 = circle(M, O);  // 经过 O 和 P

// 交点是切点
T1 = intersection(c, c2, 0);
T2 = intersection(c, c2, 1);

// 切线
t1 = line(P, T1);
t2 = line(P, T2);
```

### 8. 根轴（等幂轴）

```js
// 两个不相交的圆
c1 = circle(point(-2, 0), 1.5);
c2 = circle(point(2, 0), 1.5);

// 创建第三个辅助圆
c3 = circle(point(0, 2), 2);

// 交点
P1 = intersection(c1, c3, 0);
P2 = intersection(c2, c3, 0);

// 根轴可以通过这些交点的连线构造
```

### 9. 曲线交点

```js
// 抛物线
f = functiongraph(function(x) { return x * x; }, -2, 2);

// 直线
l = line(point(-2, 2), point(2, 2));

// 交点
P1 = intersection(f, l, 0);
P2 = intersection(f, l, 1);
```

### 10. 多边形交点

```js
// 两个多边形
pol1 = polygon(point(-1, -1), point(1, -1), point(0, 1));
pol2 = polygon(point(-1, 0), point(1, 0), point(0, 2));

// 边的交点
// 需要指定具体的边
P = intersection(pol1.borders[0], pol2.borders[0], 0);
```

## 注意事项

1. **索引选择**：当有两个交点时，使用索引 0 或 1 选择
2. **无交点情况**：当元素不相交时，交点可能不可见或报错
3. **数值精度**：对于接近相切的情况，数值精度可能影响结果
4. **性能**：复杂曲线的交点计算可能较慢
5. **alwaysIntersect**：某些情况下（如线段），可设置 `alwaysIntersect: true` 将线段视为直线处理

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Circle](./Circle.md) - 圆
- [Midpoint](./Midpoint.md) - 中点
- [PerpendicularPoint](./PerpendicularPoint.md) - 垂足
