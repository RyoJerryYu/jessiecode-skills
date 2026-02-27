# 三角形垂心 (Orthocenter)

## 图形描述

三角形 ABC 的三条高交于一点，该点即为三角形的垂心。高是从顶点垂直于对边的线段。

## JessieCode 代码

```js
// Triangle ABC
A = point(-6, -5);
B = point(7, -4);
C = point(1, 6);
pol = polygon(A, B, C);

hA = perpendicularsegment(pol.borders[1], A);
hB = perpendicularsegment(pol.borders[2], B);
hC = perpendicularsegment(pol.borders[0], C);


cc1 = intersection(hA, hB) << withLabel: false >>;
cc2 = intersection(hB, hC) << withLabel: false >>;
distance = sqrt((cc1.X()-cc2.X())^2+(cc1.Y()-cc2.Y())^2);
text(-6, -6, "d = "+distance.toFixed(2));
```

## 知识点

- **高（Altitude）**：从三角形一个顶点向对边作的垂线段
- **垂心（Orthocenter）**：三角形三条高的交点
- **三线共点**：三角形的三条高交于一点（垂心）
- **垂心位置**：锐角三角形垂心在形内，直角三角形垂心在直角顶点，钝角三角形垂心在形外

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| polygon | `polygon(A, B, C)` | 创建多边形 |
| perpendicularsegment | `perpendicularsegment(line, point)` | 创建点到直线的垂线段 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| text | `text(x, y, content)` | 创建文本标签 |

---
*来源：02-Examples/04-三角形垂心.md*
