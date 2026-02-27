# Parallel 平行线

## 描述

平行线是通过一个给定点，且与给定直线平行的直线。

## JessieCode 语法

```js
// 通过直线和点创建平行线
par = parallel(line, point);

// 通过两点和另一点创建平行线
par = parallel(point1, point2, point);

// 带属性创建
par = parallel(l, P) <<
    strokeColor: 'blue',
    dash: 1
>>;
```

## 参数

### 方式一：直线和点

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line | 参考直线 |
| point | Point | 平行线经过的点 |

### 方式二：两点和另一点

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point | 定义参考直线的第一个点 |
| point2 | Point | 定义参考直线的第二个点 |
| point | Point | 平行线经过的点 |

## 属性

平行线继承自 Line，因此拥有 Line 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `straightFirst` | Boolean | true | 是否向前延伸 |
| `straightLast` | Boolean | true | 是否向后延伸 |

## 示例

### 1. 创建基本平行线

```js
// 参考直线
A = point(0, 2);
B = point(2, 1);
l = line(A, B);

// 外部点
P = point(3, 3);

// 平行线
par1 = parallel(l, P);
```

### 2. 使用三点创建

```js
// 定义参考直线的两点
p1 = point(0, 2);
p2 = point(2, 1);

// 平行线经过的点
p3 = point(1, 3);

// 平行线（可以限制为线段）
par = parallel(p1, p2, p3) <<
    straightFirst: false,
    straightLast: false
>>;
```

### 3. 平行线族

```js
// 参考直线
A = point(-3, 0);
B = point(3, 2);
l = line(A, B);

// 一系列平行线
for (i = -2; i <= 2; i = i + 1) {
    Pi = point(i, i * 2);
    parallel(l, Pi) << strokeColor: 'blue', strokeWidth: 1 >>;
}
```

### 4. 动态平行线

```js
// 可移动的参考直线
A = point(-2, 0);
B = point(2, 1);
l = line(A, B);

// 可移动的点
P = point(1, 2);

// 动态平行线
par = parallel(l, P) <<
    strokeColor: 'blue',
    dash: 1
>>;

// 显示斜率相同
slopeText = text(-3, 4, function() {
    return "Slope: " + ((B.Y() - A.Y()) / (B.X() - A.X())).toFixed(2);
});
```

### 5. 平行四边形构造

```js
// 三个顶点
A = point(-2, -1);
B = point(2, -1);
C = point(1, 2);

// 边 AB 和 AC
AB = segment(A, B);
AC = segment(A, C);

// 过 C 平行于 AB 的直线
parC = parallel(AB, C);

// 过 B 平行于 AC 的直线
parB = parallel(AC, B);

// 第四个顶点（交点）
D = intersection(parC, parB, 0);

// 平行四边形
parallelogram = polygon(A, B, D, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;
```

### 6. 梯形构造

```js
// 下底
A = point(-3, -2);
B = point(3, -2);
base = segment(A, B);

// 上底的一个端点
C = point(-1, 2);

// 过 C 平行于 base 的直线
par = parallel(base, C);

// 上底的另一个端点（在平行线上）
D = glider(par);

// 梯形
trapezoid = polygon(A, B, D, C) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.5
>>;

// 上底线段
topBase = segment(C, D) << strokeWidth: 2 >>;
```

### 7. 三角形中位线

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 两边中点
mAB = midpoint(A, B);
mAC = midpoint(A, C);

// 中位线（平行于底边 BC）
midline = segment(mAB, mAC);

// 验证平行
baseBC = pol.borders[1];

// 中位线定理：中位线平行于第三边且等于其一半
textText = text(-2, 3, function() {
    return "Midline = " + L(midline).toFixed(2) + ", BC = " + L(baseBC).toFixed(2);
});
```

### 8. 平行线截比例线段

```js
// 两条平行线
l1 = line(point(0, 0), point(4, 1));
P = point(0, 2);
l2 = parallel(l1, P);

// 截线
t1 = line(point(1, -1), point(1, 3));
t2 = line(point(2, -1), point(2, 3));
t3 = line(point(3, -1), point(3, 3));

// 交点
A = intersection(l1, t1, 0);
B = intersection(l1, t2, 0);
C = intersection(l1, t3, 0);
D = intersection(l2, t1, 0);
E = intersection(l2, t2, 0);
F = intersection(l2, t3, 0);

// 平行线分线段成比例
// AB/BC = DE/EF
```

### 9. 坐标网格

```js
// 水平线族
for (i = -4; i <= 4; i = i + 1) {
    line(point(-5, i), point(5, i)) <<
        strokeColor: 'gray',
        strokeWidth: 0.5
    >>;
}

// 垂直线族
for (j = -4; j <= 4; j = j + 1) {
    line(point(j, -5), point(j, 5)) <<
        strokeColor: 'gray',
        strokeWidth: 0.5
    >>;
}
```

### 10. 相似三角形

```js
// 大三角形
A = point(0, 0);
B = point(4, 0);
C = point(0, 3);
bigTri = polygon(A, B, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.3
>>;

// 平行于 BC 的直线
P = point(0, 1.5);
par = parallel(B, C, P);

// 交点
D = intersection(par, A, B, 0);  // 实际上 D 在 AB 上

// 小三角形
// 通过平行线构造相似三角形
```

## 注意事项

1. **唯一性**：过直线外一点有且仅有一条平行线
2. **斜率**：平行线的斜率相等
3. **延伸行为**：使用 `straightFirst` 和 `straightLast` 可以控制直线是否无限延伸
4. **线段模式**：通过三点方式创建时，可以设置为线段模式

## 相关元素

- [Line](./Line.md) - 直线
- [Perpendicular](./Perpendicular.md) - 垂线
- [Segment](./Segment.md) - 线段
- [Intersection](./Intersection.md) - 交点
