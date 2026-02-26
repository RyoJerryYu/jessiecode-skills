# 作用域链示例 / Scope Chain Example

## 图形描述

此示例演示 JavaScript/JessieCode 中的作用域链和闭包概念。代码展示了：
- 全局变量的定义和访问
- 函数内部的局部变量
- 嵌套函数对外部变量的访问
- 闭包的创建和使用
- 不同闭包实例维护各自的状态

这是一个关于 JavaScript 核心概念——作用域链和闭包的重要示例。

## JessieCode 代码

```javascript
z = 1;
h = function (x) {
    y = 2;
    return x + y + z;
};
f = function () {
    y = 4;
    return function (x) {
        return y+z+x;
    };
};
q = function (x) {
    return function () {
        return x;
    };
};
w = q(10);
e = q(20);
r = w();
t = e();
```

## 知识点

1. **全局作用域**：变量 `z` 在全局作用域定义，可被所有函数访问
2. **函数作用域**：函数内部定义的变量（如 `y`）在函数内可见
3. **词法作用域**：内层函数可访问外层函数的变量
4. **闭包**：函数返回内层函数，内层函数保留对外部变量的引用
5. **闭包实例**：`q(10)` 和 `q(20)` 创建两个独立的闭包实例
6. **状态保持**：每个闭包实例维护各自捕获的变量值
7. **函数调用**：`w()` 和 `e()` 分别调用不同的闭包实例
8. **变量捕获**：闭包捕获的是词法环境中的变量引用

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `function` | JavaScript 函数定义语法 | [MDN - function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function) |
| 作用域链 | JavaScript 变量查找机制 | [MDN - Scope Chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) |
| 闭包 | 函数捕获外部作用域的变量 | [MDN - Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) |

---

*来源：JessieCode 官方示例 - scopechain.html*
