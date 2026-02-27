# Input 输入框

## 描述

Input 元素用于创建包含 HTML 表单输入元素的特殊文本。该元素的 "display" 属性必须设置为 'html'（默认值）。

**设置 CSS 类：** `cssClass` 属性会影响包含输入元素的 HTML div 元素。要更改 HTML 输入元素的 CSS 样式，需要使用形式为 `.myinput > input { ... }` 的选择器。参见 Button 元素的类似示例：[Button](./Button.md)。

**使用 JavaScript 访问输入元素：** 底层的 HTML 输入元素可以通过子对象 'rendNodeInput' 访问，例如添加事件监听器。

*定义于：* [input.js](./src/src_element_input.js.md)。
*继承自* [Text](./Text.md)。

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md), JXG.CoordsElement**
   ↳ **[JXG.Text](./JXG.Text.md)**
      ↳ **[Text](./Text.md)**
         ↳ **Input**

## JessieCode 语法

```js
// 基本语法 - 创建输入框
inp = input(x, y, 'defaultValue', 'label');

// 带属性创建
inp = input(0, 1, 'sin(x)*x', 'f(x)=') <<
    cssStyle: 'width: 100px'
>>;

// 使用函数创建动态输入框
inp = input(-6, 1, 'Math.sin(x)*x', 'f(x)=') <<
    cssStyle: function() { return 'width:' + slider.Value() + 'px'; }
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | 输入框左下角的 x 坐标（数字或函数） |
| y | Number/Function | 输入框左下角的 y 坐标（数字或函数） |
| value | String | 输入框的默认值（字符串） |
| label | String/Function | 输入框的标签（字符串或函数） |

**说明：**
- x 和 y 是输入框左下角的坐标。当 x 和 y 为数字时，位置固定；当 x 或 y 为函数时，位置可变。
- 默认值必须以字符串形式提供。
- 标签可以是字符串或函数。

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `cssStyle` | String/Function | '' | CSS 样式字符串或返回样式字符串的函数 |
| `cssClass` | String | '' | CSS 类名 |
| `highlightCssClass` | String | '' | 高亮时的 CSS 类名 |
| `disabled` | Boolean | false | 是否禁用输入框 |
| `maxlength` | Number | 524288 | 最大字符数 |
| `visible` | Boolean | true | 是否可见 |

### 专用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `disabled` | Boolean | false | 控制 HTML 输入框的 "disabled" 属性 |
| `maxlength` | Number | 524288 | 控制 HTML 输入框的 "maxlength" 属性（同 HTML 默认值） |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `set(val)` | val: String | 设置输入框的值 |
| `Value()` | 无 | 获取输入框的内容（值） |
| `setText(val)` | val: String | 设置输入框的标签文本 |

## 子对象

| 子对象 | 描述 |
|--------|------|
| `rendNodeInput` | 底层的 HTML 输入元素，可用于添加事件监听器等操作 |

## 示例

### 1. 创建基本输入框

```js
// 在位置 [0, 1] 创建输入框
inp = input(0, 1, 'sin(x)*x', 'f(x)=') <<
    cssStyle: 'width: 100px'
>>;

// 使用输入框的值创建函数图像
f = function(x) { return JXG.snippet(inp.Value(), true, 'x', false); };
graph = functiongraph(f,
    function() {
        var c = new Coords(JXG.COORDS_BY_SCREEN, [0, 0], board);
        return c.usrCoords[1];
    },
    function() {
        var c = new Coords(JXG.COORDS_BY_SCREEN, [board.canvasWidth, 0], board);
        return c.usrCoords[1];
    }
);
```

### 2. 添加事件监听器 (keyup)

```js
// 创建一个点
A = point(3, -2);

// 创建输入框
inp = input(-4, -4, '1', 'x ');

// 添加 keyup 事件监听器
inp.rendNodeInput.addEventListener('keyup', function() {
    var x = parseFloat(this.value);
    if (!isNaN(x)) {
        A.moveTo([x, 3], 100);
    }
});
```

### 3. 添加事件监听器 (change)

```js
// 创建一个点
A = point(3, -2);

// 创建输入框
inp = input(-4, -4, '1', 'x ');

// 添加 change 事件监听器
inp.rendNodeInput.addEventListener('change', function() {
    var x = parseFloat(inp.Value());
    A.moveTo([x, 2], 100);
});
```

### 4. 动态改变输入框宽度

```js
// 创建滑块
s = slider([-3, 3], [2, 3], [50, 100, 300]);

// 创建输入框，宽度随滑块变化
inp = input(-6, 1, 'Math.sin(x)*x', 'f(x)=') <<
    cssStyle: function() { return 'width:' + s.Value() + 'px'; }
>>;
```

### 5. 应用 CSS 类

```js
// 在 HTML 中定义 CSS 样式
/*
<style>
    div.JXGtext_inp {
        font-weight: bold;
    }

    // 标签
    div.JXGtext_inp > span > span {
        padding: 3px;
    }

    // 输入框
    div.JXGtext_inp > span > input {
        width: 100px;
        border: solid 4px red;
        border-radius: 25px;
    }
</style>
*/

// 创建带有 CSS 类的输入框
inp = input(-6, 1, 'x', 'y') <<
    cssClass: 'JXGtext_inp',
    highlightCssClass: 'JXGtext_inp'
>>;
```

### 6. 使用 set 方法修改值

```js
// 创建输入框
i1 = input(-3, 4, 'sin(x)', 'f(x)=') <<
    cssStyle: 'width:4em',
    maxlength: 2
>>;

// 创建按钮，点击时修改输入框的值
b1 = button(-3, -1, '修改', function() {
    i1.setText('g(x)');  // 修改标签
    i1.set('cos(x)');    // 修改值
}) <<
    cssStyle: 'width:400px'
>>;
```

### 7. 结合 Checkbox 和 Button

```js
// 创建输入框
i1 = input(-3, 4, 'sin(x)', 'f(x)=') <<
    cssStyle: 'width:4em',
    maxlength: 2
>>;

// 创建复选框
c1 = checkbox(-3, 2, '标签 1');

// 创建按钮
b1 = button(-3, -1, '修改文本', function() {
    i1.setText('g(x)');
    i1.set('cos(x)');
    c1.setText('标签 2');
    b1.setText('文本已修改');
}) <<
    cssStyle: 'width:400px'
>>;
```

### 8. 更新函数图像

```js
// 创建输入框
inp = input(0, 1, 'sin(x)*x', 'f(x)=') <<
    cssStyle: 'width: 100px'
>>;

// 创建函数图像
f = board.jc.snippet(inp.Value(), true, 'x', false);
graph = functiongraph(f,
    function() {
        var c = new Coords(JXG.COORDS_BY_SCREEN, [0, 0], board);
        return c.usrCoords[1];
    },
    function() {
        var c = new Coords(JXG.COORDS_BY_SCREEN, [board.canvasWidth, 0], board);
        return c.usrCoords[1];
    }
);

// 创建更新按钮
updateBtn = button(1, 3, '更新图像', function() {
    graph.Y = board.jc.snippet(inp.Value(), true, 'x', false);
    graph.updateCurve();
    board.update();
});
```

## 注意事项

1. **display 属性**：Input 元素的 "display" 属性必须设置为 'html'（默认值）
2. **CSS 样式**：使用 `cssStyle` 属性设置输入框的样式，可以是字符串或返回字符串的函数
3. **CSS 类**：使用 `cssClass` 设置 CSS 类名，使用选择器 `.myinput > input { ... }` 可以样式化 HTML input 元素
4. **访问 HTML 元素**：通过 `rendNodeInput` 子对象可以访问底层的 HTML 输入元素
5. **事件监听**：可以为 `rendNodeInput` 添加 'keyup'、'change' 等事件监听器
6. **坐标固定与可变**：x 和 y 为数字时位置固定，为函数时位置可变

## 相关元素

- [Text](./Text.md) - 文本
- [Button](./Button.md) - 按钮
- [Checkbox](./Checkbox.md) - 复选框
- [Slider](./Slider.md) - 滑块
- [Functiongraph](./Functiongraph.md) - 函数图像
