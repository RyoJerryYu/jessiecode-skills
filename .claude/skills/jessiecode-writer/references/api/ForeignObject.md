# ForeignObject 外部对象

<!-- USAGE_FREQUENCY: advanced -->

## 描述

在 SVG foreignObject 容器中显示任何 HTML 内容 - 甚至可以显示在其他元素下方。

可以使用 `board.create('foreignobject')` 的快捷方式 `board.create('fo')`。

**注意：** 在 Safari 15 及更早版本中，如果 foreignObject 包含 `<video>` 或 `<iframe>` 标签，或使用 `position:absolute|relative|fixed` 定位的元素，foreignObject 不遵守图层结构。在这种情况下，foreignobject 将显示在 JSXGraph 构造的"上方"。

## JessieCode 语法

```js
// 基本语法 - 创建外部对象
fo = foreignobject(content, position, size);

// 快捷方式
fo = fo(content, position, size);

// 仅指定内容和位置
fo = foreignobject('<div>Hello</div>', [0, 0]);

// 指定内容、位置和大小
fo = foreignobject('<div>Hello</div>', [0, 0], [2, 1]);

// 带属性创建
fo = foreignobject(content, [x, y], [width, height]) <<
    layer: 0,
    fixed: true
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| content | String | foreignObject 的 HTML 内容。也可以是 `<video>` 或 `<iframe>` |
| position | Array | foreignObject 的位置，格式为 [x, y]（用户坐标）。与图像相同 |
| size | Array (可选) | foreignObject 的大小（用户坐标）。如果未指定，大小由内容的 HTML 属性或 CSS 属性决定 |

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md), JXG.CoordsElement**
&nbsp;&nbsp;&nbsp;↳ **[JXG.ForeignObject](./JXG.ForeignObject.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **ForeignObject**

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `attractors` | Array | empty | 吸引器元素列表 |
| `evaluateOnlyOnce` | Boolean | false | 如果设置为 true，此对象仅计算一次，更新时不重新计算 |
| `layer` | Number | 0 | 图层编号（决定显示顺序） |
| `fixed` | Boolean | false | 是否固定（不可拖动） |
| `visible` | Boolean | true | 是否可见 |

### attractors {Array}

吸引器元素列表。如果 foreignobject 与吸引器的距离小于 attractorDistance，则 foreignobject 成为该元素的滑点。

*定义于：* [options.js](./src/src_options.js.md)

**默认值：** empty

### evaluateOnlyOnce {Boolean}

如果设置为 true，此对象仅计算一次，更新时不重新计算。

这在一个 foreignObject 中的另一个 board 中是必要的。

*定义于：* [options.js](./src/src_options.js.md)

**默认值：** false

## 示例

### 1. 显示视频

```js
// 创建一个点作为参考
p = point(1, 7) << size: 16 >>;

// 创建包含视频的外部对象
fo = foreignobject(
    '<video width="300" height="200" src="https://example.com/video.mp4" controls></video>',
    [0, -3],
    [9, 6]
) <<
    layer: 8,
    fixed: true
>>;
```

### 2. 显示 HTML 文本框

```js
// 使用快捷方式创建外部对象
fo = fo(
    '<div style="background-color:blue; color: yellow; padding:20px; width:200px; height:50px;">Hello</div>',
    [-7, -6]
) <<
    layer: 1,
    fixed: false
>>;
```

### 3. 视频背景上的函数图像

```js
// 创建背景为浅蓝色的画板
// board.renderer.container.style.backgroundColor = 'lightblue';

// 创建点
p1 = point(-2, 3.5) << fixed: false, color: 'yellow', size: 6, name: '6 am' >>;
p2 = point(0, 3.5) << fixed: false, color: 'yellow', size: 6, name: '12 pm' >>;
p3 = point(2, 3.5) << fixed: false, color: 'yellow', size: 6, name: '6 pm' >>;

// 创建包含视频的外部对象作为背景
fo = fo(
    '<video width="100%" height="100%" src="https://example.com/video.mp4" controls></video>',
    [-6, -4],
    [12, 8]
) <<
    layer: 0,
    fixed: true
>>;

// 创建插值多项式函数
f = (x) => {
    // 拉格朗日插值多项式
    return 0.5 * x * x - 0.5 * x + 3.5;
};

// 在视频上绘制函数图像
graph = functiongraph(f, -10, 10) <<
    fixed: true,
    strokeWidth: 3,
    layer: 8
>>;
```

### 4. 显示 iframe

```js
// 创建包含 iframe 的外部对象
fo = fo(
    '<iframe src="https://www.openstreetmap.org/export/embed.html?bbox=-0.004017949104309083%2C51.47612752641776%2C0.0003057718276977539%2C51.478569861898606&layer=mapnik" width="400" height="300" frameborder="0"></iframe>',
    [-5, -5],
    [10, 8]
) <<
    layer: 5,
    fixed: true
>>;
```

### 5. 交互式 HTML 表单

```js
// 创建包含输入表单的外部对象
fo = fo(
    '<div style="background-color: white; padding: 15px; border: 1px solid #ccc;">' +
        '<label for="slider1">滑块值：</label>' +
        '<input type="range" id="slider1" min="0" max="10" value="5">' +
        '<span id="value">5</span>' +
    '</div>',
    [3, 5]
) <<
    fixed: true,
    layer: 10
>>;
```

### 6. 自定义样式面板

```js
// 创建包含自定义控件的面板
fo = fo(
    '<div style="' +
        'background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); ' +
        'color: white; ' +
        'padding: 20px; ' +
        'border-radius: 10px; ' +
        'width: 200px;' +
    '">' +
        '<h3 style="margin: 0 0 10px 0;">控制面板</h3>' +
        '<p>调整参数来改变图形</p>' +
    '</div>',
    [-8, 5]
) <<
    fixed: true,
    layer: 100
>>;
```

### 7. 使用 CSS 定位的内容

```js
// 注意：在 Safari 中，使用 position 定位可能不遵守图层结构
fo = fo(
    '<div style="' +
        'position: relative;' +
        'width: 150px;' +
        'height: 100px;' +
        'background-color: rgba(255, 0, 0, 0.5);' +
    '">' +
        '<span style="position: absolute; top: 10px; left: 10px;">绝对定位内容</span>' +
    '</div>',
    [0, 0],
    [3, 2]
);
```

### 8. 动态内容

```js
// 创建外部对象，内容为动态生成
content = '<div id="dynamic-content">初始内容</div>';
fo = fo(content, [-5, 5]) << fixed: true >>;

// 可以通过 JavaScript 更新内容
// document.getElementById('dynamic-content').innerText = '更新后的内容';
```

### 9. 图片画廊

```js
// 创建包含多张图片的外部对象
fo = fo(
    '<div style="display: flex; gap: 10px;">' +
        '<img src="image1.jpg" width="100">' +
        '<img src="image2.jpg" width="100">' +
        '<img src="image3.jpg" width="100">' +
    '</div>',
    [-6, -3],
    [12, 3]
) <<
    layer: 1,
    fixed: true
>>;
```

### 10. 数学公式显示

```js
// 使用 MathJax 或 KaTeX 显示数学公式
fo = fo(
    '<div style="font-size: 18px; background: white; padding: 10px;">' +
        '<p>二次公式：</p>' +
        '<p>x = \\frac{-b \\pm \\sqrt{b^2 - 4ac}}{2a}</p>' +
    '</div>',
    [4, 4],
    [4, 2]
) <<
    fixed: true,
    layer: 10
>>;
```

## 注意事项

1. **Safari 兼容性**：在 Safari 15 及更早版本中，包含 `<video>`、`<iframe>` 或使用 CSS position 定位的 foreignObject 可能不遵守图层结构
2. **图层控制**：使用 `layer` 属性控制 foreignObject 的显示顺序。较小的值显示在下层，较大的值显示在上层
3. **大小指定**：可以不指定大小，让内容决定大小；或指定大小以控制显示区域
4. **HTML 内容**：可以是任何有效的 HTML，包括 `<video>`、`<iframe>`、表单等
5. **性能考虑**：复杂 HTML 内容可能影响渲染性能
6. **固定位置**：通常设置 `fixed: true` 防止意外移动

## 相关元素

- [Image](./Image.md) - 图像
- [Text](./Text.md) - 文本
- [Group](./Group.md) - 分组
