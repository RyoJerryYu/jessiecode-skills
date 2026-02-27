# JessieCode 版本兼容性

> 本文档说明 JessieCode 和相关依赖的版本信息

---

## JessieCode 版本

**当前文档基于**：JessieCode v1.x

JessieCode 是 JSXGraph 库的脚本语言，用于创建交互式几何图形和函数图像。

---

## JSXGraph 兼容性

**最低兼容版本**：JSXGraph v1.6.0+

JessieCode 作为 JSXGraph 的脚本层，与 JSXGraph 核心库紧密集成。

### 推荐的 JSXGraph 版本

- **生产环境**：JSXGraph v1.6.0 或更高版本
- **开发环境**：JSXGraph 最新稳定版

### 引入 JSXGraph

```html
<!-- CDN 引入（推荐） -->
<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/npm/jsxgraph@1.6.0/distrib/jsxgraph.css" />
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/jsxgraph@1.6.0/distrib/jsxgraphcore.js"></script>

<!-- 或使用本地文件 -->
<link rel="stylesheet" type="text/css" href="path/to/jsxgraph.css" />
<script type="text/javascript" src="path/to/jsxgraphcore.js"></script>
```

---

## 已知版本差异

### 幂运算符 `**`

| 特性 | 支持版本 | 说明 |
|------|---------|------|
| `**` 幂运算符 | v1.5+ | `x ** 2` 等价于 `x^2` |
| `^` 幂运算符 | 所有版本 | 传统幂运算符 |

**建议**：在 JessieCode 中优先使用 `^`，兼容性更好。

### `.toFixed()` 方法

| 特性 | 支持版本 | 说明 |
|------|---------|------|
| `.toFixed()` | 所有版本 | JavaScript 互操作，用于格式化数字 |

**示例**：
```js
text(0, 0, "距离 = " + dist(A, B).toFixed(2));
```

### 对象字面量语法

| 特性 | 支持版本 | 说明 |
|------|---------|------|
| `<< >>` | 所有版本 | JessieCode 对象字面量（标准） |
| `{}` | 不支持 | JavaScript 对象字面量（错误） |

**重要**：JessieCode 中**必须使用 `<< >>`** 创建对象字面量，不能使用 JavaScript 的 `{}`。

---

## JessieCode 语法版本

### 当前支持的语法特性

| 特性 | 状态 | 说明 |
|------|------|------|
| 基础数据类型 | ✅ | Boolean, String, Number |
| 对象字面量 `<< >>` | ✅ | 使用 `<< >>` 创建对象 |
| 函数声明 | ✅ | `function(x) { ... }` |
| 控制结构 | ✅ | if/while/do-while/for |
| 预定义常量 | ✅ | PI, EULER, $board 等 |
| 几何函数 | ✅ | point(), line(), circle() 等 |
| 属性访问 | ✅ | 使用 `.` 访问属性和方法 |
| 查找元素 | ✅ | `$('id')` 根据 ID 查找 |

### 不支持的 JavaScript 特性

| 特性 | 原因 | 替代方案 |
|------|------|---------|
| `var/let/const` | JessieCode 使用隐式声明 | 直接赋值 `x = 1` |
| 箭头函数 | 语法不支持 | 使用 `function(x) { ... }` |
| 模板字符串 | 不支持 | 使用字符串拼接 `'Hello, ' + name` |
| 解构赋值 | 不支持 | 逐个赋值 |
| 类 (class) | 不支持 | 使用对象和函数 |
| 模块导入 (import/export) | 有限支持 | 使用 JessieCode 的 `import` 语句 |

---

## 常见问题

### Q1: 如何查看当前使用的 JessieCode/JSXGraph 版本？

**A**: 在浏览器控制台运行：
```javascript
console.log(JXG.Version);  // JSXGraph 版本号
```

### Q2: 代码在旧版本 JSXGraph 中不工作怎么办？

**A**:
1. 升级到最新版本的 JSXGraph
2. 检查是否使用了新版本特性
3. 查阅 [JSXGraph 更新日志](https://github.com/jsxgraph/jsxgraph/blob/develop/ChangeLog.md)

### Q3: `**` 和 `^` 哪个更好？

**A**: 建议使用 `^`，原因：
- 所有版本都支持
- 数学记号更直观
- 与 JessieCode 文档一致

### Q4: 为什么不能使用 `{}` 创建对象？

**A**: JessieCode 使用 `<< >>` 以避免与 JavaScript 的块语句混淆。这是 JessieCode 的专用语法。

---

## 版本历史

| 日期 | JessieCode | JSXGraph | 重要变更 |
|------|-----------|----------|---------|
| 2024-01 | v1.x | v1.6.0 | 当前文档基准版本 |
| 2022-06 | v1.x | v1.5.0 | 添加 `**` 幂运算符支持 |
| 2020-01 | v1.x | v1.0.0 | JSXGraph 1.0 发布 |

---

## 参考资料

- [JSXGraph 官方文档](https://jsxgraph.org/)
- [JSXGraph GitHub](https://github.com/jsxgraph/jsxgraph)
- [JessieCode 语法参考](./grammar.md)

---

*最后更新：2026-02-27*
*基于改进计划 T2.3 任务*
