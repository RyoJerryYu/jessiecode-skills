# Checkbox 复选框

<!-- USAGE_FREQUENCY: core -->

## 描述

复选框元素是一个包含 HTML 复选框标签的文本元素。它允许用户通过勾选/取消勾选来控制布尔状态，常用于创建交互式图表中的开关控制。

## JessieCode 语法

```js
// 基本语法 - 创建复选框
c = checkbox(x, y, '标签文本');

// 带属性创建
c = checkbox(0, 3, '显示网格') <<
    checked: true,
    withLabel: true
>>;

// 复选框控制其他元素
c = checkbox(0, 4, '显示点');
P = point(1, 1) <<
    visible: function() { return c.Value(); }
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | 复选框左下角的 x 坐标（固定值或函数） |
| y | Number/Function | 复选框左下角的 y 坐标（固定值或函数） |
| label | String/Function | 复选框的标签文本 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `checked` | Boolean | false | 控制复选框是否被勾选 |
| `disabled` | Boolean | false | 控制复选框是否被禁用 |
| `cssClass` | String | '' | CSS 类名，用于自定义样式 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | true | 是否显示标签 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | 无 | 返回复选框的状态（勾选返回 true，否则返回 false） |
| `setText(text)` | text: String | 设置复选框的标签文本 |

## 示例

### 1. 创建基本复选框

```js
// 在位置 [0, 3] 创建复选框
c = checkbox(0, 3, 'Change Y');

// 创建一个点，其 Y 坐标由复选框控制
P = point(0.5, function() {
    y = 0.5;
    if (c.Value()) {
        y += 0.5;
    }
    return y;
});
```

### 2. 复选框控制元素可见性

```js
// 创建复选框
showPoint = checkbox(0, 4, '显示点');

// 创建一个点，其可见性由复选框控制
P = point(2, 2) <<
    visible: function() { return showPoint.Value(); }
>>;
```

### 3. 复选框控制点的移动

```js
// 创建复选框
movePoint = checkbox(0, 4, '移动点');

// 创建点
P = point(1, 1);

// 添加事件监听器
P.on('change', function() {
    if (movePoint.Value()) {
        P.moveTo([4, 1]);
    } else {
        P.moveTo([1, 1]);
    }
});
```

### 4. 默认勾选的复选框

```js
// 创建默认勾选的复选框
c = checkbox(0, 3, '启用网格') <<
    checked: true
>>;

// 根据复选框状态显示/隐藏网格
grid = grid() <<
    visible: function() { return c.Value(); }
>>;
```

### 5. 复选框与其他输入元素组合

```js
// 创建输入框
i1 = input(1, 5, 'sin(x)', 'f(x)=') <<
    cssStyle: 'width:4em',
    maxlength: 2
>>;

// 创建复选框
c1 = checkbox(1, 3, '标签 1');

// 创建按钮，点击后更改文本
b1 = button(1, 1, '更改文本', function() {
    i1.setText('g(x)=');
    i1.set('cos(x)');
    c1.setText('标签 2');
    b1.setText('文本已更改');
}) <<
    cssStyle: 'width:200px'
>>;
```

### 6. 复选框控制函数图像

```js
// 创建复选框控制正弦函数显示
showSin = checkbox(0, 4, 'sin(x)');
showCos = checkbox(0, 3, 'cos(x)');

// 创建函数图像
sinGraph = functiongraph(function(x) { return sin(x); }) <<
    visible: function() { return showSin.Value(); },
    strokeColor: 'red'
>>;

cosGraph = functiongraph(function(x) { return cos(x); }) <<
    visible: function() { return showCos.Value(); },
    strokeColor: 'blue'
>>;
```

### 7. 复选框控制轨迹显示

```js
// 创建滑块
t = slider(0, 2*PI, 0.01);

// 创建动点
P = point(function() { return cos(V(t)); },
          function() { return sin(V(t)); });

// 创建轨迹
trace = locus(P) <<
    visible: function() { return checkbox(0, 4, '显示轨迹').Value(); }
>>;
```

## 注意事项

1. **HTML 元素**：复选框是 HTML 元素，不是 SVG 图形，因此位置使用 board 坐标系统
2. **访问 HTML 节点**：可以通过 `element.rendNodeCheckbox` 访问底层的 HTML 复选框元素
3. **事件监听**：可以为复选框添加事件监听器，如 'change' 事件
4. **CSS 样式**：使用 `cssClass` 属性设置 CSS 类，选择器形式为 `.mycheck > checkbox { ... }`
5. **值获取**：使用 `Value()` 方法获取复选框的当前状态

## 相关元素

- [Button](./Button.md) - 按钮
- [Input](./Input.md) - 输入框
- [Slider](./Slider.md) - 滑块
- [Text](./Text.md) - 文本
