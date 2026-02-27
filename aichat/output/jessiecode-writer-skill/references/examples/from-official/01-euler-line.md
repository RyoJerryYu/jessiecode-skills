# 欧拉线 (Euler Line)

## 图形描述

本示例演示了三角形的欧拉线构造。欧拉线是一条通过三角形三个重要点的直线：
- 垂心 H（三条高的交点）
- 重心 S（三条中线的交点）
- 外心 U（外接圆圆心）

这三个点始终共线，形成的直线称为欧拉线。

## JessieCode 代码

```js
// Prepare some visual properties
cerise = <<
    strokeColor: '#901B77',
    fillColor: '#CA147A',
    visible: true,
    withLabel: true
>>;
grass = <<
    strokeColor: '#009256',
    fillColor: '#65B72E',
    visible: true,
    withLabel: true
>>;
perp = <<
    strokeColor: 'black',
    dash: 1,
    strokeWidth: 1,
    point: cerise
>>;
median = <<
    strokeWidth: 1,
    strokeColor: '#333333',
    dash: 2
>>;

// The triangle
A = point(1, 0) cerise;
B = point(-1, 0) cerise;
C = point(0.2, 1.5) cerise;

pol = polygon(A, B, C) << fillColor: '#FFFF00', borders: << strokeWidth: 2, strokeColor: '#009256' >> >>;

// The perpendiculars
H_c = perpendicularsegment(pol.borders[0], C) perp;
H_a = perpendicularsegment(pol.borders[1], A) perp;
H_b = perpendicularsegment(pol.borders[2], B) perp;

// intersection
H = intersection(H_c, H_b, 0) grass;

// Midpoints
mAB = midpoint(A, B) cerise;
mBC = midpoint(B, C) cerise;
mCA = midpoint(C, A) cerise;

ma = segment(mBC, A) median;
mb = segment(mCA, B) median;
mc = segment(mAB, C) median;
S = intersection(ma, mc, 0) grass;

grass.name = 'U';
c = circumcircle(A, B, C) << strokeColor: '#000000', dash: 3, strokeWidth: 1, center: grass >>;

euler = line(H, S) << strokeWidth: 2, strokeColor: '#901B77' >>;
```

## 知识点

1. **属性对象复用**：定义 `cerise`、`grass`、`perp`、`median` 等可复用的属性对象
2. **三角形构造**：使用 `polygon(A, B, C)` 创建三角形
3. **垂线段**：使用 `perpendicularsegment(borders[i], point)` 创建从顶点到对边的垂线段
4. **交点**：使用 `intersection(line1, line2, 0)` 获取两条直线的交点
5. **中点**：使用 `midpoint(A, B)` 创建线段中点
6. **中线**：连接顶点与对边中点的线段
7. **外接圆**：使用 `circumcircle(A, B, C)` 创建三角形外接圆
8. **欧拉线**：通过垂心 H 和重心 S 的直线，外心 U 也在这条线上

## 涉及元素

- [Point](../../03-api/Point.md) - 点
- [Polygon](../../03-api/Polygon.md) - 多边形
- [PerpendicularSegment](../../03-api/PerpendicularSegment.md) - 垂线段
- [Intersection](../../03-api/Intersection.md) - 交点
- [Midpoint](../../03-api/Midpoint.md) - 中点
- [Segment](../../03-api/Segment.md) - 线段
- [Circumcircle](../../03-api/Circumcircle.md) - 外接圆
- [Line](../../03-api/Line.md) - 直线
