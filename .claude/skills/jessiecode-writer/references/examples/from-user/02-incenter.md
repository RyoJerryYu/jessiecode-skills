# 三角形内心 (Incenter)

## 图形描述

三角形 ABC 的三条角平分线交于一点，该点即为三角形的内心。内心到三角形三条边的距离相等，是三角形内切圆的圆心。

## JessieCode 代码

```js
// Triangle ABC
A = point(-6, -5);
B = point(7, -4);
C = point(1, 6);
pol = polygon(A, B, C);

bCAB = bisector(C, A, B);
bABC = bisector(A, B, C);
bBCA = bisector(B, C, A);

cI = incircle(A, B, C);

cc1 = intersection(bCAB, bABC) << withLabel: false >>;
cc2 = intersection(bABC, bBCA) << withLabel: false >>;
distance = sqrt((cc1.X()-cc2.X())^2+(cc1.Y()-cc2.Y())^2);
text(-6, -6, "d = "+distance.toFixed(2));
```

## 知识点

- **角平分线（Angle Bisector）**：将一个角平分为两个相等角的射线
- **内心（Incenter）**：三角形三条角平分线的交点
- **内切圆（Incircle）**：与三角形三条边都相切的圆，圆心为内心
- **三线共点**：三角形的三条角平分线交于一点（内心）

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| polygon | `polygon(A, B, C)` | 创建多边形 |
| bisector | `bisector(A, B, C)` | 创建角平分线（角 ABC 的平分线） |
| incircle | `incircle(A, B, C)` | 创建三角形的内切圆 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| text | `text(x, y, content)` | 创建文本标签 |

---
*来源：02-Examples/02-三角形内心.md*
