# 三角形重心 (Centroid)

## 图形描述

三角形 ABC 的三条中线交于一点，该点即为三角形的重心。重心将每条中线分为 2:1 两段，重心到顶点的距离是到对边中点距离的两倍。

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

mStyle = <<dash:2>>;
mA = segment(A,mBC) mStyle;
mB = segment(B,mAC) mStyle;
mC = segment(C,mAB) mStyle;


cc1 = intersection(mA,mB)<<withLabel: false>>;
cc2 = intersection(mB,mC)<<withLabel: false>>;
distance = sqrt((cc1.X()-cc2.X())**2+(cc1.Y()-cc2.Y())**2);
text(-6,-6,"d = "+distance.toFixed(2));
```

## 知识点

- **中线（Median）**：连接三角形一个顶点和对边中点的线段
- **重心（Centroid）**：三角形三条中线的交点
- **重心性质**：重心将每条中线分为 2:1 两段（顶点到重心：重心到中点）
- **三线共点**：三角形的三条中线交于一点（重心）
- **质心**：重心也是三角形的质量中心（假设均匀分布）

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| polygon | `polygon(A, B, C)` | 创建多边形 |
| midpoint | `midpoint(A, B)` | 创建中点 |
| segment | `segment(A, B)` | 创建线段 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| text | `text(x, y, content)` | 创建文本标签 |
| 样式属性 | `<<dash:2>>` | 设置虚线样式 |

---
*来源：02-Examples/03-三角形重心.md*
