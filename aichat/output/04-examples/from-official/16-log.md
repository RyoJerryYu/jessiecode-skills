# 日志输出示例 / Log Output Example

## 图形描述

此示例演示 JessieCode 中的日志输出功能。代码定义了名为 `cerise` 的视觉属性对象（包含描边颜色和填充颜色），然后通过 `$log` 函数分别输出该对象、数字 `5` 和字符串 `'hello, world'` 到控制台。这是一个基础的调试和输出示例，展示了如何在 JessieCode 中打印不同类型的值。

## JessieCode 代码

```javascript
// Prepare some visual properties
cerise = <<
    strokeColor: '#901B77',
    fillColor: '#CA147A'
>>;

$log(cerise);
$log(5);
$log('hello, world');
```

## 知识点

1. **对象字面量语法**：使用 `<< >>` 定义对象/属性集合
2. **属性定义**：在对象内使用 `key: value` 形式定义属性
3. **字符串字面量**：使用单引号 `'string'` 定义字符串
4. **日志输出函数**：`$log()` 用于向控制台输出值
5. **注释语法**：使用 `//` 添加单行注释
6. **多类型支持**：JessieCode 支持对象、数字、字符串等多种数据类型

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `$log()` | JessieCode 内置的日志输出函数，用于调试和信息打印 | [JessieCode API - Output](https://jsxgraph.org/docs/symbols/JessieCode.html) |
| `<< >>` | JessieCode 特有的对象/属性集合字面量语法 | [JessieCode Syntax Guide](https://jsxgraph.org/docs/symbols/JessieCode.html) |

---

*来源：JessieCode 官方示例 - log.html*
