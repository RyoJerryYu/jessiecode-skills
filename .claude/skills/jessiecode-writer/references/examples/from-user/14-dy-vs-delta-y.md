# 微分中 dy 与 Δy 的区别 (Difference between dy and Δy in Differential Calculus)

## 图形描述

不断缩小 $dx$ 滑块，并按住 `shift` 用鼠标滚轮放大，观察 $\Delta y$ 与 $\Delta x$ 的比例，以及 $\Delta y - dy$ 与 $\Delta x$ 的比例。

## JessieCode 代码

```js
F = function(x){return x**2;};
f = functiongraph(F)<<strokeWidth:2>>;
P = glider(0.4,0.16,f);
tanL = tangent(P);

dx = slider([0.1,0.9],[0.3,0.9], [0,0.2,0.5]);

ppx = function() {return P.X()+dx.Value();};
ppy = function() {return F(ppx());};
invisible = <<visible: false>>;
xisdx = line(
	function(){return [ppx(), 0];},
	function(){return [ppx(), ppy()];}
)invisible;
yisy = line(
	function(){return [P.X(), P.Y()];},
	function(){return [ppx(), P.Y()];}
)invisible;

largeFont = <<fontSize:18>>;
deltaP = point(ppx,ppy)<<name:'$\\Delta y$', label:largeFont>>;
dyP = intersection(xisdx, tanL) <<name:'$dy$', label:largeFont>>;
dxP = point(ppx, P.Y())<<withLabel:false>>;

dxL = segment(dxP, P)<<name:'$dx = \\Delta x$', withLabel: true, label: largeFont>>;
delyL = segment(dxP, deltaP)<<color: 'blue'>>;
dyL = segment(dxP, dyP)<<dash:3, color: 'cyan'>>;
text(0.1,0.8,function(){return "$\\frac{\\Delta y - dy}{\\Delta x} = $"+((delyL.L()-dyL.L())/(dxL.L())).toFixed(2);})largeFont;
```

可以观察到，无论怎么缩小，$dy$ 与 $dx$ 的比例都保持不变。而 $\Delta y$ 与 $dy$ 会相对变得越来越接近。$\Delta y$ 与 $\Delta x$ 会越来越接近 $dy$ 与 $dx$ 的比例。

## 知识点

- **函数**：f(x) = x² 是演示用的二次函数
- **增量 Δy**：函数的实际变化量，Δy = f(x+Δx) - f(x)
- **微分 dy**：函数的线性近似变化量，dy = f'(x)dx
- **切线**：在点 P 处与曲线相切的直线，斜率等于导数
- **导数关系**：dy/dx = f'(x)，对于 f(x) = x²，f'(x) = 2x
- **极限思想**：当 Δx → 0 时，Δy ≈ dy，即 (Δy - dy)/Δx → 0
- **几何意义**：
  - Δy 是曲线上两点之间的垂直距离（蓝色线段）
  - dy 是切线上对应两点之间的垂直距离（青色虚线）
  - 当 Δx 足够小时，两者几乎重合

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| function | `function(x){...}` | 定义函数 |
| functiongraph | `functiongraph(f)` | 创建函数图像 |
| glider | `glider(x, y, curve)` | 创建可在曲线上滑动的点 |
| tangent | `tangent(point)` | 创建切线 |
| slider | `slider(p1, p2, [min, max, step])` | 创建滑块控制器 |
| line | `line(p1, p2)` | 创建直线（支持动态点） |
| intersection | `intersection(line, curve)` | 创建交点 |
| point | `point(x, y)` | 创建点 |
| segment | `segment(A, B)` | 创建线段 |
| text | `text(x, y, content)` | 创建文本标签 |
| 动态点 | `point(function(){...}, function(){...})` | 创建位置动态计算的点 |
| 动态文本 | `text(x, y, function(){...})` | 创建动态更新的文本 |
| 样式属性 | `<<visible: false>>` | 隐藏元素 |
| 样式属性 | `<<dash:3, color: 'cyan'>>` | 设置线型和颜色 |
| 样式属性 | `<<fontSize:18>>` | 设置字体大小 |
| LaTeX 数学 | `$\\Delta y$` | 使用 LaTeX 格式显示数学符号 |

---
*来源：04-Cool Showcase/06-微分中 dy 与 delta y 的区别.md*
