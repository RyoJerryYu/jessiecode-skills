# 函数示例 (Functions)

## 图形描述

本示例演示了在 JessieCode 中定义和使用函数的不同方式。展示了函数定义、属性对象组合使用等语法特性。

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

euler = line(H, S) << strokeWidth: 2, strokeColor:'#901B77' >>;
```

## 知识点

1. **属性对象定义**：定义可复用的样式对象，如 `cerise`、`grass`、`perp`、`median`
2. **属性嵌套**：在多边形创建时，使用 `borders: << strokeWidth: 2 >>` 设置边的属性
3. **数组索引访问**：使用 `pol.borders[0]` 访问多边形的第一条边
4. **几何构造流程**：
   - 创建三角形顶点
   - 创建三角形
   - 创建三条垂线段（高）
   - 获取垂心（高的交点）
   - 创建三边中点
   - 创建三条中线
   - 获取重心（中线的交点）
   - 创建外接圆，获取外心
   - 创建欧拉线
5. **动态属性修改**：`grass.name = 'U'` 修改点的名称

## 涉及元素

- [Point](../../03-api/Point.md) - 点
- [Polygon](../../03-api/Polygon.md) - 多边形
- [PerpendicularSegment](../../03-api/PerpendicularSegment.md) - 垂线段
- [Intersection](../../03-api/Intersection.md) - 交点
- [Midpoint](../../03-api/Midpoint.md) - 中点
- [Segment](../../03-api/Segment.md) - 线段
- [Circumcircle](../../03-api/Circumcircle.md) - 外接圆
- [Line](../../03-api/Line.md) - 直线
