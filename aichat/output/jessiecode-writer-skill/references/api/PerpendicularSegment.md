# PerpendicularSegment 垂线段

## 描述

垂线段是垂直于给定直线并通过一个不在该直线上的点的线段。它是线段（Segment）的一种特殊形式，表示从点到直线的最短距离。

## JessieCode 语法

```js
// 通过直线和点创建垂线段
perpSeg = perpendicularsegment(line, point);

// 带属性创建
perpSeg = perpendicularsegment(l, P) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line | 参考直线（垂线段垂直于该直线） |
| point | Point | 垂线段经过的点（不在直线上） |

## 属性

垂线段继承自 Segment，因此拥有 Segment 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 线段名称 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `L()` | 无 | 获取垂线段长度（点到直线的距离） |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `L(segment)` | 获取线段长度 | `L(perpSeg)` |
| `dist(P, Q)` | 计算两点距离 | `dist(P, foot)` |

## 示例

### 1. 创建基本垂线段

```js
// 参考直线
A = point(0, 2);
B = point(2, 1);
l = line(A, B);

// 外部点
P = point(3, 3);

// 垂线段（从点 P 到直线 l 的最短距离）
perpSeg = perpendicularsegment(l, P);

// 显示距离
distText = text(1, 4, "Distance = " + L(perpSeg));
```

### 2. 点到直线的距离演示

```js
// 创建直线
l = line(point(0, 0), point(4, 2));

// 外部点
P = point(2, 3);

// 垂线段（红色加粗显示）
perpSeg = perpendicularsegment(l, P) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 获取垂足
foot = perpendicularpoint(l, P);

// 标记垂足
F = point(foot) <<
    strokeColor: 'blue',
    fillColor: 'blue',
    size: 4
>>;

// 显示距离值
distText = text(-3, 4, function() {
    return "d = " + L(perpSeg).toFixed(3);
});
```

### 3. 三角形的高

```js
// 三角形顶点
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 三角形
pol = polygon(A, B, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.3
>>;

// 从 C 到 AB 边的高（垂线段）
hC = perpendicularsegment(pol.borders[0], C) <<
    strokeColor: 'red',
    dash: 1
>>;

// 垂足
Hc = perpendicularpoint(pol.borders[0], C);

// 显示高的长度
heightText = text(0, -2, "Height h = " + L(hC));
```

### 4. 动态垂线段

```js
// 可拖动的直线
A = point(-2, 0);
B = point(2, 1);
l = line(A, B);

// 可拖动的点
P = point(1, 2);

// 动态垂线段
perpSeg = perpendicularsegment(l, P) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 垂足
foot = perpendicularpoint(l, P);

// 实时显示距离
distText = text(-3, 3, function() {
    return "Distance: " + L(perpSeg).toFixed(2);
});

// 拖动 A、B 或 P 点时，垂线段长度会实时更新
```

### 5. 点到直线的距离公式演示

```js
// 直线 ax + by + c = 0
// 点 (x₀, y₀) 到直线的距离公式：
// d = |ax₀ + by₀ + c| / √(a² + b²)

// 创建直线（通过两点）
P1 = point(-3, 0);
P2 = point(3, 2);
l = line(P1, P2);

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

### 6. 三角形的三条高

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 三条高（垂线段）
hA = perpendicularsegment(pol.borders[1], A) <<
    strokeColor: 'red', dash: 1 >>;
hB = perpendicularsegment(pol.borders[2], B) <<
    strokeColor: 'green', dash: 1 >>;
hC = perpendicularsegment(pol.borders[0], C) <<
    strokeColor: 'blue', dash: 1 >>;

// 垂心（高的交点）
H = intersection(hA, hB, 0);

// 标记垂心
H = point(H) <<
    strokeColor: 'black',
    fillColor: 'black',
    size: 6,
    name: 'H'
>>;
```

### 7. 垂线段与平行线

```js
// 基础直线
l1 = line(point(-3, 0), point(3, 0));

// 平行线
l2 = parallel(l1, point(0, 2));

// 从 l2 上一点到 l1 的垂线段
P = point(1, 2);
perpSeg = perpendicularsegment(l1, P) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 平行线间的距离处处相等
distText = text(-2, 2.5, "Distance between lines = " + L(perpSeg));
```

### 8. 直角标记

```js
// 直线和外部点
l = line(point(0, 0), point(4, 0));
P = point(2, 3);

// 垂线段
perpSeg = perpendicularsegment(l, P) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 垂足
foot = perpendicularpoint(l, P);

// 标记直角
rightAngle = angle(point(0, 0), foot, P) <<
    radius: 0.5,
    type: 'square',
    strokeColor: 'gray'
>>;
```

### 9. 点到线段的最短距离

```js
// 线段
A = point(-2, 0);
B = point(2, 0);
s = segment(A, B);

// 外部点
P = point(0, 2);

// 垂线段
perpSeg = perpendicularsegment(s, P) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 垂足
foot = perpendicularpoint(s, P);

// 注意：如果垂足不在线段 AB 上，则最短距离是到端点 A 或 B 的距离
```

### 10. 测量点到直线的距离

```js
// 创建可调节的直线
slider = slider(0, 2, 0.1);
A = point(-3, 0);
B = point(3, V(slider));
l = line(A, B);

// 固定点
P = point(0, 3);

// 垂线段
perpSeg = perpendicularsegment(l, P) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 显示距离
distText = text(-3, 4, function() {
    return "d(P, l) = " + L(perpSeg).toFixed(3);
});

// 拖动 slider 改变直线斜率，观察距离变化
```

## 注意事项

1. **最短距离**：垂线段的长度等于点到直线的最短距离
2. **唯一性**：过直线外一点有且仅有一条垂线段到该直线
3. **垂足位置**：垂足是垂线与直线的交点
4. **与 perpendicular 的区别**：`perpendicular` 创建的是无限延伸的垂线，而 `perpendicularsegment` 创建的是有限长度的垂线段
5. **长度获取**：使用 `L(perpSeg)` 或 `perpSeg.L()` 获取垂线段长度

## 相关元素

- [Perpendicular](./Perpendicular.md) - 垂线（无限延伸）
- [Segment](./Segment.md) - 线段
- [Line](./Line.md) - 直线
- [PerpendicularPoint](./PerpendicularPoint.md) - 垂足
- [Parallel](./Parallel.md) - 平行线
- [Distance](./Measurement.md) - 距离测量
