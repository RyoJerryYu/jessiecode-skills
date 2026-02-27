# JessieCode 语法规则参考

本文档描述了 JessieCode 脚本语言的完整语法规则，供 `jessiecode-writer` 技能使用。

---

## 1. 数据类型 (Datatypes)

### 1.1 布尔值 (Boolean)

```js
true   // 真
false  // 假
```

**注意**：布尔值大小写不敏感，`TRUE`、`True`、`tRuE` 都是有效的布尔常量。

### 1.2 字符串 (Strings)

```js
'hello world'           // 基本字符串
'world\'s best'         // 使用反斜杠转义引号
'line1\nline2'          // 支持转义字符
```

**规则**：
- 字符串必须使用单引号 `'` 包裹
- 引号 inside 字符串需要使用反斜杠 `\` 转义
- 支持标准转义字符：`\n` (换行), `\t` (制表符), `\\` (反斜杠), `\'` (单引号)

### 1.3 数字 (Number)

```js
42          // 整数
3.14159     // 浮点数
-17.5       // 负数
0.001       // 小数
```

**规则**：
- 对应 JavaScript 的 `number` 类型
- 支持整数、浮点数、负数
- 不支持八进制、十六进制字面量

### 1.4 对象 (Objects)

```js
// 对象字面量
obj = <<
    property: 'string',
    prop: 42,
    method: function (x) {
        return x * x;
    }
>>;

// 使用对象
sixteen = obj.method(4);  // 返回 16
color = obj.property;     // 返回 'string'
```

**规则**：
- 对象使用 `<< >>` 符号创建（而非 JavaScript 的 `{}`）
- 属性之间用逗号分隔
- 支持嵌套对象和函数

### 1.5 函数 (Functions)

```js
// 函数声明
f = function (a, b, c) {
    return a + b + c;
};

// 使用函数
result = f(1, 2, 3);  // 返回 6

// 无参函数
g = function () {
    return 42;
};
```

**规则**：
- 使用 `function` 关键字声明
- 参数列表用圆括号 `()` 包裹
- 函数体用花括号 `{}` 包裹

---

## 2. 运算符 (Operators)

### 2.1 逻辑运算符

| 运算符 | 描述 | 示例 |
|:-------|:-----|:-----|
| `||` | 逻辑或 | `a || b` |
| `&&` | 逻辑与 | `a && b` |
| `!` | 逻辑非 | `!a` |

### 2.2 算术运算符

| 运算符 | 描述 | 示例 |
|:-------|:-----|:-----|
| `+` | 加法 | `a + b` |
| `-` | 减法或一元负号 | `a - b`, `-a` |
| `*` | 乘法 | `a * b` |
| `/` | 除法 | `a / b` |
| `%` | 取模 | `a % b` |
| `^` | 幂运算 | `a ^ b` |

### 2.3 赋值运算符

| 运算符 | 描述 | 示例 |
|:-------|:-----|:-----|
| `=` | 赋值 | `a = 5` |

**注意**：JessieCode 仅支持简单的 `=` 赋值，不支持 `+=`、`-=` 等复合赋值运算符。

### 2.4 比较运算符

| 运算符 | 描述 | 示例 |
|:-------|:-----|:-----|
| `==` | 等于 | `a == b` |
| `!=` | 不等于 | `a != b` |
| `<` | 小于 | `a < b` |
| `>` | 大于 | `a > b` |
| `<=` | 小于等于 | `a <= b` |
| `>=` | 大于等于 | `a >= b` |
| `~=` | 约等于（用于浮点数比较） | `a ~= b` |

### 2.5 条件运算符（三元运算符）

```js
// 语法
condition ? expr1 : expr2

// 示例
maxValue = (a > b) ? a : b;
grade = (score >= 60) ? 'pass' : 'fail';
```

### 2.6 字符串运算符

| 运算符 | 描述 | 示例 |
|:-------|:-----|:-----|
| `+` | 字符串连接 | `'Hello, ' + 'World'` → `'Hello, World'` |

### 2.7 成员访问运算符

| 运算符 | 描述 | 示例 |
|:-------|:-----|:-----|
| `.` | 访问对象的属性和方法 | `obj.property`, `point.X()` |

---

## 3. 注释 (Comments)

```js
// 这是单行注释
// 以 // 开头的整行内容都会被忽略

A = point(1, 2);  // 行尾注释也是允许的
```

**规则**：
- 仅支持单行注释（`//` 风格）
- 不支持多行注释（`/* */` 风格）

---

## 4. 控制结构 (Control Structures)

### 4.1 条件语句 (If)

```js
// 基本形式
if (condition) {
    // 语句块
}

// 带 else
if (condition) {
    // 语句块 1
} else {
    // 语句块 2
}

// 带 else if
if (condition1) {
    // 语句块 1
} else if (condition2) {
    // 语句块 2
} else {
    // 语句块 3
}
```

### 4.2 While 循环

```js
while (condition) {
    // 循环体
}

// 示例
i = 0;
while (i < 10) {
    i = i + 1;
}
```

### 4.3 Do-While 循环

```js
do {
    // 循环体
} while (condition);

// 示例
i = 0;
do {
    i = i + 1;
} while (i < 10);
```

### 4.4 For 循环

```js
for (initialization; condition; increment) {
    // 循环体
}

// 示例
for (i = 0; i < 10; i = i + 1) {
    // 执行 10 次
}
```

**注意**：JessieCode 的 for 循环语法与 JavaScript 完全相同。

---

## 5. 预定义常量 (Predefined Constants)

| 常量名 | 描述 | 近似值 |
|:-------|:-----|:-------|
| `$board` | 当前画布的引用 | - |
| `PI` | 圆周率 π | 3.141592653589793 |
| `EULER` | 欧拉数 e | 2.718281828459045 |
| `LN2` | 2 的自然对数 | 0.6931471805599453 |
| `LN10` | 10 的自然对数 | 2.302585092994046 |
| `LOG2E` | 以 2 为底的 e 的对数 | 1.4426950408889634 |
| `LOG10E` | 以 10 为底的 e 的对数 | 0.4342944819032518 |
| `SQRT2` | 2 的平方根 | 1.4142135623730951 |
| `SQRT1_2` | 1/2 的平方根 | 0.7071067811865476 |

---

## 6. 预定义函数 (Predefined Functions)

### 6.1 数学函数

所有 JavaScript `Math` 对象的函数都可用：

| 函数 | 描述 | 示例 |
|:-----|:-----|:-----|
| `sin(x)` | 正弦 | `sin(PI/2)` → 1 |
| `cos(x)` | 余弦 | `cos(0)` → 1 |
| `tan(x)` | 正切 | `tan(PI/4)` → 1 |
| `asin(x)` | 反正弦 | - |
| `acos(x)` | 反余弦 | - |
| `atan(x)` | 反正切 | - |
| `sinh(x)` | 双曲正弦 | - |
| `cosh(x)` | 双曲余弦 | - |
| `abs(x)` | 绝对值 | `abs(-5)` → 5 |
| `sqrt(x)` | 平方根 | `sqrt(16)` → 4 |
| `cbrt(x)` | 立方根 | `cbrt(27)` → 3 |
| `log(x)` 或 `ln(x)` | 自然对数 | `log(EULER)` → 1 |
| `log(x, b)` | 以 b 为底的对数 | `log(100, 10)` → 2 |
| `log2(x)` 或 `lb(x)` | 以 2 为底的对数 | - |
| `log10(x)` 或 `ld(x)` | 以 10 为底的对数 | `log10(1000)` → 3 |
| `exp(x)` | e 的 x 次幂 | `exp(1)` → EULER |
| `pow(b, e)` | b 的 e 次幂 | `pow(2, 3)` → 8 |
| `ceil(x)` | 向上取整 | `ceil(3.2)` → 4 |
| `floor(x)` | 向下取整 | `floor(3.8)` → 3 |
| `round(x)` | 四舍五入 | `round(3.5)` → 4 |
| `max(a, b, c, ...)` | 最大值 | `max(1, 5, 3)` → 5 |
| `min(a, b, c, ...)` | 最小值 | `min(1, 5, 3)` → 1 |
| `random(max)` | 随机数 (0 到 max) | `random()` 或 `random(100)` |
| `factorial(n)` | 阶乘 n! | `factorial(5)` → 120 |
| `trunc(v, p)` | 截断小数 | `trunc(3.14159, 2)` → 3.14 |

### 6.2 几何函数

| 函数 | 描述 | 示例 |
|:-----|:-----|:-----|
| `V(s)` | 获取元素的值（如滑块、角度） | `V(slider1)` |
| `L(s)` | 计算线段的长度 | `L(segment1)` |
| `X(P)` | 获取点 P 的 x 坐标 | `X(pointA)` |
| `Y(P)` | 获取点 P 的 y 坐标 | `Y(pointA)` |
| `dist(P, Q)` | 计算两点之间的距离 | `dist(A, B)` |
| `deg(A, B, C)` | 计算角度（度） | `deg(A, B, C)` |
| `rad(A, B, C)` | 计算角度（弧度） | `rad(A, B, C)` |
| `$(id)` | 根据 ID 查找元素 | `$('pointA')` |

### 6.3 $board 方法

| 方法 | 描述 | 示例 |
|:-----|:-----|:-----|
| `update()` | 更新所有依赖并重绘 | `$board.update()` |
| `on(event, handler, context)` | 注册事件处理器 | `$board.on('down', handler)` |
| `off(event, handler)` | 注销事件处理器 | `$board.off('down')` |
| `setView(array, keepaspectratio)` | 更改视口 | `$board.setView([-2, 3, 2, -3])` |
| `setBoundingbox(array, keepaspectratio)` | 设置边界框 | `$board.setBoundingbox([-5, 5, 5, -5])` |
| `migratePoint(P, Q)` | 用点 Q 替换点 P | `$board.migratePoint(A, B)` |
| `colorblind(type)` | 模拟色盲视图 | `$board.colorblind('protanopia')` |

**色盲类型**：`protanopia`（红色盲）、`tritanopia`（蓝色盲）、`deuteranopia`（绿色盲）

---

## 7. 元素创建 (Element Creation)

### 7.1 基本语法

```js
// 创建点
A = point(1, 2);

// 创建线段
s = segment(A, B);

// 创建直线
l = line(A, B);

// 创建圆
c = circle(A, B);  // 圆心 A，经过点 B
```

### 7.2 带属性的元素创建

```js
// 使用 << >> 语法设置属性
A = point(1, 2) <<
    strokeColor: 'red',
    fillColor: 'black',
    size: 5,
    face: '[]'
>>;

// 嵌套属性
pol = polygon(A, B, C) <<
    fillColor: '#FFFF00',
    borders: <<
        strokeWidth: 2,
        strokeColor: '#009256'
    >>
>>;
```

### 7.3 常用元素函数

| 元素类型 | 函数名 | 参数示例 |
|:--------|:------|:--------|
| 点 | `point(x, y)` | `point(1, 2)` |
| 线段 | `segment(A, B)` | `segment(pointA, pointB)` |
| 直线 | `line(A, B)` | `line(pointA, pointB)` |
| 射线 | `halfline(A, B)` | `halfline(pointA, pointB)` |
| 圆 | `circle(center, point)` | `circle(O, A)` |
| 三角形 | `polygon(A, B, C)` | `polygon(A, B, C)` |
| 中点 | `midpoint(A, B)` | `midpoint(A, B)` |
| 交点 | `intersection(el1, el2, index)` | `intersection(l1, l2, 0)` |
| 垂线 | `perpendicular(line, point)` | `perpendicular(l, P)` |
| 平行线 | `parallel(line, point)` | `parallel(l, P)` |
| 滑块 | `slider(min, max, step)` | `slider(0, 10, 0.1)` |
| 文本 | `text(x, y, content)` | `text(1, 2, 'Hello')` |
| 角度 | `angle(A, B, C)` | `angle(A, B, C)` |

---

## 8. 访问元素 (Accessing Elements)

### 8.1 通过变量赋值

```js
A = point(1, 2);
A.strokeColor = '#123456';
A.size = 10;
```

### 8.2 通过 $() 函数

```js
// 创建时指定 ID
point(1, 2) << id: 'foo', name: 'bar' >>;

// 通过 $() 查找
$('foo').strokeColor = '#654321';
```

### 8.3 通过 ID 直接访问

```js
point(1, 2) << id: 'foo' >>;
foo.strokeColor = '#f00f00';  // 直接使用 ID 作为变量名
```

**限制**：仅当 `foo` 未被用作变量名时才有效。

### 8.4 通过名称访问

```js
point(1, 2) << id: 'foo', name: 'bar' >>;
bar.strokeColor = '#541541';  // 使用 name 属性
```

**限制**：仅当 `bar` 未被用作变量名时才有效。

---

## 9. 元素属性和方法

### 9.1 属性设置

```js
// 设置点的大小
A.size = 10;

// 设置点的样式
A.face = '[]';

// 设置颜色
A.strokeColor = 'red';
A.fillColor = 'blue';
```

### 9.2 子元素访问

```js
// 访问点的标签
A.label.strokeColor = 'red';

// 访问滑块的基线
slider1.baseline.strokeWidth = 2;
```

### 9.3 可用方法

**所有元素**：
- `setLabelText(text)` - 设置标签文本

**点 (Point)**：
- `move(dx, dy)` - 移动点
- `glide(line)` - 使点在直线上滑动
- `free()` - 释放点
- `X()` - 获取 x 坐标
- `Y()` - 获取 y 坐标

**滑点 (Glider)**：
- 继承点的所有方法
- `setPosition(position)` - 设置位置

**文本 (Text)**：
- `setText(text)` - 设置文本内容
- `move(dx, dy)` - 移动文本
- `free()` - 释放文本

**滑块 (Slider)**：
- `Value()` - 获取当前值

**角度 (Angle)**：
- `Value()` - 获取角度值

---

## 10. 代码示例

### 10.1 基本图形

```js
// 创建一个三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

triangle = polygon(A, B, C);
```

### 10.2 带样式的图形

```js
// 定义样式对象
redStyle = <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 5
>>;

// 应用样式
A = point(-2, 0) redStyle;
B = point(2, 0) redStyle;
```

### 10.3 动态图形

```js
// 创建滑块
a = slider(0, 5, 0.1);

// 创建依赖于滑块的点
P = point(a, sin(a));

// 创建轨迹
t = locus(P, a);
```

### 10.4 使用函数

```js
// 定义函数
f = function (x) {
    return x * x - 2 * x + 1;
};

// 绘制函数图像
graph = functiongraph(f, -5, 5);
```

---

## 11. 语法注意事项

### 11.1 分号

```js
// 语句通常以分号结束（建议）
A = point(1, 2);
B = point(3, 4);
```

### 11.2 大小写敏感

```js
// 变量名大小写敏感
myPoint = point(1, 2);
mypoint = point(3, 4);  // 这是两个不同的变量

// 但布尔常量大小写不敏感
flag1 = true;
flag2 = TRUE;  // 有效
flag3 = TrUe;  // 也有效
```

### 11.3 作用域

```js
// 全局变量
globalVar = 42;

// 函数内的局部变量
myFunc = function () {
    localVar = 100;  // 在函数内创建
    return localVar;
};
```

---

## 12. 常见错误

### 12.1 错误的对象语法

```js
// 错误：使用 {} 而非 << >>
A = point(1, 2) { strokeColor: 'red' };  // 错误！

// 正确
A = point(1, 2) << strokeColor: 'red' >>;  // 正确
```

### 12.2 错误的属性访问

```js
// 错误：使用方括号
A['strokeColor'] = 'red';  // 不支持！

// 正确：使用点号
A.strokeColor = 'red';  // 正确
```

### 12.3 忘记函数括号

```js
// 错误
A = point 1, 2;  // 错误！

// 正确
A = point(1, 2);  // 正确
```
