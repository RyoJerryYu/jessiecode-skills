# Text3D 3D 文本

<!-- USAGE_FREQUENCY: advanced -->

## 描述

在 3D 视图中创建文本元素。

## JessieCode 语法

```js
// 通过坐标和文本创建 3D 文本
txt = view.create('text3d', [[x, y, z], '文本内容'], options);

// 使用函数创建动态位置
txt = view.create('text3d', [function() { return [x, y, z]; }, '文本'], options);

// 带属性创建
txt = view.create('text3d', [[1, 2, 1], 'hello'], <<
    fontSize: 20,
    strokeColor: 'red'
>>);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | x 坐标（数字或函数） |
| y | Number/Function | y 坐标（数字或函数） |
| z | Number/Function | z 坐标（数字或函数） |
| txt | String/Function | 文本内容（字符串或函数） |
| slide (可选) | GeometryElement3D | 可选的 3D 元素，使文本成为该元素上的滑点 |

**参数组合说明**：
- `x, y, z, txt, slide`：坐标由 x, y, z 组成（数字或函数），加上文本内容。如果提供可选的 3D 元素 "slide"，则文本成为该元素上的滑点
- `[x, y, z], txt, slide`：坐标可以作为数组或返回数组的函数提供

## 属性

Text3D 继承自 Text 元素，因此支持 Text 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fontSize` | Number | 12 | 字体大小（像素） |
| `strokeColor` | String | '#000000' | 文本颜色 |
| `fillColor` | String | '#000000' | 填充颜色（如使用特定显示模式） |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `anchorX` | String | 'left' | 水平锚点：'left', 'middle', 'right' |
| `anchorY` | String | 'middle' | 垂直锚点：'top', 'middle', 'bottom' |
| `display` | String | 'internal' | 显示模式：'internal', 'html', 'canvas' |
| `cssClass` | String | '' | CSS 类名（display 为 html 时） |
| `useMathJax` | Boolean | false | 使用 MathJax 渲染数学公式 |

## 方法

### normalizeCoords()

规范化齐次坐标，使第一个坐标（w 坐标）等于 1 或 0。

**返回值**：Text3D 对象的引用

**示例**：
```js
p.normalizeCoords();
```

### setPosition(coords, noevent)

设置 3D 点的位置。

**参数**：
- `coords`：3D 坐标，形式为 [x, y, z]（欧几里得）或 [w, x, y, z]（齐次）
- `noevent`：如果为 true，则不触发事件

**返回值**：Text3D 对象的引用

**示例**：
```js
p.setPosition([1, 3, 4]);
```

### updateCoords()

更新齐次坐标数组（私有方法）。

**返回值**：Text3D 对象的引用

**示例**：
```js
p.updateCoords();
```

## 示例

### 1. 基本 3D 文本

```js
var bound = [-4, 6];
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central'
    });

var txt1 = view.create('text3d', [[1, 2, 1], 'hello'], {
    fontSize: 20,
});
```

### 2. 设置文本样式

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central'
    });

// 红色大字体文本
var txt1 = view.create('text3d', [[2, 2, 2], '红色文本'], {
    fontSize: 24,
    strokeColor: 'red',
    anchorX: 'middle',
    anchorY: 'middle'
});

// 蓝色小字体文本
var txt2 = view.create('text3d', [[-2, -2, 0], '蓝色文本'], {
    fontSize: 14,
    strokeColor: 'blue'
});
```

### 3. 动态位置文本

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 创建动点
var p = view.create('point3d', [
    function() { return Math.cos(Date.now() / 1000); },
    function() { return Math.sin(Date.now() / 1000); },
    0
], {size: 4});

// 文本跟随点移动
var txt = view.create('text3d', [
    function() { return p.X(); },
    function() { return p.Y(); },
    function() { return p.Z(); },
    '动点'
], {
    fontSize: 14,
    strokeColor: 'blue'
});
```

### 4. 使用数组提供坐标

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 坐标作为数组提供
var txt = view.create('text3d', [
    [1, 2, 3],
    '坐标 [1,2,3]'
], {
    fontSize: 16
});

// 或使用返回数组的函数
var txt2 = view.create('text3d', [
    function() { return [Math.sin(t), Math.cos(t), 0]; },
    '函数坐标'
], {
    fontSize: 16
});
```

### 5. 文本锚点

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 左对齐（默认）
var txt1 = view.create('text3d', [[0, 0, 0], '左对齐'], {
    anchorX: 'left',
    anchorY: 'middle'
});

// 居中对齐
var txt2 = view.create('text3d', [[0, 1, 0], '居中对齐'], {
    anchorX: 'middle',
    anchorY: 'middle'
});

// 右对齐
var txt3 = view.create('text3d', [[0, 2, 0], '右对齐'], {
    anchorX: 'right',
    anchorY: 'middle'
});
```

### 6. HTML 显示模式

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 使用 HTML 显示模式，可以应用 CSS 样式
var txt = view.create('text3d', [[0, 0, 0], '<b>粗体</b> <i>斜体</i>'], {
    display: 'html',
    cssClass: 'my-3d-text'
});
```

### 7. 数学公式

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 使用 MathJax 显示数学公式
var txt = view.create('text3d', [[0, 0, 0], '$$x^2 + y^2 = z^2$$'], {
    useMathJax: true,
    fontSize: 18
});
```

### 8. 标记 3D 点

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central'
    });

// 创建几个点
var p1 = view.create('point3d', [1, 1, 1], {size: 4, withLabel: false});
var p2 = view.create('point3d', [3, 2, 1], {size: 4, withLabel: false});
var p3 = view.create('point3d', [2, 3, 2], {size: 4, withLabel: false});

// 用文本标记这些点
var txt1 = view.create('text3d', [
    function() { return [p1.X() + 0.2, p1.Y() + 0.2, p1.Z()]; },
    'P1'
], {
    fontSize: 14,
    strokeColor: 'red'
});

var txt2 = view.create('text3d', [
    function() { return [p2.X() + 0.2, p2.Y() + 0.2, p2.Z()]; },
    'P2'
], {
    fontSize: 14,
    strokeColor: 'blue'
});

var txt3 = view.create('text3d', [
    function() { return [p3.X() + 0.2, p3.Y() + 0.2, p3.Z()]; },
    'P3'
], {
    fontSize: 14,
    strokeColor: 'green'
});
```

### 9. 滑块控制文本位置

```js
// 创建滑块
var sliderX = board.create('slider', [[-4, -2], [4, 4], [-5, 0, 5]]);
var sliderY = board.create('slider', [[-2, 0], [4, 4], [-5, 0, 5]]);

var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 文本位置随滑块变化
var txt = view.create('text3d', [
    function() { return sliderX.Value(); },
    function() { return sliderY.Value(); },
    1,
    '滑块控制位置'
], {
    fontSize: 16,
    strokeColor: 'purple'
});
```

### 10. 3D 坐标轴标签

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        axesPosition: 'none'
    });

// 创建坐标轴标签
var labelX = view.create('text3d', [[5.2, 0, 0], 'x'], {
    fontSize: 16,
    anchorX: 'middle'
});

var labelY = view.create('text3d', [[0, 5.2, 0], 'y'], {
    fontSize: 16,
    anchorX: 'middle'
});

var labelZ = view.create('text3d', [[0, 0, 5.2], 'z'], {
    fontSize: 16,
    anchorX: 'middle'
});
```

## 注意事项

1. **坐标格式**：坐标可以作为三个独立参数 [x, y, z] 提供，也可以作为数组 [x, y, z] 提供
2. **动态更新**：当坐标或文本内容使用函数时，文本会动态更新
3. **显示模式**：`display: 'html'` 允许使用 HTML 标签和 CSS 样式
4. **MathJax**：使用 `useMathJax: true` 可以渲染 LaTeX 数学公式
5. **锚点**：使用 `anchorX` 和 `anchorY` 控制文本的对齐方式
6. **滑点**：如果提供可选的 3D 元素作为 slide 参数，文本可以成为该元素上的滑点

## 相关元素

- [Text](./Text.md) - 2D 文本
- [Point3D](./Point3D.md) - 3D 点
- [View3D](./View3D.md) - 3D 视图
- [Label](./Label.md) - 标签
