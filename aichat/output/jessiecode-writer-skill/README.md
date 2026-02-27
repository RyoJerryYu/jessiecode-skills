# jessiecode-writer 技能

## 技能描述

`jessiecode-writer` 是一个用于生成 JessieCode 代码的专业技能。当用户调用此技能时，它可以根据用户对几何图形或数学函数的描述，生成符合 JessieCode 语法规则的可运行代码。

## 使用场景

- 根据几何描述生成几何图形构造代码
- 根据函数描述生成函数图像代码
- 根据数学概念生成演示动画代码
- 根据用户需求修改或扩展现有 JessieCode 代码

## 技能结构

```
jessiecode-writer/
├── README.md              # 本文件（技能说明）
├── instructions.md        # 主要指令文档
└── references/
    ├── grammar.md         # 语法规则参考
    ├── api/               # JSXGraph 元素 API 文档
    └── examples/          # 示例代码库
```

## 参考资源

### 语法规则

- [grammar.md](references/grammar.md) - 完整的 JessieCode 语法规则参考

### API 文档

- [references/api/](references/api/) - JSXGraph 元素 API 文档（按元素名称组织）

### 示例代码

- [references/examples/from-official/](references/examples/from-official/) - 官方示例代码（24 个）
- [references/examples/from-user/](references/examples/from-user/) - 用户示例代码（14 个）

## 使用方法

在对话中调用 `/jessiecode-writer` 技能，并提供你的需求描述，例如：

```
/jessiecode-writer 帮我生成一个三角形的外接圆和内切圆的代码
```

或

```
/jessiecode-writer 创建一个演示欧拉线的几何图形，包含垂心、重心、外心
```

## 输出格式

技能将输出完整的 JessieCode 代码，使用 `jessiecode` 代码块包裹：

```jessiecode
// 生成的 JessieCode 代码
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
polygon(A, B, C);
```

## 质量保障

生成的代码遵循：
- 正确的 JessieCode 语法
- 清晰的代码结构
- 合理的样式设置
- 必要的注释说明

## 版本

v1.0 - 初始版本，包含完整的语法规则、API 文档和 38 个示例代码
