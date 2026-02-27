# 完全四边形 (Complete Quadrilateral)

## 图形描述

完全四边形是由四条直线（无三线共点）及其六个交点构成的几何图形。本示例展示了完全四边形的调和分割性质：|AD|/|BD| = |AC|/|BC|。

## JessieCode 代码

```js
A = point(-4, -2)<<color:'red'>>;
B = point(0,-2)<<color:'red'>>;
lAB = line(A,B);

C = glider(4,0,lAB)<<color: 'red'>>;

E = point(1,4);
lAE = line(A,E);
lBE = line(B,E);

F = glider(0,0,lAE);
lCF = line(C,F);
G = intersection(lCF, lBE);

lAG = line(A,G)<<dash:2>>;
lBF = line(B,F)<<dash:2>>;
H = intersection(lAG,lBF);
lEH = line(E,H)<<dash:2>>;
D = intersection(lAB, lEH)<<color:'red'>>;

text(2,-4,function(){return "|AD|/|BD|=|AC|/|BC|";});
```

## 知识点

- **完全四边形**：由四条直线（无三线共点）及其六个交点构成的图形
- **调和分割（Harmonic Division）**：点列 (A,B;C,D) 成调和点列，满足 |AD|/|BD| = |AC|/|BC|
- **完全四边形性质**：完全四边形的对角线互相调和分割
- **射影几何**：调和分割是射影几何中的重要概念

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| line | `line(A, B)` | 创建直线 |
| glider | `glider(x, y, line)` | 创建可在直线上滑动的点 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| text | `text(x, y, content)` | 创建文本标签 |
| 样式属性 | `<<color:'red'>>` | 设置颜色 |
| 样式属性 | `<<dash:2>>` | 设置虚线样式 |
| 动态文本 | `text(x, y, function(){...})` | 创建动态更新的文本 |

---
*来源：02-Examples/21-完全四边形.md*
