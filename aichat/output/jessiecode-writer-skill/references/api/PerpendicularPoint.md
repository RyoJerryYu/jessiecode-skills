# PerpendicularPoint 垂足点

## 描述

垂足点是点在直线上的正交投影（垂直投影）得到的点。该点位于直线上，且连接原点与垂足点的线段与直线垂直。

垂足点继承自 `Point` 元素。

## JessieCode 语法

```js
// 基本语法 - 创建点在直线上的垂足
P = perpendicularpoint(point, line);

// 带属性创建
P = perpendicularpoint(A, l) <<
    strokeColor: 'red',
    fillColor: 'yellow',
    size: 5,
    withLabel: true,
    name: 'P'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point | Point | 要进行投影的点 |
| line | Line | 目标直线（点将投影到此直线上） |

## 属性

垂足点继承自 `Point` 元素，因此支持所有点的属性。

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
| `fixed` | Boolean | true | 是否固定（垂足点默认固定，不可拖动） |
| `showInfobox` | Boolean | true | 是否显示信息框 |

## 方法

垂足点继承自 `Point` 元素，因此支持所有点的方法。

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点（垂足点通常不可移动） |
| `glide(line)` | line: Line | 使点在直线上滑动 |
| `free()` | 无 | 释放点 |

## 示例

### 1. 创建基本垂足点

```js
// 创建两个点定义一条直线
p1 = point(0.0, 4.0);
p2 = point(6.0, 1.0);

// 创建直线
l1 = line(p1, p2);

// 创建要投影的点
p3 = point(3.0, 3.0);

// 创建 p3 在直线 l1 上的垂足点
pp1 = perpendicularpoint(p3, l1);
```

### 2. 设置垂足点的样式

```js
// 创建直线
A = point(0, 0);
B = point(5, 3);
l = line(A, B);

// 创建要投影的点
P = point(2, 4) <<
    strokeColor: 'blue',
    fillColor: 'lightblue',
    size: 6
>>;

// 创建红色的垂足点
foot = perpendicularpoint(P, l) <<
    strokeColor: 'red',
    fillColor: 'yellow',
    size: 8,
    face: 'square',
    withLabel: true,
    name: 'F'
>>;
```

### 3. 动态垂足点

```js
// 创建可拖动的点
A = point(0, 0);
B = point(4, 0);
l = line(A, B);

// 创建可拖动的投影源点
P = point(2, 3);

// 创建垂足点（随 P 的移动而自动更新）
foot = perpendicularpoint(P, l);

// 创建连接 P 和 foot 的垂线
perpLine = line(P, foot) <<
    dash: 1,
    strokeColor: 'gray'
>>;
```

### 4. 三角形的垂足

```js
// 三角形顶点
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 三角形边
a = line(B, C);
b = line(A, C);
c = line(A, B);

// 从各顶点到对边的垂足
Ha = perpendicularpoint(A, a);
Hb = perpendicularpoint(B, b);
Hc = perpendicularpoint(C, c);

// 标记垂足
Ha = point(Ha) << strokeColor: 'red', size: 4 >>;
Hb = point(Hb) << strokeColor: 'red', size: 4 >>;
Hc = point(Hc) << strokeColor: 'red', size: 4 >>;
```

### 5. 垂心（三角形三条高的交点）

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 三角形边
a = line(B, C);
b = line(A, C);
c = line(A, B);

// 从各顶点到对边的垂线
hA = perpendicular(a, A);
hB = perpendicular(b, B);
hC = perpendicular(c, C);

// 垂心（高的交点）
H = intersection(hA, hB, 0);
H = point(H) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 6,
    withLabel: true,
    name: 'H'
>>;
```

### 6. 抛物线的顶点

```js
// 焦点
F = point(0, 1);

// 准线
A = point(-3, -1);
B = point(3, -1);
directrix = line(A, B);

// 创建抛物线
parabola = parabola(F, directrix) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 顶点是焦点到准线垂线段的中点
V = perpendicularpoint(F, directrix);
V = midpoint(F, V);
V = point(V) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 5,
    withLabel: true,
    name: 'V'
>>;
```

### 7. 点到直线的距离

```js
// 直线
l = line(point(0, 0), point(4, 0));

// 外部点
P = point(2, 3);

// 垂足
foot = perpendicularpoint(P, l);

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

### 8. 垂直关系标记

```js
// 参考直线
A = point(0, 2);
B = point(6, 1);
l = line(A, B);

// 外部点
P = point(3, 3);

// 垂足
foot = perpendicularpoint(P, l);

// 垂线
perp = line(P, foot) <<
    strokeColor: 'red',
    dash: 1
>>;

// 标记直角
rightAngle = angle(A, foot, P) <<
    radius: 0.5,
    type: 'square',
    strokeColor: 'gray'
>>;
```

### 9. 多个投影点

```js
// 创建坐标轴
xAxis = line(0, 0, 1, 0) << withLabel: true, name: 'x' >>;
yAxis = line(0, 0, 0, 1) << withLabel: true, name: 'y' >>;

// 创建任意点
P = point(3, 2);

// 创建在 x 轴和 y 轴上的垂足
projX = perpendicularpoint(P, xAxis) <<
    strokeColor: 'blue',
    face: 'plus'
>>;
projY = perpendicularpoint(P, yAxis) <<
    strokeColor: 'green',
    face: 'plus'
>>;

// 创建投影辅助线
lineX = line(P, projX) << dash: 1, strokeColor: 'gray' >>;
lineY = line(P, projY) << dash: 1, strokeColor: 'gray' >>;
```

### 10. 垂足轨迹

```js
// 固定直线
l = line(point(-4, 0), point(4, 0));

// 圆上的动点
c = circle(point(0, 2), 2);
P = glider(c);

// 垂足
foot = perpendicularpoint(P, l);

// 垂足会在直线 l 上移动
// 可以创建轨迹来可视化
```

## 注意事项

1. **垂足位置**：垂足点始终位于目标直线上
2. **垂直关系**：连接原点与垂足点的线段与目标直线垂直
3. **固定属性**：垂足点默认是固定的（`fixed: true`），不能直接拖动
4. **动态更新**：当源点或目标直线移动时，垂足点会自动更新位置
5. **继承特性**：垂足点继承自 Point 元素，支持点的所有属性和方法
6. **创建方式**：使用 `perpendicularpoint(point, line)` 语法创建，参数顺序为（点，直线）
7. **唯一性**：过直线外一点有且仅有一个垂足
8. **最短距离**：点到直线的最短距离是垂线段的长度

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Perpendicular](./Perpendicular.md) - 垂线
- [Orthogonalprojection](./Orthogonalprojection.md) - 正交投影点（与垂足点功能相同）
- [Segment](./Segment.md) - 线段（可创建垂线段）
- [Intersection](./Intersection.md) - 交点
