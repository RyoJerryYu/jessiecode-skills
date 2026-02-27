# 表达式滑块示例 / Expression Slider Example

## 图形描述

此示例展示了一个动态函数绘图功能。代码首先创建一个水平滑块，范围为 0 到 10，初始值为 5，命名为 `a`。然后定义一个线性函数 `f(x) = a*x`，其中 `a` 的值由滑块控制。最后使用 `plot` 函数绘制该函数图像。当用户拖动滑块时，函数图像的斜率会实时更新，展示了 JSXGraph 的动态交互特性。

## JessieCode 代码

```javascript
slider([0, 0], [3, 0], [0, 5, 10]) <<name: 'a'>>;
f = function (x) {
    return a*x;
};
plot(f);
```

## 知识点

1. **滑块创建**：`slider(point1, point2, range)` 创建一个可交互的滑块控件
   - 第一个参数 `[0, 0]`：滑块起点坐标
   - 第二个参数 `[3, 0]`：滑块终点坐标
   - 第三个参数 `[0, 5, 10]`：范围 `[最小值，当前值，最大值]`
2. **滑块命名**：使用 `<<name: 'a'>>` 为滑块变量命名，使其可在后续代码中引用
3. **函数定义**：使用 `function(x) { ... }` 语法定义 JavaScript 函数
4. **动态绑定**：函数内部引用滑块变量 `a`，实现动态更新
5. **函数绘图**：`plot()` 函数用于绘制函数图像

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `slider` | 创建滑块控件，用于动态调整参数值 | [JSXGraph - Slider](https://jsxgraph.org/docs/symbols/Slider.html) |
| `plot` | 绘制函数图像的 JessieCode 内置函数 | [JessieCode - plot](https://jsxgraph.org/docs/symbols/JessieCode.html) |
| `function` | JavaScript 函数定义语法 | [MDN - function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function) |

---

*来源：JessieCode 官方示例 - exprslider.html*
