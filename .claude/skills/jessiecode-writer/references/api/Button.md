# Button 按钮

## 描述

按钮是包含 HTML 按钮标签的文本元素。点击按钮可以触发 JavaScript 或 JessieCode 代码。

## JessieCode 语法

```js
// 基本语法
btn = button(x, y, label, handler);

// handler 可以是 JavaScript 函数或 JessieCode 字符串
btn = button(1, 2, "Click me", function() {
    // JavaScript 代码
});

// 使用 JessieCode 字符串
btn = button(1, 2, "Click", "$('point1').moveTo([1, 1]);");
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | 按钮左下角的 x 坐标 |
| y | Number/Function | 按钮左下角的 y 坐标 |
| label | String/Function | 按钮标签 |
| handler | Function/String (可选) | 点击时执行的函数或 JessieCode 字符串 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `cssClass` | String | '' | CSS 类名 |
| `cssStyle` | String | '' | CSS 样式 |
| `disabled` | Boolean | false | 是否禁用 |
| `display` | String | 'html' | 显示方式（必须为 'html'） |
| `visible` | Boolean | true | 是否可见 |

### 子元素

| 子元素 | 描述 |
|--------|------|
| `rendNodeButton` | 底层 HTML 按钮元素 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `setText(text)` | text: String | 设置按钮文本 |
| `setDisabled(disabled)` | disabled: Boolean | 设置禁用状态 |

## 示例

### 1. 创建基本按钮

```js
// 创建按钮
btn = button(1, 2, "Click Me", function() {
    alert("Button clicked!");
});
```

### 2. 移动点的按钮

```js
// 创建点
P = point(0.5, 0.5);

// 移动点的按钮
moveBtn = button(1, 2, "Move Point", function() {
    P.moveTo([P.X() + 0.5, P.Y() + 0.5], 1000);
});

// 使用 JessieCode 字符串
moveBtn2 = button(1, 3, "Move with JessieCode",
    "$('point').moveTo([1, 1], 500);"
) << id: 'point' >>;
```

### 3. 切换按钮

```js
// 创建切换按钮
toggleBtn = button(-2, -2, "Off", function() {
    // 切换状态
    toggleBtn.value = !toggleBtn.value;

    // 更新按钮文本
    if (toggleBtn.value) {
        toggleBtn.rendNodeButton.innerHTML = "On";
    } else {
        toggleBtn.rendNodeButton.innerHTML = "Off";
    }
});

// 初始化
toggleBtn.value = false;

// 根据按钮状态显示/隐藏点
P = point(2, -2) <<
    visible: function() { return toggleBtn.value; }
>>;
```

### 4. 多个按钮控制

```js
// 创建点
P = point(0, 0);

// 方向按钮
upBtn = button(0, 3, "↑ Up", function() {
    P.moveTo([P.X(), P.Y() + 0.5], 200);
});

downBtn = button(0, 1, "↓ Down", function() {
    P.moveTo([P.X(), P.Y() - 0.5], 200);
});

leftBtn = button(-2, 2, "← Left", function() {
    P.moveTo([P.X() - 0.5, P.Y()], 200);
});

rightBtn = button(2, 2, "Right →", function() {
    P.moveTo([P.X() + 0.5, P.Y()], 200);
});
```

### 5. 重置按钮

```js
// 创建可移动的点
A = point(1, 1);
B = point(2, 2);
C = point(3, 1);

// 保存初始位置
initialA = [1, 1];
initialB = [2, 2];
initialC = [3, 1];

// 重置按钮
resetBtn = button(0, 4, "Reset", function() {
    A.moveTo(initialA, 500);
    B.moveTo(initialB, 500);
    C.moveTo(initialC, 500);
});
```

### 6. 动画控制按钮

```js
// 圆上的动点
c = circle(point(0, 0), 2);
P = glider(c);

// 开始/停止按钮
playBtn = button(-3, 3, "Play", function() {
    P.startAnimation(1, 100, 50, -1);  // 无限循环
    playBtn.rendNodeButton.innerHTML = "Playing...";
    playBtn.disabled = true;
});

stopBtn = button(1, 3, "Stop", function() {
    P.stopAnimation();
    playBtn.rendNodeButton.innerHTML = "Play";
    playBtn.disabled = false;
});
```

### 7. 动态标签按钮

```js
// 计数器
counter = 0;

// 计数按钮
countBtn = button(0, 0, "Count: 0", function() {
    counter = counter + 1;
    countBtn.rendNodeButton.innerHTML = "Count: " + counter;
});

// 重置计数
resetBtn = button(0, -1, "Reset", function() {
    counter = 0;
    countBtn.rendNodeButton.innerHTML = "Count: 0";
});
```

### 8. 自定义样式按钮

```js
// 需要 CSS 支持
// .mybutton > button {
//     background-color: #04AA6D;
//     color: white;
//     padding: 10px 20px;
//     font-size: 16px;
// }

styledBtn = button(0, 0, "Styled Button", function() {
    alert("Styled button clicked!");
}) <<
    cssClass: 'mybutton',
    highlightCssClass: 'mybutton'
>>;
```

### 9. 条件按钮

```js
// 输入框和按钮组合
input = input(0, 2, "default", "Enter:") <<
    cssStyle: 'width: 150px'
>>;

submitBtn = button(0, 1, "Submit", function() {
    value = input.rendNodeInput.value;
    text(0, 0, "You entered: " + value);
});
```

### 10. 函数变换控制

```js
// 原函数
f = function(x) { return x * x; };
original = functiongraph(f, -3, 3) << strokeColor: 'black' >>;

// 变换参数
h = 0;  // 水平平移
k = 0;  // 垂直平移

// 变换后的函数
transformed = functiongraph(
    function(x) { return f(x - h) + k; },
    -3, 3
) << strokeColor: 'red', dash: 1 >>;

// 控制按钮
moveRightBtn = button(-4, 4, "→", function() {
    h = h + 0.5;
    $board.update();
});

moveLeftBtn = button(-4.5, 4, "←", function() {
    h = h - 0.5;
    $board.update();
});

moveUpBtn = button(-3.5, 4, "↑", function() {
    k = k + 0.5;
    $board.update();
});

moveDownBtn = button(-3.5, 3.5, "↓", function() {
    k = k - 0.5;
    $board.update();
});
```

## 注意事项

1. **HTML 模式**：按钮必须使用 `display: 'html'`（默认）
2. **CSS 样式**：需要通过 `.cssClass > button` 选择器设置按钮样式
3. **JavaScript 访问**：可以通过 `rendNodeButton` 访问底层 HTML 按钮元素
4. **禁用状态**：使用 `disabled` 属性或方法控制按钮是否可用
5. **事件处理**：handler 可以是 JavaScript 函数或 JessieCode 字符串

## 相关元素

- [Text](./Text.md) - 文本（父类）
- [Input](./Input.md) - 输入框
- [Checkbox](./Checkbox.md) - 复选框
- [Slider](./Slider.md) - 滑块
