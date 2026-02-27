# 空字符串示例 / Empty String Example

## 图形描述

此示例演示在 JSXGraph 中创建 HTML 文本元素。代码使用 `text` 函数在坐标 (1, 1) 处创建一个文本标签，内容为 `<strong>hello</strong`（注意：这里 HTML 标签未正确闭合，缺少 `>`）。这展示了如何在 JSXGraph 中添加支持 HTML 格式的文本标注。

## JessieCode 代码

```javascript
t = text(1, 1, '<strong>hello</strong');
```

## 知识点

1. **文本元素创建**：`text(x, y, content)` 在指定坐标创建文本
2. **HTML 内容**：文本内容可包含 HTML 标签
3. **变量赋值**：将创建的元素赋值给变量 `t`
4. **字符串字面量**：使用单引号定义字符串

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `text` | 创建文本/HTML 标注元素 | [JSXGraph - Text](https://jsxgraph.org/docs/symbols/Text.html) |

---

*来源：JessieCode 官方示例 - emptystring.html*
