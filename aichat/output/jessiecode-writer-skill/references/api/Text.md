# Text 文本

## 描述

文本元素用于在画布上显示文字。支持 HTML、MathJax、KaTeX 和 GEONExT 语法。坐标可以是绝对的（相对于画布坐标系）或相对于某个锚点元素。

## JessieCode 语法

```js
// 基本语法 - 固定位置文本
t = text(x, y, "Hello World");

// 动态位置文本
t = text(function() { return A.X(); }, 1, "Dynamic");

// 动态内容文本
t = text(0, 0, function() { return "Value: " + V(slider); });

// 相对于点的文本（锚点）
t = text(0.5, 0.5, "Label") << anchor: pointA >>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | x 坐标（数字或函数） |
| y | Number/Function | y 坐标（数字或函数） |
| text | String/Function | 文本内容（字符串或返回字符串的函数） |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fontSize` | Number | 12 | 字体大小（像素） |
| `fontUnit` | String | 'px' | 字体单位 |
| `display` | String | 'html' | 渲染方式：'html' 或 'internal' |
| `anchor` | Point/Text/Image | null | 锚点元素 |
| `anchorX` | String | 'left' | 水平对齐：'left', 'middle', 'right', 'auto' |
| `anchorY` | String | 'middle' | 垂直对齐：'top', 'middle', 'bottom', 'auto' |
| `rotate` | Number | 0 | 旋转角度（度） |
| `visible` | Boolean | true | 是否可见 |
| `parse` | Boolean | true | 是否解析文本（用于下标等） |

### 数学渲染属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `useMathJax` | Boolean | false | 使用 MathJax 渲染 |
| `useKatex` | Boolean | false | 使用 KaTeX 渲染 |
| `useASCIIMathML` | Boolean | false | 使用 ASCIIMathML 渲染 |

### 数字格式化属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `digits` | Number | 2 | 小数位数 |
| `formatNumber` | Boolean | false | 格式化数字 |
| `toFraction` | Boolean | false | 显示为分数 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `setText(text)` | text: String | 设置文本内容 |
| `move(dx, dy)` | dx, dy: Number | 移动文本 |
| `free()` | 无 | 释放文本 |

## 示例

### 1. 创建基本文本

```js
// 固定位置文本
t1 = text(0, 1, "Hello World");

// 多行文本（使用 HTML）
t2 = text(0, 2, "Line 1<br>Line 2");

// 带变量名的文本
t3 = text(1, 1, "Point A");
```

### 2. 动态位置文本

```js
// 文本跟随点移动
A = point(1, 2);
label = text(0.3, 0.3, "A") << anchor: A >>;

// 或使用函数
A = point(1, 2);
label2 = text(function() { return A.X() + 0.3; },
              function() { return A.Y() + 0.3; },
              "A");
```

### 3. 动态内容文本

```js
// 显示滑块值
s = slider([1, 4], [4, 4], [0, 1, 10]);
valueText = text(1, 3, function() {
    return "Slider value: " + V(s).toFixed(2);
});

// 显示点坐标
P = point(2, 3);
coordText = text(0, 0, function() {
    return "P = (" + P.X().toFixed(2) + ", " + P.Y().toFixed(2) + ")";
});
```

### 4. 设置字体样式

```js
// 自定义字体大小
t1 = text(0, 1, "Large text") <<
    fontSize: 24
>>;

// 使用不同字体单位
t2 = text(0, 2, "Responsive") <<
    fontUnit: 'vw',
    fontSize: 2
>>;
```

### 5. 文本对齐

```js
// 左对齐（默认）
t1 = text(0, 1, "Left") <<
    anchorX: 'left'
>>;

// 居中对齐
t2 = text(0, 2, "Center") <<
    anchorX: 'middle'
>>;

// 右对齐
t3 = text(0, 3, "Right") <<
    anchorX: 'right',
    anchorY: 'bottom'
>>;
```

### 6. 使用 MathJax 显示数学公式

```js
// 需要加载 MathJax
t1 = text(0, 1, "\\( x = \\frac{-b \\pm \\sqrt{b^2-4ac}}{2a} \\)") <<
    label: << useMathJax: true, parse: false >>
>>;

// 希腊字母
t2 = text(0, 2, "\\( \\alpha + \\beta = \\gamma \\)") <<
    label: << useMathJax: true >>
>>;
```

### 7. 显示计算结果

```js
// 计算并显示
A = point(0, 0);
B = point(3, 4);
s = segment(A, B);

// 显示距离
distText = text(0, 5, function() {
    return "Distance AB = " + L(s).toFixed(2);
});

// 显示面积
C = point(0, 4);
pol = polygon(A, B, C);
areaText = text(0, 6, function() {
    return "Area = " + area(pol).toFixed(2);
});
```

### 8. 旋转文本

```js
// 旋转 45 度（需要 display: 'internal'）
t1 = text(0, 0, "Rotated") <<
    rotate: 45,
    display: 'internal'
>>;
```

### 9. 标签自动解析

```js
// 解析下标
A = point(0, 0) << withLabel: true, name: 'A_1' >>;

// 解析上标
B = point(1, 1) << withLabel: true, name: 'x^2' >>;

// 关闭解析
C = point(2, 2) << withLabel: true, name: 'A_B', parse: false >>;
```

### 10. 分数显示

```js
// 显示为分数
t1 = text(0, 1, 0.5) <<
    formatNumber: true,
    toFraction: true,
    useMathJax: true
>>;
// 显示为：1/2

// 自定义小数位数
t2 = text(0, 2, PI) <<
    formatNumber: true,
    digits: 4
>>;
// 显示为：3.1416
```

### 11. 条件文本

```js
// 根据条件显示不同文本
s = slider([1, 4], [4, 4], [-5, 0, 5]);
statusText = text(1, 3, function() {
    if (V(s) > 0) {
        return "Positive";
    } else if (V(s) < 0) {
        return "Negative";
    } else {
        return "Zero";
    }
});
```

### 12. 组合使用

```js
// 创建函数图像
a = slider([1, 4], [4, 4], [-3, 1, 3]) << name: 'a' >>;
f = function(x) { return V(a) * x * x; };
graph = functiongraph(f, -3, 3);

// 显示函数方程
funcText = text(-3, 3, function() {
    return "f(x) = " + V(a).toFixed(2) + "x²";
}) <<
    fontSize: 16,
    anchorX: 'left'
>>;

// 显示顶点
vertex = point(0, 0);
vertexLabel = text(0.2, 0.2, "Vertex") <<
    anchor: vertex,
    anchorX: 'left',
    anchorY: 'bottom'
>>;
```

## 注意事项

1. **坐标系统**：坐标是相对于画布的绝对坐标，除非使用了 `anchor` 属性
2. **动态内容**：文本内容可以是函数，用于创建动态更新的文本
3. **MathJax/KaTeX**：使用数学渲染需要相应库已加载
4. **解析功能**：`parse: true` 可以将 `k_a` 转换为下标格式
5. **锚点坐标**：使用锚点时，坐标是相对于锚点的偏移量

## 相关元素

- [Label](./Label.md) - 标签（元素的子标签）
- [Smartlabel](./Smartlabel.md) - 智能标签
- [Button](./Button.md) - 按钮（可包含文本）
