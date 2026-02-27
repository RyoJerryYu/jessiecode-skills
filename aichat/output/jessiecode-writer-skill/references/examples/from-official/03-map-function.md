# 映射函数 (Map Function)

## 图形描述

本示例演示了 JessieCode 中的映射函数（map）语法。映射函数是一种简洁定义数学函数的方式，支持求值、微分等操作。

## JessieCode 代码

```js
//e = 3 * (sin(2) + cos(1));
//f = map (x) -> 3 * (sin(x) + cos(x));
// doesn't work
//g = map (x) -> 3 * (sin(x) + cos(x)) > 3;
f = map (x) -> 3 + x;
h = D(f, x);
y = f(4);
```

## 知识点

1. **映射函数语法**：`map (x) -> expression` 是定义函数的简洁方式
2. **函数微分**：使用 `D(f, x)` 对函数 f 关于变量 x 求导
3. **函数求值**：使用 `f(4)` 对函数在 x=4 处求值
4. **注释语法**：使用 `//` 进行单行注释
5. **变量赋值**：使用 `=` 将函数、表达式结果赋值给变量

## 涉及元素

- JessieCode 语法：映射函数、函数微分、函数求值
- [Functiongraph](../../03-api/Functiongraph.md) - 函数图像（可使用 plot 绘制上述函数）
