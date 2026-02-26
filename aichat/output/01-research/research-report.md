# JessieCode 调研报告

## 1. JessieCode 概述

### 1.1 背景与历史

JessieCode 是一个专门为 JSXGraph 设计的脚本语言，由 Michael Gerhäuser 和 Alfred Wassermann 于 2011-2021 年开发。它的设计目标是为 JSXGraph 提供一个安全的脚本接口。

### 1.2 特点

- **安全性**：JessieCode 类似于 JavaScript，但**防止访问 DOM**，这使得它可以在社区驱动的网站中安全使用
- **简洁性**：语法简洁，专为几何图形创建而设计
- **交互性**：支持创建交互式数学图形
- **依赖**：需要 JSXGraph 库才能运行

### 1.3 使用场景

- 数学教育网站
- 交互式几何图形展示
- 在线数学教材
- 动态数学可视化

## 2. JessieCode 与 JSXGraph 的关系

### 2.1 依赖关系

```
JessieCode → JSXGraph → HTML5 Canvas/SVG
```

JessieCode 是 JSXGraph 的脚本语言层，它提供了更简洁的语法来创建和操作 JSXGraph 元素。

### 2.2 工作原理

1. JessieCode 代码被解析为抽象语法树 (AST)
2. AST 被编译为 JavaScript 代码
3. JavaScript 代码调用 JSXGraph API 创建图形元素
4. JSXGraph 负责在画布上渲染图形

### 2.3 核心类

- `JXG.JessieCode`：主要的解析器和解释器类
- `JXG.Board`：画布对象，通过 `$board` 访问

## 3. JessieCode 语法特性

### 3.1 数据类型

| 类型 | 描述 | 示例 |
|------|------|------|
| Boolean | 布尔值 | `true`, `false` (大小写不敏感) |
| String | 字符串 | `'hello'`, `'world\'s'` |
| Number | 数字 | `42`, `3.14` |
| Object | 对象 | `<< property: 'value' >>` |
| Function | 函数 | `function(x) { return x*x; }` |

### 3.2 运算符

**逻辑运算符**：`||`, `&&`, `!`

**算术运算符**：`+`, `-`, `*`, `/`, `%`, `^` (幂运算)

**比较运算符**：`==`, `!=`, `<`, `>`, `<=`, `>=`, `~=` (约等于)

**赋值运算符**：`=`

**三元运算符**：`bool ? expr1 : expr2`

**成员访问**：`.` (访问对象属性)

### 3.3 控制结构

```js
// 条件语句
if (condition) {
    // ...
} else if (otherCondition) {
    // ...
} else {
    // ...
}

// 循环
while (condition) { /* ... */ }
do { /* ... */ } while (condition);
for (i = 0; i < 10; i = i + 1) { /* ... */ }
```

### 3.4 预定义常量

| 常量 | 描述 |
|------|------|
| `$board` | 当前画布引用 |
| `PI` | 圆周率 π |
| `EULER` | 欧拉数 e |
| `LN2`, `LN10` | 2 和 10 的自然对数 |
| `LOG2E`, `LOG10E` | 以 2 和 10 为底的 E 的对数 |
| `SQRT2`, `SQRT1_2` | √2 和 √(1/2) |

### 3.5 预定义函数

**数学函数**：`sin`, `cos`, `tan`, `asin`, `acos`, `atan`, `abs`, `sqrt`, `log`, `exp`, `floor`, `ceil`, `round`, `max`, `min`, `random`, `factorial` 等

**几何函数**：
- `V(s)` - 获取元素值（如滑块）
- `L(s)` - 计算线段长度
- `X(P)`, `Y(P)` - 获取点坐标
- `dist(P, Q)` - 计算两点距离
- `deg(A, B, C)` - 计算角度（度）
- `rad(A, B, C)` - 计算角度（弧度）
- `$(id)` - 根据 ID 查找元素

**$board 方法**：
- `update()` - 更新并重绘
- `on(event, handler)` - 注册事件
- `off(event)` - 注销事件
- `setView(array)` - 设置视口
- `setBoundingbox(array)` - 设置边界框

## 4. 元素创建与操作

### 4.1 创建元素

```js
// 基本语法
A = point(1, 2);

// 带属性
A = point(1, 2) <<
    strokeColor: 'red',
    face: '[]',
    size: 7,
    fillColor: 'black'
>>;
```

### 4.2 访问元素

```js
// 通过变量
A = point(1, 2);
A.strokeColor = '#123456';

// 通过 ID
point(1, 2) << id: 'foo' >>;
$('foo').strokeColor = '#654321';

// 通过名称
point(1, 2) << id: 'foo', name: 'bar' >>;
bar.strokeColor = '#f00f00';
```

### 4.3 元素方法

可用方法包括：
- `setLabelText()` - 所有元素
- `move()`, `glide()`, `free()`, `X()`, `Y()` - 点
- `setPosition()` - 滑点
- `setText()` - 文本
- `Value()` - 滑块、角度

## 5. 技术实现

### 5.1 编译流程

```
.bnf 文件 → Jison 解析器生成器 → JessieCode 解析器 → 与解释器合并 → jessiecode.js
```

### 5.2 所需工具

- `jison` - 解析器生成器
- `uglify-js` - 代码压缩
- `jshint/jslint` - 代码检查 (可选)

### 5.3 许可证

双许可证：
- GNU LGPL v3+
- MIT License

## 6. 总结

JessieCode 是一个专为数学教育设计的领域特定语言 (DSL)，它：

1. **安全**：限制 DOM 访问，适合用户生成内容
2. **简洁**：用少量代码创建复杂几何图形
3. **强大**：完整支持 JSXGraph 的所有功能
4. **易学**：语法类似 JavaScript，降低学习门槛

这些特性使 JessieCode 成为创建交互式几何图形的理想选择，特别适合教育和协作场景。
