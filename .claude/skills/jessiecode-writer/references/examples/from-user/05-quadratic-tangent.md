# 二次函数与切线 (Quadratic Function and Tangent Line)

## 图形描述

展示二次函数 f(x) = x² 的图像，以及函数图像上任意一点处的切线。拖动点可以观察切线斜率如何随切点位置变化。

## JessieCode 代码

```js
f = functiongraph(function(x){return x**2;});
p = glider(1,1,f)<<
	name: "$tanglent$",
	label: <<
		fontsize: 16,
		color: "magenta"
	>>
>>;

t = tangent(p)<<color: "magenta">>;
text(-5,4,"$f(x)=x^2$")<<fontsize: 18>>;
text(-5,3.2, function(){return "$x = "+p.X().toFixed(2)+"$";})<<fontsize:18>>;
text(-5,2.4,function(){return "$k = "+t.Slope().toFixed(2)+"$";})<<fontsize:18>>;
```

## 知识点

- **二次函数**：f(x) = x² 的图像是抛物线
- **切线（Tangent Line）**：与曲线在某点相切的直线
- **导数**：切线的斜率等于函数在该点的导数值
- **导数公式**：对于 f(x) = x²，f'(x) = 2x
- **动态演示**：通过拖动点观察切线斜率的变化规律

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| functiongraph | `functiongraph(fn)` | 创建函数图像 |
| glider | `glider(x, y, object)` | 创建可在对象上滑动的点 |
| tangent | `tangent(point)` | 创建切线 |
| text | `text(x, y, content)` | 创建文本标签 |
| 样式属性 | `<<fontsize: 16, color: "magenta">>` | 设置字体大小和颜色 |
| 动态文本 | `text(x, y, function(){...})` | 创建动态更新的文本 |
| Slope() | `line.Slope()` | 获取直线斜率 |

---
*来源：02-Examples/11-二次函数与切线.md*
