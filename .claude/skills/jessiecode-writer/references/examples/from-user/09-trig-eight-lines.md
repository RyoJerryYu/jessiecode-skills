# 割圆八线 (Eight Trigonometric Lines)

## 图形描述

从下图可看出，正角对应的割线、切线、弦称为正割、正切、正弦，余角对应的称为余割、余切、余弦。

拖动紫色的点，可观察各三角函数如何随角的大小变化而变化。

## JessieCode 代码

```js
O = point(0, 0) << fixed: true >>;
c = circle(O, 1) << strokeWidth: 1 >>;
P = glider(0.6, 0.8, c) << withLabel: false >>;
r = segment(O, P) << visible: false >>;
PX = point(function() { return P.X(); }, 0) << visible: false >>;
PY = point(0, function() { return P.Y(); }) << visible: false >>;
xoneP = point(1, 0) << visible: false >>;
yoneP = point(0, 1) << visible: false >>;
theta = angle(xoneP, O, P) << name: 'θ' >>;

xone = line([1, 0], [1, 1]) << strokeWidth: 1 >>;
yone = line([0, 1], [1, 1]) << strokeWidth: 1 >>;

tanP = intersection(r, xone) << name: '正割点', color: 'magenta' >>;
cotP = intersection(r, yone) << name: '余割点', color: 'green' >>;

sinL = segment(P, PX) << name: '正弦', withLabel: true, color: 'magenta' >>;
cosL = segment(P, PY) << name: '余弦', withLabel: true, color: 'green' >>;

tanL = segment(tanP, xoneP) << name: '正切', withLabel: true, color: 'magenta' >>;
cotL = segment(cotP, yoneP) << name: '余切', withLabel: true, color: 'green' >>;

secL = segment(tanP, O) << name: '正割', withLabel: true, color: 'magenta', dash: 1, strokeWidth: 4 >>;
cscL = segment(cotP, O) << name: '余割', withLabel: true, color: 'green', dash: 2, strokeWidth: 4 >>;

versinL = segment(PX, xoneP) << name: '正矢', withLabel: true, color: 'magenta' >>;
coversinL = segment(PY, yoneP) << name: '余矢', withLabel: true, color: 'green' >>;
```

## 知识点

- **单位圆**：半径为 1 的圆，是定义三角函数的基础
- **正弦（sine）**：sin(θ) = y 坐标，图中为线段 sinL
- **余弦（cosine）**：cos(θ) = x 坐标，图中为线段 cosL
- **正切（tangent）**：tan(θ) = sin(θ)/cos(θ)，图中为线段 tanL
- **余切（cotangent）**：cot(θ) = cos(θ)/sin(θ)，图中为线段 cotL
- **正割（secant）**：sec(θ) = 1/cos(θ)，图中为线段 secL
- **余割（cosecant）**：csc(θ) = 1/sin(θ)，图中为线段 cscL
- **正矢（versine）**：versin(θ) = 1 - cos(θ)，图中为线段 versinL
- **余矢（coversine）**：coversin(θ) = 1 - sin(θ)，图中为线段 coversinL

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| point | `point(x, y)` | 创建点 |
| circle | `circle(center, radius)` | 创建圆 |
| glider | `glider(x, y, circle)` | 创建可在圆上滑动的点 |
| segment | `segment(A, B)` | 创建线段 |
| line | `line(p1, p2)` | 创建直线 |
| intersection | `intersection(line1, line2)` | 创建交点 |
| angle | `angle(A, B, C)` | 创建角（角 ABC） |
| text | `text(x, y, content)` | 创建文本标签 |
| 样式属性 | `<<fixed:true>>` | 固定点不可拖动 |
| 样式属性 | `<<visible: false>>` | 隐藏元素 |
| 样式属性 | `<<withLabel:true, name:'名称'>>` | 显示标签和名称 |
| 样式属性 | `<<dash:1, strokeWidth:4>>` | 设置线型和线宽 |

---
*来源：04-Cool Showcase/01-立方体投影.md（实际内容：割圆八线）*
