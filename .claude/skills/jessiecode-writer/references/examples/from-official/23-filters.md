# 过滤器/字符串处理示例 / Filters and String Processing Example

## 图形描述

此示例是一个综合性的 JessieCode 语法演示，展示了各种数据类型和语法结构：
- 单行和多行注释
- 空字符串（单引号和双引号）
- Unicode 字符（希腊字母 α）
- 包含引号的字符串
- 数组字面量
- 布尔值和数值运算
- 对象字面量及其属性访问

这是一个全面的语法测试示例，展示了 JessieCode 对 JavaScript 各种语法特性的支持。

## JessieCode 代码

```javascript
// single line comment
'';
"";
alpha = 'α';
dq = "";
sqsidq = "'";
dqs = "double quote strings, yay!'";
a = [1, 2, 3, 4];
e = 1 + true;
g = e + ''; // end of line comment
f = '' + '';
o = <<>>;
o.test = 3;
/*
multiline comment
*/
```

## 知识点

1. **单行注释**：使用 `//` 添加行内或行首注释
2. **多行注释**：使用 `/* */` 添加跨行注释
3. **空字符串**：`''` 和 `""` 都表示空字符串
4. **Unicode 支持**：字符串可直接包含 Unicode 字符（如 `α`）
5. **引号转义**：双引号字符串可包含单引号，无需转义
6. **数组字面量**：使用 `[1, 2, 3, 4]` 语法定义数组
7. **类型转换**：`1 + true` 中布尔值转换为数字（结果为 2）
8. **字符串拼接**：使用 `+` 连接字符串
9. **对象字面量**：使用 `<< >>` 定义空对象
10. **属性访问**：使用点语法 `o.test` 访问/设置对象属性

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `//` `/* */` | JavaScript 注释语法 | [MDN - Comments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#comments) |
| `''` `""` | 字符串字面量 | [MDN - String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) |
| `[]` | 数组字面量 | [MDN - Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) |
| `<< >>` | JessieCode 对象字面量语法 | [JessieCode API](https://jsxgraph.org/docs/symbols/JessieCode.html) |
| 类型转换 | JavaScript 隐式类型转换规则 | [MDN - Type Conversion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_Types#type_conversion) |

---

*来源：JessieCode 官方示例 - filters.html*
