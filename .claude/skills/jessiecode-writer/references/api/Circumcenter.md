# Circumcenter 外心

<!-- USAGE_FREQUENCY: common -->

## 描述

外心是三角形外接圆的圆心。它由三个点确定，这三个点都在以该外心为圆心的圆上。外心是三角形三条边的垂直平分线的交点。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建外心
center = circumcenter(A, B, C);

// 带属性创建
center = circumcenter(A, B, C) <<
    strokeColor: 'red',
    fillColor: 'black',
    size: 5,
    withLabel: true,
    name: 'O'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| A | Point | 第一个点 |
| B | Point | 第二个点 |
| C | Point | 第三个点 |

**注意**：三个点不能共线，否则无法确定唯一的外接圆。

## 属性

外心继承自 Point，因此具有所有点的属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | true | 是否固定（外心默认固定） |

## 方法

外心继承自 Point，因此具有所有点的方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点（外心通常不可移动） |

## 示例

### 1. 创建基本外心

```js
// 创建三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 创建外心
O = circumcenter(A, B, C);

// 显示外心
O = circumcenter(A, B, C) <<
    withLabel: true,
    name: 'O',
    strokeColor: 'red',
    fillColor: 'black',
    size: 5
>>;
```

### 2. 外心与外接圆

```js
// 三角形顶点
A = point(1, 1);
B = point(5, 1);
C = point(3, 4);

// 外心
O = circumcenter(A, B, C) <<
    strokeColor: 'red',
    fillColor: 'black',
    size: 5,
    withLabel: true,
    name: 'O'
>>;

// 外接圆（使用外心和圆周上的点）
circumcircle = circle(O, A) <<
    strokeColor: 'blue',
    dash: 1
>>;
```

### 3. 动态外心

```js
// 可移动的三角形顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);  // 可以拖动

// 外心随顶点移动而更新
O = circumcenter(A, B, C) <<
    withLabel: true,
    name: 'O',
    strokeColor: 'red'
>>;

// 外接圆
c = circle(O, A);

// 显示外心坐标
text(-3, 4, function() {
    return "O = (" + O.X().toFixed(2) + ", " + O.Y().toFixed(2) + ")";
});
```

### 4. 不同类型三角形的外心

```js
// 锐角三角形 - 外心在三角形内部
A1 = point(-6, 2);
B1 = point(-2, 2);
C1 = point(-4, 5);
O1 = circumcenter(A1, B1, C1) << strokeColor: 'blue' >>;

// 直角三角形 - 外心在斜边中点
A2 = point(-1, 0);
B2 = point(3, 0);
C2 = point(-1, 3);
O2 = circumcenter(A2, B2, C2) << strokeColor: 'green' >>;

// 钝角三角形 - 外心在三角形外部
A3 = point(2, 0);
B3 = point(6, 0);
C3 = point(3, 1);
O3 = circumcenter(A3, B3, C3) << strokeColor: 'red' >>;
```

### 5. 外心与垂直平分线

```js
// 三角形顶点
A = point(1, 1);
B = point(5, 1);
C = point(3, 4);

// 三边中点
Mab = midpoint(A, B);
Mbc = midpoint(B, C);
Mca = midpoint(C, A);

// 垂直平分线
perpAB = perpendicular(Mab, line(A, B));
perpBC = perpendicular(Mbc, line(B, C));
perpCA = perpendicular(Mca, line(C, A));

// 三条垂直平分线交于外心
O = circumcenter(A, B, C) <<
    strokeColor: 'red',
    fillColor: 'black',
    size: 6,
    withLabel: true,
    name: 'O'
>>;

// 设置垂直平分线样式
perpAB << dash: 1, strokeColor: 'gray' >>;
perpBC << dash: 1, strokeColor: 'gray' >>;
perpCA << dash: 1, strokeColor: 'gray' >>;
```

### 6. 外心到顶点的距离

```js
// 三角形顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 外心
O = circumcenter(A, B, C);

// 外接圆半径（外心到任一顶点的距离）
R = circle(O, A);

// 显示半径
text(1, 4, function() {
    r = dist(O, A);
    return "Circumradius R = " + r.toFixed(3);
});

// 验证：OA = OB = OC
text(1, 3.5, function() {
    return "OA = " + dist(O, A).toFixed(3);
});
text(1, 3, function() {
    return "OB = " + dist(O, B).toFixed(3);
});
text(1, 2.5, function() {
    return "OC = " + dist(O, C).toFixed(3);
});
```

### 7. 外心与欧拉线

```js
// 三角形顶点
A = point(0, 0);
B = point(5, 0);
C = point(2, 4);

// 外心
O = circumcenter(A, B, C) <<
    strokeColor: 'red',
    withLabel: true,
    name: 'O'
>>;

// 重心（中线交点）
G = centroid(A, B, C) <<
    strokeColor: 'blue',
    withLabel: true,
    name: 'G'
>>;

// 垂心（高线交点）
H = orthocenter(A, B, C) <<
    strokeColor: 'green',
    withLabel: true,
    name: 'H'
>>;

// 欧拉线：O、G、H 三点共线
eulerLine = line(O, H) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;

// 验证 G 在欧拉线上
```

### 8. 外心的轨迹

```js
// 固定两点
A = point(-2, 0);
B = point(2, 0);

// C 点在圆上运动
centerC = point(0, 3);
radiusC = 2;
c = circle(centerC, radiusC);
C = glider(c);  // C 在圆上滑动

// 外心随 C 点移动
O = circumcenter(A, B, C);

// 创建外心轨迹
trace(O, true);
```

## 注意事项

1. **三点不共线**：三个点不能在同一直线上，否则无法确定唯一的外接圆
2. **外心位置**：
   - 锐角三角形：外心在三角形内部
   - 直角三角形：外心在斜边中点
   - 钝角三角形：外心在三角形外部
3. **垂直平分线交点**：外心是三角形三条边的垂直平分线的交点
4. **等距离性质**：外心到三角形三个顶点的距离相等
5. **固定点**：外心默认为固定点，不能直接拖动

## 相关元素

- [Circumcircle](./Circumcircle.md) - 外接圆
- [CircumcircleArc](./CircumcircleArc.md) - 外接圆弧
- [CircumcircleSector](./CircumcircleSector.md) - 外接圆扇形
- [Midpoint](./Midpoint.md) - 中点
- [Perpendicular](./Perpendicular.md) - 垂线
- [Centroid](./Centroid.md) - 重心
- [Orthocenter](./Orthocenter.md) - 垂心
