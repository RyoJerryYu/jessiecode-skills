## 任务描述

生成一个用于编写 JessieCode 的技能 `jessiecode-writer` 。当用户调用 `jessiecode-writer` 时，可以生成符合用户要求的 JessieCode 代码。

## 任务步骤

1. 调研：调研 JessieCode 的语法和用法，了解其特点、使用场景、语法规则、与 JSXGraph 的联系等。
2. 语法规则：阅读 JessieCode 的示例代码与文档，理解其语法规则，并编写可供 `jessiecode-writer` 中引用的语法规则文档。
3. API 文档：阅读 JSXGraph 的文档，了解其中各元素的属性和方法，并翻译为 `jessiecode-writer` 中可引用的 Markdown 文档。
4. 示例：将 JessieCode 的示例代码翻译为 `jessiecode-writer` 中可引用的示例代码。
5. 编写 `jessiecode-writer` 的技能文档。

## 安全规定(!!!important!!!)

- 所有产出必须位于 `@aichat/output/` 目录下。
- 不得修改 `@aichat/` 目录以外的文件。
- 每完成一个步骤，都暂停并等待用户检查产出。

## 步骤详细

### 输出目录结构

```
aichat/output/
├── 01-research/           # 调研报告
│   └── research-report.md
├── 02-grammar/            # 语法规则文档
│   └── grammar-reference.md
├── 03-api/                # API 文档
│   └── (按元素名称命名，如 Angle.md, Point.md 等)
├── 04-examples/           # 示例代码文档
│   ├── from-official/     # 官方示例
│   └── from-user/         # 用户提供的示例
└── 05-skill/              # 最终技能文档
    └── jessiecode-writer/
```

### 调研

调研内容：

- JessieCode 的背景、特点、使用场景
- JessieCode 的与 JSXGraph 的联系
- 其他你认为需要调研的内容

调研网站提示：

- JessieCode 的官方仓库： https://github.com/jsxgraph/JessieCode/tree/master
- JSXGraph 的文档： https://jsxgraph.org/docs/
- JSXGraph 文档中 JessieCode 相关的一页： https://jsxgraph.org/docs/symbols/JXG.JessieCode.html
- JessieCode 的官方仓库 README 已下载到本地 @JessieCode_README.md 中

步骤：

1. 阅读 @JessieCode_README.md 中的内容
2. 从互联网上搜索相关资料
3. 搜索完资料后，进行头脑风暴
4. 将搜索到的资料与头脑风暴的结果整理成一份调研报告。

产出：

- [ ] 调研报告

### 语法规则

阅读 JessieCode 的文档与示例代码，理解其语法规则，并编写可供 `jessiecode-writer` 中引用的语法规则 Markdown 文档。

可供阅读的文档：

- JessieCode 仓库 README： @JessieCode_README.md （已下载到本地）
- JessieCode 官方仓库示例代码： @JessieCode-examples/ （已下载到本地）
- 我之前编写的可用的 JessieCode 示例代码： @my-jessiecode-examples/

注意：JessieCode 官方仓库示例代码中，包含了完整的可渲染的 HTML 文档，但 `jessiecode-writer` 只需要编写其中 JessieCode 代码的部分。
比如 @JessieCode-examples/euler.html 中，`jessiecode-writer` 只需要编写其中的 `textarea` 标签中的内容。

注意：我之前编写的可用的 JessieCode 示例代码的 Markdown 文档中，`jessiecode` 代码块包裹了 JessieCode 代码与 frontmatter 。 `jessiecode-writer` 只需要编写其中 JessieCode 代码的部分。

产出：

- [ ] 语法规则文档（输出至 `02-grammar/grammar-reference.md`）

### API 文档

之前调研阶段已整理了 JessieCode 与 JSXGraph 的关系。 JessieCode 中可以使用的元素大多与 JSXGraph 中的元素一一对应。
需要阅读 JSXGraph 的文档，了解其中各元素的属性和方法，并翻译为 `jessiecode-writer` 中可引用的 Markdown 文档。

可供阅读的文档：

- JSXGraph 文档（HTML）： @jsxgraph-elements/ （已下载到本地）
- JSXGraph 文档（Markdown）： @jsxgraph-elements-transformed/ （已下载到本地）

@jsxgraph-elements-transformed/ 目录下的文档，是我之前已经用脚本从 html 文档提取出来的 Markdown 文档。
已去除 HTML 文档中无关紧要的 Style 、 Header 等大量无关内容。
但并不保证没有缺漏或错误转换。

由于文档内容量大，你需要按以下步骤分步产出：

1. 阅读文件系统结构，确认有多少文档，并填充下面 “API 文档产出清单” 中的 TODO List 项。
2. 先阅读其中 5 个示例文档，理解其内容并产出 5 份 API 文档 Markdown 文档。然后勾选对应的 TODO List 项，暂停并等待用户检查产出。
3. 第一轮用户检查通过后，你再以相同方法，每轮阅读 10 个文档，产出 10 份 API 文档 Markdown 文档。然后勾选对应的 TODO List 项，暂停并等待用户检查产出。
4. 直到所有文档都被阅读完毕。

产出：

- [ ] API 文档产出清单 TODO List
- [ ] 第一轮 5 份 API 文档
- [ ] API 文档产出清单中剩余的所有 API 文档

**质量验证**：
- 在转换过程中，如发现原文档有缺漏或错误，需在转换后的文档中添加备注说明
- 每轮产出后，随机抽取 1-2 份文档与原 JSXGraph 文档进行比对，确保翻译准确性

#### API 文档产出清单

- [ ] Angle.md
- [ ] ...（由 AI 填充剩余 TODO List 项）

### 示例

阅读 JessieCode 的示例代码，理解这些代码所代表的图形意义，从中提取并编写可供 `jessiecode-writer` 中引用的示例代码 Markdown 文档。

可供阅读的文档：

- JessieCode 官方仓库示例代码： @JessieCode-examples/ （已下载到本地）
- 我之前编写的可用的 JessieCode 示例代码： @my-jessiecode-examples/

输出的示例代码 Markdown 文档中，需要为每个示例代码添加一个标题，并附加这段代码所代表的图形意义的描述。

**质量验证**：
- 每轮产出后，随机抽取 1-2 份示例代码进行验证，确保代码可运行且描述准确

步骤：

1. 读取文件系统结构，确认有多少个示例代码，并填充下面 “示例代码产出清单” 中的 TODO List 项。
2. 阅读 @JessieCode-examples/ 目录下的 5 个示例代码，理解其图形意义，并编写 5 份示例代码 Markdown 文档。然后勾选对应的 TODO List 项，暂停并等待用户检查产出。
3. 第一轮用户检查通过后，你再以相同方法，每轮阅读 10 个示例代码，产出 10 份示例代码 Markdown 文档。然后勾选对应的 TODO List 项，暂停并等待用户检查产出。
4. 直到 @JessieCode-examples/ 目录下的所有示例代码都被阅读完毕。
5. 继续对 @my-jessiecode-examples/ 目录下的示例代码进行同样的步骤。
6. 直到 @my-jessiecode-examples/ 目录下的所有示例代码都被阅读完毕。

产出：
- [ ] 示例代码产出清单 TODO List
- [ ] 第一轮 5 份示例代码 Markdown 文档
- [ ] 示例代码产出清单中剩余的所有示例代码 Markdown 文档

#### 示例代码文档格式

每份示例代码文档应包含以下内容：
- 标题：示例名称
- 图形描述：这段代码所代表的图形意义
- JessieCode 代码：完整的 JessieCode 代码
- 知识点：涉及的 JessieCode/JSXGraph 知识点（可选）

#### 示例代码产出清单

@JessieCode-examples/ 目录下的示例代码：
- [ ] euler.md
- [ ] ...（由 AI 填充剩余 TODO List 项）

@my-jessiecode-examples/ 目录下的示例代码：
- [ ] 02-Examples/01-三角形外心.md
- [ ] ...（由 AI 填充剩余 TODO List 项）

## 产出

最后，将所有产出汇总，生成一个完整的 `jessiecode-writer` 的技能。

你可能需要使用 `/skill-creator` 技能，来生成 `jessiecode-writer` 的技能。

注意不要将所有内容都写入同一个 Markdown 文档，而是将内容拆分到 /references 中去。

### 技能文档结构

```
jessiecode-writer/
├── README.md              # 技能说明
├── instructions.md        # 主要指令文档
└── references/
    ├── grammar.md         # 语法规则（引用自 02-grammar/）
    ├── api/               # API 文档（引用自 03-api/）
    └── examples/          # 示例代码（引用自 04-examples/）
```

产出：

- [ ] `jessiecode-writer` 的技能文档

