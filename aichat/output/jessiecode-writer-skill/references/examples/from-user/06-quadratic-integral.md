# 二次函数与积分 (Quadratic Function and Riemann Sum)

## 图形描述

展示二次函数 f(x) = x² 的图像，以及使用黎曼和（右端点法）来近似计算函数下方的面积。通过滑块控制矩形数量，观察近似值如何随分割细化而逼近真实积分值。

## JessieCode 代码

```js
f = function(x){return x**2;};
funcGraph = functiongraph(f);
p = glider(2,4,funcGraph)<<
	name: "$tanglent$",
	label: <<fontsize: 16>>
>>;

overDX = slider([0,-1], [4,-1], [1,5,20]);
rsum = riemannsum(f,
function(){return p.X()*overDX.Value();},
'right',
0,
function() {return p.X();}
);

text(5,4,"$f(x)=x^2$")<<fontsize: 18>>;
text(5,3.2, function(){return "$x = "+p.X().toFixed(2)+"$";})<<fontsize:18>>;
```

## 知识点

- **二次函数**：f(x) = x² 的图像是抛物线
- **黎曼和（Riemann Sum）**：用矩形面积和近似曲线下面积
- **右端点法**：使用每个子区间右端点的函数值作为矩形高度
- **定积分**：当分割无限细时，黎曼和的极限即为定积分值
- **数值积分**：通过有限分割近似计算积分

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| function | `function(x){...}` | 定义函数 |
| functiongraph | `functiongraph(f)` | 创建函数图像 |
| glider | `glider(x, y, object)` | 创建可在对象上滑动的点 |
| slider | `slider(p1, p2, [min, max, step])` | 创建滑块控制器 |
| riemannsum | `riemannsum(f, width, type, start, end)` | 创建黎曼和矩形 |
| text | `text(x, y, content)` | 创建文本标签 |
| 动态文本 | `text(x, y, function(){...})` | 创建动态更新的文本 |

---
*来源：02-Examples/12-二次函数与积分.md*
