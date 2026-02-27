# 欧拉线 (Euler Line)

## 图形描述

- 绿色虚线：中垂线
- 蓝色虚线：中线
- 红色虚线：高

三种线分别交于外心、重心、垂心。外心、重心、垂心必定在同一直线上。

## JessieCode 代码

```js
// Triangle ABC
tStyle = <<fillColor: 'yellow', fillOpacity: 0.2>>;
A = point(-6, -5) tStyle;
B = point(7, -4) tStyle;
C = point(1, 6) tStyle;
tri = polygon(A,B,C) tStyle;

mStyle = <<opacity: 0.2>>;
mAB = midpoint(A,B) mStyle;
mBC = midpoint(B,C) mStyle;
mCA = midpoint(C,A) mStyle;

// circumcenter
cStyle = <<
dash: 2,
color: 'green',
strokeWidth: 1,
radius: 0.5
>>;
pAB = perpendicular(tri.borders[0], mAB) cStyle;
pBC = perpendicular(tri.borders[1], mBC) cStyle;
pCA = perpendicular(tri.borders[2], mCA) cStyle;

angle(pAB, tri.borders[0], -1,-1)cStyle;
angle(pBC, tri.borders[1], -1,-1)cStyle;
angle(pCA, tri.borders[2], -1,-1)cStyle;

circP = intersection(pAB,pBC) cStyle;

// centroid
gStyle = <<
dash:2,
color: 'blue',
strokeWidth: 1
>>;
mA = segment(A, mBC) gStyle;
mB = segment(B, mCA) gStyle;
mC = segment(C, mAB) gStyle;

gravP = intersection(mA,mB) gStyle;

// orthocenter
oStyle = <<
dash:  2,
color: 'red',
strokeWidth: 1,
radius: 0.5
>>;
hA = perpendicularsegment(tri.borders[1], A) oStyle;
hB = perpendicularsegment(tri.borders[2], B) oStyle;
hC = perpendicularsegment(tri.borders[0], C) oStyle;

angle(A, hA.point, B) oStyle;
angle(B, hB.point, C) oStyle;
angle(C, hC.point, A) oStyle;

orthP = intersection(hA,hB) oStyle;

// euler line
eline = line(circP, gravP) <<color: 'fuchsia'>>;
```

## 知识点

- **外心（Circumcenter）**：三角形三条边中垂线的交点（绿色）
- **重心（Centroid）**：三角形三条中线的交点（蓝色）
- **垂心（Orthocenter）**：三角形三条高的交点（红色）
- **欧拉线（Euler Line）**：三角形的外心、重心、垂心三点共线，这条直线称为欧拉线
- **欧拉线性质**：重心位于外心和垂心之间，且重心到外心的距离是重心到垂心距离的一半
- **莱莫恩线**：欧拉线是三角形几何中最著名的共线定理之一

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| polygon | `polygon(A, B, C)` | 创建多边形 |
| midpoint | `midpoint(A, B)` | 创建中点 |
| perpendicular | `perpendicular(line, point)` | 创建垂线 |
| perpendicularsegment | `perpendicularsegment(line, point)` | 创建垂线段 |
| segment | `segment(A, B)` | 创建线段 |
| line | `line(A, B)` | 创建直线 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| angle | `angle(A, B, C)` | 创建角标记 |
| 样式对象 | `<<dash: 2, color: 'green'>>` | 定义样式对象并复用 |

---
*来源：04-Cool Showcase/04-欧拉线.md*
