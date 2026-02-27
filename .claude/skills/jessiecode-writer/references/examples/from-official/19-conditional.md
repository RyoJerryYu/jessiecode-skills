# 条件类型示例 / Conditional Type Example

## 图形描述

此示例演示 JessieCode 中的条件表达式和布尔类型处理。代码展示了：
- 布尔值的日志输出
- 布尔变量的赋值和使用
- 三元条件运算符的使用
- 函数内部的条件判断

这是一个关于条件逻辑和类型转换的基础示例，展示了如何在 JessieCode 中处理布尔值和条件表达式。

## JessieCode 代码

```javascript
$log(true);
flag = true;
res = flag;
$log(flag);
res = flag;
res = (flag == true? 'true' : 'false');
$log(res);
f = function(x) {
    return x < 0 ? 'neg' : 'pos';
};
```

## 知识点

1. **布尔字面量**：`true` 和 `false` 是 JessieCode 的布尔值
2. **变量赋值**：使用 `=` 进行变量赋值
3. **日志输出**：`$log()` 可输出布尔值
4. **条件运算符**：`condition ? expr1 : expr2` 三元运算符语法
5. **比较运算**：`==` 用于相等性比较
6. **字符串返回**：条件表达式可返回字符串
7. **函数内条件**：函数内部可使用条件表达式进行判断
8. **数值比较**：`<` 用于数值大小比较

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `$log()` | JessieCode 内置的日志输出函数 | [JessieCode API - Output](https://jsxgraph.org/docs/symbols/JessieCode.html) |
| `true/false` | 布尔字面量 | [MDN - Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) |
| `?:` | 三元条件运算符 | [MDN - Conditional Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) |
| `function` | JavaScript 函数定义 | [MDN - function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function) |

---

*来源：JessieCode 官方示例 - conditional.html*
