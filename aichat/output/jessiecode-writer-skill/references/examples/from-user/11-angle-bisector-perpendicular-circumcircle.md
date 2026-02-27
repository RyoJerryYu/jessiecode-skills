# 三角形角平分线与对边的中垂线交点位于外接圆上

## 图形描述

下图中粉色的为角平分线、内切圆。绿色的为三边中垂线、外接圆。

移动三角形任意一点，可以观察到，对于三角形的一个角，其角平分线与对边的中垂线的交点一定在外接圆上。

另外，内切圆与三边的切点与角平分线、中垂线都无直接关系。

## JessieCode 代码

```js
// Triangle ABC
tStyle = <<color: 'gray'>>;
A = point(-6, -5)tStyle;
B = point(7, -4) tStyle;
C = point(1, 6)tStyle;
pol = polygon(A,B,C) tStyle;

mStyle = <<color: 'gray',withLabel: false>>;
mAB = midpoint(A,B) mStyle;
mBC = midpoint(B,C) mStyle;
mCA = midpoint(C,A) mStyle;

// circumcenter
cStyle = <<strokeColor: 'green', strokeWidth: 1.5>>;
pAB = perpendicular(pol.borders[0], mAB) cStyle;
pBC = perpendicular(pol.borders[1], mBC) cStyle;
pCA = perpendicular(pol.borders[2], mCA) cStyle;

ccABC = circle(A,B,C) cStyle;
cP = intersection(pAB,pBC) cStyle;

// incenter
iStyle = <<strokeColor: 'magenta', strokeWidth: 1.5>>;
bCAB = bisector(C,A,B) iStyle;
bABC = bisector(A,B,C) iStyle;
bBCA = bisector(B,C,A) iStyle;

ciABC = incircle(A,B,C) iStyle;
iP = intersection(bCAB, bABC) iStyle;

// intersection
sStyle = <<color: 'blue'>>;
intersection(pBC, bCAB)sStyle;
intersection(pCA, bABC)sStyle;
intersection(pAB, bBCA)sStyle;
```

## 知识点

- **角平分线（Angle Bisector）**：将一个角平分为两个相等角的射线
- **中垂线（Perpendicular Bisector）**：垂直于线段并通过其中点的直线
- **外接圆（Circumcircle）**：经过三角形三个顶点的圆
- **内切圆（Incircle）**：与三角形三条边都相切的圆
- **几何定理**：三角形的一个角的角平分线与对边中垂线的交点必定在外接圆上
- **外心**：三条中垂线的交点，外接圆的圆心
- **内心**：三条角平分线的交点，内切圆的圆心

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| polygon | `polygon(A, B, C)` | 创建多边形 |
| midpoint | `midpoint(A, B)` | 创建中点 |
| perpendicular | `perpendicular(line, point)` | 创建垂线 |
| bisector | `bisector(A, B, C)` | 创建角平分线 |
| circle | `circle(A, B, C)` | 创建过三点的圆 |
| incircle | `incircle(A, B, C)` | 创建三角形的内切圆 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| 样式对象 | `<<color: 'gray'>>` | 设置颜色样式 |
| 样式属性 | `<<withLabel: false>>` | 隐藏标签 |

---
*来源：04-Cool Showcase/03-三角形角平分线与对边的中垂线交点位于外接圆上.md*
