# 三角形外心 (Circumcenter)

## 图形描述

三角形 ABC 的三条边的中垂线交于一点，该点即为三角形的外心。外心到三角形三个顶点的距离相等，是三角形外接圆的圆心。

## JessieCode 代码

```js
// Triangle ABC
A = point(-6, -5);
B = point(7, -4);
C = point(1, 6);
pol = polygon(A,B,C);

mAB = midpoint(A,B);
mBC = midpoint(B,C);
mAC = midpoint(A,C);

pAB = perpendicular(pol.borders[0], mAB);
pBC = perpendicular(pol.borders[1], mBC);
pAC = perpendicular(pol.borders[2], mAC);

cABC = circle(A,B,C);

cc1 = intersection(pAB,pBC)<<withLabel: false>>;
cc2 = intersection(pAB,pAC)<<withLabel: false>>;
distance = sqrt((cc1.X()-cc2.X())**2+(cc1.Y()-cc2.Y())**2);
text(-6,-6,"d = "+distance.toFixed(2));
```

## 知识点

- **中垂线（Perpendicular Bisector）**：垂直于线段并通过其中点的直线
- **外心（Circumcenter）**：三角形三条边中垂线的交点
- **外接圆（Circumcircle）**：经过三角形三个顶点的圆，圆心为外心
- **三线共点**：三角形的三条中垂线交于一点（外心）

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| polygon | `polygon(A, B, C)` | 创建多边形 |
| midpoint | `midpoint(A, B)` | 创建中点 |
| perpendicular | `perpendicular(line, point)` | 创建垂线 |
| circle | `circle(A, B, C)` | 创建过三点的圆 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| text | `text(x, y, content)` | 创建文本标签 |

---
*来源：02-Examples/01-三角形外心.md*
