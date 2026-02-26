# Gaetano 的几何示例 / Gaetano's Geometry Example

## 图形描述

此示例创建了一个交互式几何图形。主要内容包括：
- 设置画板视图范围为 `[-7, 4, 7, -4]`，并保持宽高比
- 创建原点 O(0,0)、单位点 U(1,0) 和 I(0,1)
- 绘制 x 轴和 y 轴，带箭头和标签
- 创建一个半径为 3 的圆，圆心在原点
- 创建一个可拖动的点 p，初始位置在 (1,1)
- 实现拖动约束逻辑：当点 p 到原点的距离超过圆的半径时，将其移回圆内

这是一个展示几何约束和事件处理的综合示例。

## JessieCode 代码

```javascript
$board.setView([-7,4,7,-4],keepaspectratio=true);
O=point(0,0)<<name:'0',fixed:true>>;
U=point(1,0)<<name:'1',fixed:true>>;
I=point(0,1)<<name:'i',fixed:true>>;
x=line(O,U)<<withLabel:true,name:'x',lastArrow:true>>;
y=line(O,I)<<withLabel:true,name:'y',lastArrow:true>>;
r = 3;
c=circle(O,r);
p=point(1,1)<<color:'lime'>>;
g=<<x:1,y:1>>;
p.on('drag',function(){
	if(sqrt(p.X()^2+p.Y()^2)>r) {
		p.moveTo([g.x,g.y]);
	};
	g.x=p.X();
	g.y=p.Y();
});
```

## 知识点

1. **画板设置**：`$board.setView()` 设置视图范围和选项
2. **点创建**：`point(x, y)` 创建点，可用 `fixed:true` 固定点
3. **直线创建**：`line(point1, point2)` 创建通过两点的直线
4. **圆创建**：`circle(center, radius)` 创建圆
5. **对象属性**：使用 `<< >>` 语法设置对象属性（颜色、标签等）
6. **坐标访问**：`point.X()` 和 `point.Y()` 获取点的坐标
7. **事件处理**：`element.on(eventName, callback)` 注册事件监听器
8. **点移动**：`point.moveTo([x, y])` 将点移动到新位置
8. **数学函数**：`sqrt()` 计算平方根，`^2` 表示平方运算
9. **对象变量**：使用普通对象 `g` 存储上次有效位置

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `$board.setView()` | 设置画板的视图范围和显示选项 | [JSXGraph - board](https://jsxgraph.org/docs/symbols/JSXGraph.html) |
| `point` | 创建几何点元素 | [JSXGraph - Point](https://jsxgraph.org/docs/symbols/Point.html) |
| `line` | 创建通过两点的直线 | [JSXGraph - Line](https://jsxgraph.org/docs/symbols/Line.html) |
| `circle` | 创建圆（圆心 + 半径） | [JSXGraph - Circle](https://jsxgraph.org/docs/symbols/Circle.html) |
| `element.on()` | 为元素注册事件监听器 | [JSXGraph - addEvent](https://jsxgraph.org/docs/symbols/Element.html#addEvent) |
| `point.moveTo()` | 将点移动到指定位置 | [JSXGraph - Point#moveTo](https://jsxgraph.org/docs/symbols/Point.html#moveTo) |
| `point.X() / point.Y()` | 获取点的 X/Y 坐标 | [JSXGraph - Point#X](https://jsxgraph.org/docs/symbols/Point.html#X) |

---

*来源：JessieCode 官方示例 - gaetano_g.html*
